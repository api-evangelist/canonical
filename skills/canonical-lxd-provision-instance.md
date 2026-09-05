---
name: canonical-lxd-provision-instance
description: >-
  Provision, inspect and safely tear down an LXD instance (container or VM) through the LXD REST API,
  handling the asynchronous operation model correctly and leaving a restore path behind.
api: canonical:lxd-rest-api
spec: openapi/canonical-lxd-rest-api-openapi.yml
operations:
  - server_get
  - projects_get
  - images_get
  - instances_post
  - operation_wait_get
  - operation_get
  - operation_delete
  - instance_get
  - instance_state_put
  - instance_snapshots_post
  - instance_put
  - instance_delete
generated: '2026-09-05'
method: generated
source: 'derived from openapi/canonical-lxd-rest-api-openapi.yml (Canonical LXD external REST API, Swagger 2.0, 333 operations) plus conventions/canonical-conventions.yml'
---

# Provision an LXD instance

LXD is Canonical's system container and VM manager. Its API lives at `/1.0` on the LXD host — a local
unix socket, or `https://<host>:8443` for remote access with a TLS client certificate or an OIDC
token. There is no Canonical-hosted LXD; the caller always talks to a server the caller (or their
operator) runs.

## Before you call anything: read the capability list

`server_get` — `GET /1.0` — returns `api_extensions[]`. LXD has been on path version `/1.0` since
2016 and never bumps it; new capability appears as a named extension in that array instead. If a
feature you plan to use is not in `api_extensions`, this server does not have it and the call will
fail with 501 Not Implemented.

Check for `etag` in the list before relying on step 6.

## 1. Pick a project

`projects_get` — `GET /1.0/projects`. Every collection in LXD is scoped by the `?project=` query
parameter. Omit it and you are silently operating in the `default` project. Pass it explicitly on
every call in this skill.

## 2. Find an image

`images_get` — `GET /1.0/images`. Add `?recursion=1` to inline the image objects instead of getting
back a list of URLs. Recursion is LXD's expansion mechanism — there is no `include[]` and no
`fields=`.

## 3. Create the instance

`instances_post` — `POST /1.0/instances`. This returns **202** with an `Operation` under
`/1.0/operations/{id}`, not the finished instance. Every write in LXD is asynchronous.

## 4. Wait for the operation

`operation_wait_get` — `GET /1.0/operations/{id}/wait` blocks until the operation resolves. Prefer it
over polling. If you must poll, use `operation_get` — `GET /1.0/operations/{id}` — and read the
numeric status code:

| Code | Meaning |
|---|---|
| 100 | Operation created |
| 101 | Started |
| 103 | Running |
| 104 | Canceling |
| 105 | Pending |
| 200 | Success |
| 400 | Failure |
| 401 | Canceled |

Anything below 200 is still in flight. 200 is the only success.

**If you need to back out mid-flight:** `operation_delete` — `DELETE /1.0/operations/{id}` — cancels
it. This only works while the operation is running; once it reaches 200 Success there is nothing to
cancel.

## 5. Start it

`instance_state_put` — `PUT /1.0/instances/{name}/state` with `{"action": "start"}`. Also
asynchronous: wait on the returned operation the same way. Valid actions include `start`, `stop`,
`restart`, `freeze` and `unfreeze`.

Confirm with `instance_get` — `GET /1.0/instances/{name}`.

## 6. Take a snapshot BEFORE you change anything

`instance_snapshots_post` — `POST /1.0/instances/{name}/snapshots`. Do this before any configuration
change you might want to undo. It is the reversal path for step 7 and it is the only one — LXD has no
undo for a configuration change that was not snapshotted first.

## 7. Change configuration safely

`instance_put` — `PUT /1.0/instances/{name}`. The contract's own summary is *"Updates the instance
configuration or trigger a snapshot restore"*: the update and the restore are the same operation.

Use the conditional-write guard:

1. `GET /1.0/instances/{name}` and keep the `ETag` response header.
2. `PUT` the modified object with `If-Match: <that etag>`.
3. A **412 Precondition Failed** means someone else changed the object since your read. Re-read and
   re-apply — do not retry the same body.

There is no `Idempotency-Key` anywhere in the LXD API. The ETag is the only replay protection, and it
covers updates, not creates. A retried `instances_post` will create a second instance.

To roll back, `PUT` with the `restore` field naming a snapshot.

## 8. Delete

`instance_delete` — `DELETE /1.0/instances/{name}`. Asynchronous. Once the operation reports 200
Success, the instance is gone; recovery is only possible from a snapshot or a backup taken earlier.

## Errors

LXD wraps everything in `{type, status_code|error_code, metadata|error}`. On failure `type` is
`"error"`, `error_code` mirrors the HTTP status, and `error` is a free-text string — there are no
enumerated sub-codes, so do not try to branch on the message.

- **403** is also returned for objects outside your project. A 403 does not prove the object exists.
- **423 Locked** means another operation holds the object. Poll `/1.0/operations` and retry.
- **501** means this build lacks the api_extension. Re-read `server_get`.
