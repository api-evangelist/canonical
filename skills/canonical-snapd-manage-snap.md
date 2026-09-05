---
name: canonical-snapd-manage-snap
description: >-
  Install, refresh, revert and remove snaps on an Ubuntu host through the local snapd REST API,
  tracking the asynchronous change model and preserving the 31-day restore window.
api: canonical:snapd-rest-api
spec: openapi/canonical-snapd-rest-api-openapi.yml
operations:
  - getSystemInfo
  - findSnaps
  - listInstalledSnaps
  - getInstalledSnapByName
  - manageSnapByName
  - getChangeById
  - abortChangeById
  - listSnapshots
  - getNotices
generated: '2026-09-05'
method: generated
source: 'derived from openapi/canonical-snapd-rest-api-openapi.yml (Snapd REST API, OpenAPI 3.0.3, 64 operations) plus https://snapcraft.io/docs/reference/administration/system-options/'
---

# Manage snaps through the snapd REST API

snapd exposes a REST API over a **unix domain socket**, not a network port. The servers declared in
the contract are `unix:///run/snapd.socket` (full access) and `unix:///run/snapd-snap.socket` (the
restricted socket a confined snap gets). There is no bearer token: authorization is decided from unix
socket peer credentials (`SO_PEERCRED`), which the contract declares as the `PeerAuth` scheme. If you
can reach the socket with the right group membership, you are authorized; if you cannot, no header
will help you.

## 1. Learn what this system is

`getSystemInfo` — `GET /v2/system-info`. Returns the snapd version, the refresh schedule, and the
confinement modes this kernel supports. Read it before assuming a feature exists.

## 2. Find and inspect

- `findSnaps` — `GET /v2/find?q=<term>` searches the store.
- `listInstalledSnaps` — `GET /v2/snaps` lists what is on the system.
- `getInstalledSnapByName` — `GET /v2/snaps/{name}` for one snap, including its current revision and
  channel.

Record the current revision before you change anything. It is what you revert to.

## 3. Mutate

`manageSnapByName` — `POST /v2/snaps/{name}` with a body of `{"action": "<action>"}`. The contract
enumerates the actions:

`install`, `refresh`, `remove`, `revert`, `enable`, `disable`, `switch`, `hold`, `unhold`

Optional fields include `channel`, `revision`, `classic`, `devmode` and `purge`.

This is **asynchronous**. The response is a change id, not a result.

## 4. Follow the change

`getChangeById` — `GET /v2/changes/{id}`. Poll until the change reports `Done` or `Error`. For an
event-driven alternative, `getNotices` — `GET /v2/notices` — long-polls system notices.

**To back out mid-flight:** `abortChangeById` — `POST /v2/changes/{id}` with `{"action": "abort"}`.

## 5. Undo a bad refresh

`manageSnapByName` with `{"action": "revert"}` puts the snap back on its previous revision. Pass
`revision` to name a specific one.

The window is real but bounded: the `refresh.retain` system option controls how many revisions snapd
keeps on disk. Once a revision has been garbage-collected there is nothing to revert to. Check
`refresh.retain` on the host before promising a rollback.

## 6. Undo a removal

By default, `{"action": "remove"}` takes an **automatic snapshot** of the snap's data first.
Canonical publishes the window plainly: *"Automatic snapshot retention time is configured with the
`snapshots.automatic.retention` system option. The default value is 31 days."*

- `listSnapshots` — `GET /v2/snapshots` — shows the snapshot sets available to restore.
- Passing `purge: true` on the remove **suppresses the snapshot entirely**. There is then no
  restore path. Never pass `purge: true` on behalf of a user who did not ask for it.
- If the host has `snapshots.automatic.retention` set to `no`, automatic snapshots are disabled and
  every removal is irreversible. Check before removing.

## Errors

snapd nests the failure under `result` as `{message, kind, value}`, and — unusually for this
portfolio — the `kind` values are **enumerated in the contract**. Branch on `kind`, never on
`message`:

| kind | meaning | what to do |
|---|---|---|
| `snap-change-conflict` | another change is already running for this snap | poll `/v2/changes` and retry after it finishes; do not start a second change |
| `snap-not-found` / `snap-not-installed` | the snap is not present | re-read `/v2/snaps` |
| `assertion-not-found` | no model or serial assertion yet | the system is not fully seeded |
| `option-not-available` / `option-not-found` | unknown confdb option | check `getSystemInfo` |

There is no `Idempotency-Key`. Replay safety comes from the conflict model: a duplicate mutating call
while a change is in flight returns 409 `snap-change-conflict` rather than starting a second change.
