# FríoTrack API

Planned backend for FríoTrack, a cold-chain shipment monitoring product by BlackStartup for UPC course 1ASI0730, section 8088, term 202620.

## Current status

This repository contains **AV2 preparation and TB1 design documentation**. It has no executable API, implemented endpoints, database instance, migrations, authentication service, or backend tests. The current frontend is a local demonstration with browser storage; successful frontend tests or builds do not verify a backend or a cloud deployment.

The planned stack is **C#, ASP.NET Core, Entity Framework Core, and PostgreSQL**. Framework and database versions will be selected and documented when implementation begins. AWS or Azure hosting remains pending a cloud account and a separate deployment authorization.

## Planned domain boundaries

| Bounded context | Planned responsibilities |
| --- | --- |
| Identity and Access Management (IAM) | Organizations, accounts, roles, authentication, password recovery, and authorization. |
| Fleet | Vehicles, drivers, sensors, and time-bounded resource allocation. |
| Shipment | Scheduling, assigned customers, shipment lifecycle, and history. |
| Monitoring | Environmental snapshots, sensor readings, positions, and signal health. |
| Alert and Reporting | Excursions, corrective actions, notifications, incidents, and thermal reports. |

Domain, application, infrastructure, and presentation responsibilities are intended to remain separate during implementation. The [editable design catalog](docs/design/backend-model-tb1.json) describes 17 proposed relational tables and 27 persistent relationships; these are design artifacts, not an applied schema.

## Rules to preserve during implementation

- Capture minimum and maximum temperature, minimum and maximum relative humidity, and time tolerance when monitoring begins. Retain this snapshot so later edits cannot rewrite historical evaluation.
- Evaluate both environmental ranges inclusively. Acknowledging an excursion records an action while keeping it open; a later reading within **both** ranges is required for resolution.
- Validate the departure/arrival interval, positive shipment weight, and vehicle capacity. Create shipments and active resource reservations atomically and prevent overlapping vehicle or driver reservations.
- The planned lifecycle includes `DRAFT`, `SCHEDULED`, `IN_TRANSIT`, `DELIVERED`, and `CANCELLED`. Planned cancellation is limited to `DRAFT` or `SCHEDULED` and releases reservations. The current frontend persists no drafts and permits cancellation **only while scheduled**; it rejects cancellation during transit and after delivery.
- Enforce organization/resource access and assigned-customer permissions on the future server. Browser role selection does not establish server authorization or tenant isolation.
- Stop monitoring after delivery or cancellation. Time tolerance, maximum signal silence, severity handling, credentials, and persistence are planned backend behavior; the local frontend does not verify those services.

## Design sources

- [Backend classes (PlantUML)](docs/design/backend-classes-tb1.puml)
- [Relational model (Mermaid)](docs/design/database-tb1.mmd)
- [Catalog, constraints, and requirement references (JSON)](docs/design/backend-model-tb1.json)
- [Provenance and validation limits](docs/design/PROVENANCE.md)

The authoritative requirements and design discussion are maintained in [report-friotrack](https://github.com/upc-pre-202620-1asi0730-8088-FrioTrack/report-friotrack), specifically `report/13-chapter3-requirements-spec.md`, `report/14-chapter4-product-design.md`, and `report/TB1_CHECKLIST.md`. The design files here are documented snapshots of that source, not an independently approved implementation contract.

The product's existing landing is maintained in [friotrack-landing](https://github.com/upc-pre-202620-1asi0730-8088-FrioTrack/friotrack-landing). The operational frontend belongs in the separate `friotrack-frontend` repository.

## Development workflow

Use `develop` for integration and `feature/<scope>-<action>` branches for coherent changes, with pull requests targeting `develop`. Commit titles and bodies must be in English and follow Conventional Commits. Stable releases belong on `main`; no release or deployment is established by this initial documentation.

Before implementation, the team must validate requirements, confirm technology versions, define and review API contracts, and select real deployment and database configuration. Only add executable project files, migrations, credentials integration, or tests when those components have actually been implemented and verified.
