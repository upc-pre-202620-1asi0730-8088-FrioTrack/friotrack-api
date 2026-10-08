# Design snapshot provenance

These files were copied byte-for-byte from the local TB1 report sources on **2026-10-08 at 00:18 UTC (2026-10-07 in Lima)**. Their catalog is dated 2026-10-07 and identifies itself as `planned_backend_design_not_implementation`.

Source repository: [report-friotrack](https://github.com/upc-pre-202620-1asi0730-8088-FrioTrack/report-friotrack). Original paths and SHA-256 digests:

| Source path | SHA-256 |
| --- | --- |
| `report/assets/architecture/backend-model-tb1.json` | `5f58d838d5d2290fe11f4e3be20160057da2973142ccb064f8c4695ec1ea843d` |
| `report/assets/architecture/backend-classes-tb1.puml` | `476daf771275b65818d11f4a381e1172738b4090e967278555fbd64666d003cd` |
| `report/assets/architecture/database-tb1.mmd` | `0558213ea081647e3ab3f6322d5e6cd7e7c8387fd474edbae79b837f76e1b668` |

The original report paths in the catalog's `frontEndSources` property refer to the report workspace at snapshot time. They are provenance references, not paths that resolve inside this API repository. The standalone frontend carries the corresponding `src/domains/operations.js` and `src/domains/seed.js` files.

## Validation scope

The preparation check parsed the JSON catalog, counted **17 entities and 27 persistent relationships**, and verified that each copied file matches its source SHA-256 digest. Report review also distinguishes scheduled-only cancellation in the current demo from the future draft lifecycle and preserves environmental snapshot constraints.

No PlantUML or Mermaid compiler, .NET build, API request, database engine, SQL schema, migration, authentication flow, or backend test was executed during this preparation. Rendered report panels and their visual checks remain with the report; no rendered copies are included here.

Review and update these designs against actual requirements before implementing a backend. Any later change to the copied sources should record its purpose and update this provenance statement rather than imply that a design-only artifact is operational.
