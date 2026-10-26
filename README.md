# Canonical (canonical)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Canonical is the company behind Ubuntu, the world's most popular open source operating system for cloud, servers, desktops, IoT, and Kubernetes. Canonical publishes a broad set of developer APIs spanning the Ubuntu and Canonical ecosystem — the Snap Store and Snapcraft, the Charmhub charm marketplace, LXD system containers, MAAS bare-metal provisioning, Juju orchestration, Launchpad project hosting, Ubuntu Pro subscription services, and Landscape systems management — most of which are RESTful, open, and well documented.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/canonical/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/canonical/refs/heads/main/apis.yml)

## Scope

- **Type:** Index
- **Position:** Provider
- **Access:** Open

## Tags

- Cloud
- Linux
- Open Source
- Ubuntu
- Containers
- Bare Metal
- Charms
- Identity

## Timestamps

- **Created:** 2026-03-16
- **Modified:** 2026-04-23

## APIs

### Snap Store API

The public Snap Store Device API (api.snapcraft.io) serves information about snaps, revisions, channels, tracks, assertions, and refresh state to snap clients. The Snapcraft Dashboard API (dashboard.snapcraft.io) lets snap publishers manage releases, brand stores, and snap metadata programmatically.

- **Human URL:** [https://api.snapcraft.io/docs/](https://api.snapcraft.io/docs/)
- **Base URL:** `https://api.snapcraft.io`

#### Tags

- Snaps
- Store
- Packaging

#### Properties

- [Documentation](https://api.snapcraft.io/docs/)
- [Dashboard A P I](https://dashboard.snapcraft.io/docs/reference/v2/en/index.html)
- [How To](https://snapcraft.io/docs/using-the-api)
- [Postman Collection](collections/canonical.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/canonical.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Charmhub API

Developer-facing REST API for Charmhub, Canonical's marketplace for charms (Kubernetes and machine operators). Supports charm discovery, publishing, release channels, and token exchange — macaroons issued by dashboard.snapcraft.io SSO are exchanged for Charmhub developer tokens used in the Authorization header.

- **Human URL:** [https://api.charmhub.io/docs/default.html](https://api.charmhub.io/docs/default.html)
- **Base URL:** `https://api.charmhub.io`

#### Tags

- Charms
- Operators
- Kubernetes

#### Properties

- [Documentation](https://api.charmhub.io/docs/default.html)
- [Portal](https://charmhub.io/)
- [Postman Collection](collections/canonical.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/canonical.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### snapd REST API

The local REST API exposed by snapd over a Unix domain socket on every Ubuntu system running snaps. Enables local clients and tools to query snap state, install / refresh / remove snaps, manage interfaces and connections, and read system information.

- **Human URL:** [https://snapcraft.io/docs/reference/development/snapd-rest-api/](https://snapcraft.io/docs/reference/development/snapd-rest-api/)

#### Tags

- Local
- System
- Snaps

#### Properties

- [Documentation](https://snapcraft.io/docs/reference/development/snapd-rest-api/)
- [How To](https://snapcraft.io/docs/how-to-guides/snap-development/use-the-rest-api/)
- [Postman Collection](collections/canonical.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/canonical.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### LXD REST API

The REST API exposed by LXD, Canonical's system-container and VM manager. All client–daemon communication happens over HTTPS (remote) or a Unix socket (local). Provides endpoints for instances, images, networks, storage pools, profiles, projects, cluster members, and events. Fully documented in an auto-generated OpenAPI (Swagger) spec.

- **Human URL:** [https://documentation.ubuntu.com/lxd/latest/rest-api/](https://documentation.ubuntu.com/lxd/latest/rest-api/)
- **Base URL:** `https://<host>:8443/1.0`

#### Tags

- Containers
- Virtualisation
- OpenAPI

#### Properties

- [Documentation](https://documentation.ubuntu.com/lxd/latest/rest-api/)
- [OpenAPI](https://github.com/canonical/lxd/blob/main/doc/rest-api.yaml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Reference](https://linuxcontainers.org/lxd/rest-api/)
- [Postman Collection](collections/canonical.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/canonical.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### MAAS API

The RESTful API for MAAS (Metal as a Service). Everything the MAAS UI can do — commissioning, allocation, deployment, DHCP/DNS, tags, zones, pools, users, machines — is available through the API, making bare- metal infrastructure programmable and suitable for Infrastructure as Code workflows. Python and CLI bindings are provided.

- **Human URL:** [https://canonical.com/maas/docs/api](https://canonical.com/maas/docs/api)
- **Base URL:** `https://<maas-host>/MAAS/api/2.0`

#### Tags

- Bare Metal
- Provisioning
- Infrastructure

#### Properties

- [Documentation](https://canonical.com/maas/docs/api)
- [Overview](https://canonical.com/maas)
- [Portal](https://maas.io/docs)
- [Postman Collection](collections/canonical.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/canonical.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Juju Client / Controller API

Juju is Canonical's open-source orchestration engine for deploying, integrating, scaling, and managing applications on clouds, MAAS, LXD, and Kubernetes via charms. Juju clients communicate with a controller over a websocket-based API; Python and Go libraries plus the juju CLI consume this API.

- **Human URL:** [https://documentation.ubuntu.com/juju/](https://documentation.ubuntu.com/juju/)

#### Tags

- Orchestration
- DevOps
- Charms

#### Properties

- [Documentation](https://documentation.ubuntu.com/juju/)
- [Overview](https://canonical.com/juju)
- [Architecture](https://canonical.com/juju/juju-architecture)
- [Postman Collection](collections/canonical.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/canonical.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Launchpad Web Services API

Launchpad exposes a RESTful Web Services API over its project hosting, bug tracking, code, builds, translations, and distribution data. The API is authenticated with OAuth; anonymous access gives read-only access to public data. The launchpadlib Python library is the officially supported client.

- **Human URL:** [https://documentation.ubuntu.com/launchpad/user/how-to/launchpad-api/](https://documentation.ubuntu.com/launchpad/user/how-to/launchpad-api/)
- **Base URL:** `https://api.launchpad.net/`

#### Tags

- OAuth
- Open Source
- Project Hosting

#### Properties

- [Documentation](https://documentation.ubuntu.com/launchpad/user/how-to/launchpad-api/)
- [Reference](https://help.launchpad.net/API)
- [Client Library](https://launchpadlib.readthedocs.io/en/latest/introduction.html)
- [Portal](https://api.launchpad.net/)
- [Postman Collection](collections/canonical.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/canonical.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Ubuntu Pro Client API

The Ubuntu Pro client exposes a local API/CLI for managing Ubuntu Pro subscription services on a host — enabling, disabling, and inspecting Extended Security Maintenance (ESM), Livepatch, FIPS, compliance tooling (CIS, DISA-STIG), USG, and Landscape integration.

- **Human URL:** [https://documentation.ubuntu.com/pro/](https://documentation.ubuntu.com/pro/)

#### Tags

- ESM
- Livepatch
- FIPS
- Compliance
- Subscription

#### Properties

- [Documentation](https://documentation.ubuntu.com/pro/)
- [Client Docs](https://documentation.ubuntu.com/pro-client/en/latest/)
- [Portal](https://ubuntu.com/pro)
- [Postman Collection](collections/canonical.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/canonical.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Landscape API

Canonical Landscape is the systems-management platform for Ubuntu at scale. Its API lets operators manage and automate inventories, upgrades, patch compliance, reboots, scripts, monitoring, and alerts across fleets of Ubuntu machines (on-prem, hybrid, or hosted Landscape SaaS).

- **Human URL:** [https://ubuntu.com/landscape/docs](https://ubuntu.com/landscape/docs)

#### Tags

- Systems Management
- Patch Management
- Fleet

#### Properties

- [Documentation](https://ubuntu.com/landscape/docs)
- [Portal](https://ubuntu.com/landscape)
- [Postman Collection](collections/canonical.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/canonical.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Common Properties

- [LinkedIn](https://www.linkedin.com/company/canonical)
- [Website](https://canonical.com/)
- [Ubuntu Website](https://ubuntu.com/)
- [Documentation](https://documentation.ubuntu.com/)
- [Git Hub Org](https://github.com/canonical)
- [Snap Store](https://snapcraft.io/)
- [Charmhub](https://charmhub.io/)
- [Launchpad](https://launchpad.net/)
- [Discourse Forum](https://discourse.ubuntu.com/)
- [Data Privacy](https://ubuntu.com/legal/data-privacy)
- [Terms of Service](https://ubuntu.com/legal/terms)
- [Integrations](https://canonical.com/partners)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
