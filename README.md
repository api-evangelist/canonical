# Canonical (canonical)

Canonical is the company behind Ubuntu, the world's most popular open source operating system for cloud, servers, desktops, IoT, and Kubernetes. Canonical publishes a broad set of developer APIs spanning the Ubuntu and Canonical ecosystem — the Snap Store and Snapcraft, the Charmhub charm marketplace, LXD system containers, MAAS bare-metal provisioning, Juju orchestration, Launchpad project hosting, Ubuntu Pro subscription services, and Landscape systems management — most of which are RESTful, open, and well documented.

**URL:** [Visit APIs.json URL](https://raw.githubusercontent.com/api-evangelist/canonical/refs/heads/main/apis.yml)

## Scope

- **Type:** Index
- **Position:** Provider
- **Access:** Open

## Tags

 - Cloud, Linux, Open Source, Ubuntu, Containers, Bare Metal, Charms, Identity

## Timestamps

- **Created:** 2026-03-16
- **Modified:** 2026-04-23

## APIs

### Snap Store API

The public Snap Store Device API (api.snapcraft.io) serves information about snaps, revisions, channels, tracks, assertions, and refresh state to snap clients. The Snapcraft Dashboard API (dashboard.snapcraft.io) lets snap publishers manage releases, brand stores, and snap metadata programmatically.

**Human URL:** [https://api.snapcraft.io/docs/](https://api.snapcraft.io/docs/)

#### Tags

 - Snaps, Store, Packaging

#### Properties

- [Documentation](https://api.snapcraft.io/docs/)
- [Dashboard API](https://dashboard.snapcraft.io/docs/reference/v2/en/index.html)
- [How-To](https://snapcraft.io/docs/using-the-api)

### Charmhub API

Developer-facing REST API for Charmhub, Canonical's marketplace for charms (Kubernetes and machine operators). Supports charm discovery, publishing, release channels, and token exchange — macaroons issued by dashboard.snapcraft.io SSO are exchanged for Charmhub developer tokens used in the Authorization header.

**Human URL:** [https://api.charmhub.io/docs/default.html](https://api.charmhub.io/docs/default.html)

#### Tags

 - Charms, Operators, Kubernetes

#### Properties

- [Documentation](https://api.charmhub.io/docs/default.html)
- [Portal](https://charmhub.io/)

### snapd REST API

The local REST API exposed by snapd over a Unix domain socket on every Ubuntu system running snaps. Enables local clients and tools to query snap state, install / refresh / remove snaps, manage interfaces and connections, and read system information.

**Human URL:** [https://snapcraft.io/docs/reference/development/snapd-rest-api/](https://snapcraft.io/docs/reference/development/snapd-rest-api/)

#### Tags

 - Local, System, Snaps

#### Properties

- [Documentation](https://snapcraft.io/docs/reference/development/snapd-rest-api/)
- [How-To](https://snapcraft.io/docs/how-to-guides/snap-development/use-the-rest-api/)

### LXD REST API

The REST API exposed by LXD, Canonical's system-container and VM manager. All client–daemon communication happens over HTTPS (remote) or a Unix socket (local). Provides endpoints for instances, images, networks, storage pools, profiles, projects, cluster members, and events. Fully documented in an auto-generated OpenAPI (Swagger) spec.

**Human URL:** [https://documentation.ubuntu.com/lxd/latest/rest-api/](https://documentation.ubuntu.com/lxd/latest/rest-api/)

#### Tags

 - Containers, Virtualisation, OpenAPI

#### Properties

- [Documentation](https://documentation.ubuntu.com/lxd/latest/rest-api/)
- [OpenAPI](https://github.com/canonical/lxd/blob/main/doc/rest-api.yaml)
- [Reference](https://linuxcontainers.org/lxd/rest-api/)

### MAAS API

The RESTful API for MAAS (Metal as a Service). Everything the MAAS UI can do — commissioning, allocation, deployment, DHCP/DNS, tags, zones, pools, users, machines — is available through the API, making bare-metal infrastructure programmable and suitable for Infrastructure as Code workflows. Python and CLI bindings are provided.

**Human URL:** [https://canonical.com/maas/docs/api](https://canonical.com/maas/docs/api)

#### Tags

 - Bare Metal, Provisioning, Infrastructure

#### Properties

- [Documentation](https://canonical.com/maas/docs/api)
- [Overview](https://canonical.com/maas)
- [Portal](https://maas.io/docs)

### Juju Client / Controller API

Juju is Canonical's open-source orchestration engine for deploying, integrating, scaling, and managing applications on clouds, MAAS, LXD, and Kubernetes via charms. Juju clients communicate with a controller over a websocket-based API; Python and Go libraries plus the juju CLI consume this API.

**Human URL:** [https://documentation.ubuntu.com/juju/](https://documentation.ubuntu.com/juju/)

#### Tags

 - Orchestration, DevOps, Charms

#### Properties

- [Documentation](https://documentation.ubuntu.com/juju/)
- [Overview](https://canonical.com/juju)
- [Architecture](https://canonical.com/juju/juju-architecture)

### Launchpad Web Services API

Launchpad exposes a RESTful Web Services API over its project hosting, bug tracking, code, builds, translations, and distribution data. The API is authenticated with OAuth; anonymous access gives read-only access to public data. The launchpadlib Python library is the officially supported client.

**Human URL:** [https://documentation.ubuntu.com/launchpad/user/how-to/launchpad-api/](https://documentation.ubuntu.com/launchpad/user/how-to/launchpad-api/)

#### Tags

 - OAuth, Open Source, Project Hosting

#### Properties

- [Documentation](https://documentation.ubuntu.com/launchpad/user/how-to/launchpad-api/)
- [Reference](https://help.launchpad.net/API)
- [Client Library](https://launchpadlib.readthedocs.io/en/latest/introduction.html)
- [Portal](https://api.launchpad.net/)

### Ubuntu Pro Client API

The Ubuntu Pro client exposes a local API/CLI for managing Ubuntu Pro subscription services on a host — enabling, disabling, and inspecting Extended Security Maintenance (ESM), Livepatch, FIPS, compliance tooling (CIS, DISA-STIG), USG, and Landscape integration.

**Human URL:** [https://documentation.ubuntu.com/pro/](https://documentation.ubuntu.com/pro/)

#### Tags

 - ESM, Livepatch, FIPS, Compliance, Subscription

#### Properties

- [Documentation](https://documentation.ubuntu.com/pro/)
- [Client Docs](https://documentation.ubuntu.com/pro-client/en/latest/)
- [Portal](https://ubuntu.com/pro)

### Landscape API

Canonical Landscape is the systems-management platform for Ubuntu at scale. Its API lets operators manage and automate inventories, upgrades, patch compliance, reboots, scripts, monitoring, and alerts across fleets of Ubuntu machines (on-prem, hybrid, or hosted Landscape SaaS).

**Human URL:** [https://ubuntu.com/landscape/docs](https://ubuntu.com/landscape/docs)

#### Tags

 - Systems Management, Patch Management, Fleet

#### Properties

- [Documentation](https://ubuntu.com/landscape/docs)
- [Portal](https://ubuntu.com/landscape)

## Use Cases

- Package publishers and CI/CD pipelines releasing snaps and charms via the Snapcraft Dashboard and Charmhub APIs.
- Cloud-init / cloud-image and IoT vendors querying the Snap Store Device API to compose and refresh image content.
- DevOps teams scripting bare-metal lifecycle via MAAS and composing workloads on top via Juju and LXD.
- Multi-cloud platform teams using the LXD REST API to manage system containers and VMs as cattle.
- Open-source projects hosted on Launchpad automating bug triage, PPAs, code imports, and builds via the Launchpad Web Services API.
- Enterprises using Ubuntu Pro's local API to enable ESM / FIPS / Livepatch at scale in config-management workflows.
- Large Ubuntu fleets using Landscape to enforce patch compliance, perform mass upgrades, and report security posture.

## Common Properties

- [Website](https://canonical.com/)
- [Ubuntu Website](https://ubuntu.com/)
- [Documentation](https://documentation.ubuntu.com/)
- [GitHub Organization](https://github.com/canonical)
- [Snap Store](https://snapcraft.io/)
- [Charmhub](https://charmhub.io/)
- [Launchpad](https://launchpad.net/)
- [Discourse Forum](https://discourse.ubuntu.com/)
- [Data Privacy](https://ubuntu.com/legal/data-privacy)
- [Terms of Service](https://ubuntu.com/legal/terms)

## Maintainers

**FN:** Kin Lane

**Email:** kin@apievangelist.com
