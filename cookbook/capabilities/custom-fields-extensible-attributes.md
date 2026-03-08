# Custom Fields / Extensible Attributes

## What this capability is
- extensibility with predictable queryability, validation, and governance.

## When to use it
- Use when tenants or admins must add new fields without schema redeploys.
- Common across CRM, ticketing, catalog, and content-oriented systems.

## When not to use it
- Do not treat this capability as a broad catch-all; keep adjacent concerns in separate capabilities.

## Core behaviors
- Admin defines field with type, scope, validation, and permissions.
- System validates definition and persists field registry entry.
- Optional worker backfills defaults and updates indexes.
- Users submit entity data including new field values.
- API enforces validation and ACL, then stores values.
- Query layer exposes field in supported filter and export paths.

## Typical components
- Field-definition CRUD endpoints.
- Validation and preview endpoint for proposed definitions.
- Entity read and write endpoints supporting extension payloads.
- Query endpoints with explicit support matrix for filterable field types.
- Admin schema builder for adding and modifying fields.
- Entity forms that render dynamic fields by scope.
- List filters exposing indexable custom fields.
- Deprecation and migration warning surfaces.
- Backfill and reindex worker for new filterable fields.
- Schema migration worker for type changes.
- Validation audit worker for legacy data conformance.

## Key data concepts
- Field registry (key, label, type, scope, validation rules, lifecycle state)
- Value storage model (JSON column, EAV tables, or typed extension tables)
- Field-level ACL metadata
- Index strategy metadata for filterable fields
- Migration history for field type or definition changes

## Common workflows
- JSON-centric model for rapid extensibility.
- EAV model for high cardinality and dynamic schemas.
- Typed extension tables for strong query performance.
- Hybrid model where high-value fields are promoted from dynamic to typed.

## Integration touchpoints
- Field-definition CRUD endpoints.
- Validation and preview endpoint for proposed definitions.
- Entity read and write endpoints supporting extension payloads.
- Query endpoints with explicit support matrix for filterable field types.

## Risks / failure modes
- Unindexed high-cardinality fields slowing list queries -> enforce index policy and field caps.
- Field type mutation breaking historical values -> require migration plan and compatibility checks.
- ACL drift exposing sensitive custom fields -> evaluate field-level policy at read and write.
- Conflicting field keys across scopes -> namespace by tenant and entity type.
- Overuse of dynamic fields creating schema entropy -> governance thresholds and review workflow.
- Search filters referencing deprecated fields -> soft deprecation window and auto-migration helpers.
- Support field-level masking for sensitive data.
- Require explicit PII classification tags on field creation.

## Related archetypes
- CRM: tenant-specific customer segmentation fields.
- Case/Ticket: category-specific intake attributes.
- Inventory/Catalog: product attributes and merchandising dimensions.
- CMS/DMS: document metadata extensions.

## Related capabilities
- [query-filtering](query-filtering.md)
- [saved-views](saved-views.md)
- [search-index](search-index.md)
- [import-export-pipelines](import-export-pipelines.md)


