# Custom Fields / Extensible Attributes

## Problem / when to use
- Use when tenants or admins must add new fields without schema redeploys.
- Common across CRM, ticketing, catalog, and content-oriented systems.
- Goal: extensibility with predictable queryability, validation, and governance.

## Ingredients
### Data model components
- Field registry (key, label, type, scope, validation rules, lifecycle state)
- Value storage model (JSON column, EAV tables, or typed extension tables)
- Field-level ACL metadata
- Index strategy metadata for filterable fields
- Migration history for field type or definition changes

### API contracts
- Field-definition CRUD endpoints.
- Validation and preview endpoint for proposed definitions.
- Entity read and write endpoints supporting extension payloads.
- Query endpoints with explicit support matrix for filterable field types.

### UI surfaces
- Admin schema builder for adding and modifying fields.
- Entity forms that render dynamic fields by scope.
- List filters exposing indexable custom fields.
- Deprecation and migration warning surfaces.

### Jobs/workers/async components
- Backfill and reindex worker for new filterable fields.
- Schema migration worker for type changes.
- Validation audit worker for legacy data conformance.

## Reference flow (happy path + async path)
1. Admin defines field with type, scope, validation, and permissions.
2. System validates definition and persists field registry entry.
3. Optional worker backfills defaults and updates indexes.
4. Users submit entity data including new field values.
5. API enforces validation and ACL, then stores values.
6. Query layer exposes field in supported filter and export paths.

## Variants
- JSON-centric model for rapid extensibility.
- EAV model for high cardinality and dynamic schemas.
- Typed extension tables for strong query performance.
- Hybrid model where high-value fields are promoted from dynamic to typed.

## Failure modes & mitigations
- Unindexed high-cardinality fields slowing list queries → enforce index policy and field caps.
- Field type mutation breaking historical values → require migration plan and compatibility checks.
- ACL drift exposing sensitive custom fields → evaluate field-level policy at read and write.
- Conflicting field keys across scopes → namespace by tenant and entity type.
- Overuse of dynamic fields creating schema entropy → governance thresholds and review workflow.
- Search filters referencing deprecated fields → soft deprecation window and auto-migration helpers.

## Security/privacy considerations
- Support field-level masking for sensitive data.
- Require explicit PII classification tags on field creation.
- Restrict field-definition changes to privileged admin roles.
- Audit all schema changes and bulk edits.

## Observability requirements
### Trace spans
- Field-definition create and update transaction.
- Dynamic form render with schema lookup.
- Entity write with dynamic validation path.
- Reindex and backfill job execution.

### Metrics
- Dynamic field validation failure rate.
- Reindex backlog and duration.
- Query latency by dynamic field usage.
- Field-definition churn rate.
- Deprecated field usage count.

### Structured logs/audit events
- Field-definition lifecycle events.
- Validation failures by field and rule.
- ACL evaluation outcomes for sensitive fields.
- Backfill and migration execution logs.

## Testing checklist
### Unit
- Field-definition validator.
- Type coercion and constraint evaluation.
- Field-level ACL checks.

### Integration
- End-to-end schema change to runtime form rendering.
- Query and filter behavior for indexed fields.
- Export and import compatibility with dynamic fields.

### Failure injection/chaos-lite checks
- Mid-write schema update race.
- Reindex worker interruption and recovery.
- Large payload submissions with mixed valid and invalid dynamic fields.

## Operational runbook checklist
- Review schema change request and impact report.
- Validate index and migration prerequisites.
- Roll out schema changes in staged mode.
- Monitor validation errors and query latency post-deploy.
- Roll back or deprecate problematic fields with migration notes.

## Adoption notes by archetype
- CRM: tenant-specific customer segmentation fields.
- Case/Ticket: category-specific intake attributes.
- Inventory/Catalog: product attributes and merchandising dimensions.
- CMS/DMS: document metadata extensions.

## Licensing & source attribution notes
- Keep this capability description as original synthesis.
- Cite supporting patterns and OSS references with attribution.
- Avoid copying proprietary schema-builder docs.
