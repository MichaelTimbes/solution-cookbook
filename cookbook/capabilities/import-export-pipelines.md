# Import / Export Pipelines

## What this capability is
- reliable high-volume transfer with clear error isolation and replay controls.

## When to use it
- Use when systems must ingest or emit bulk structured data with validation, mapping, and operational controls.
- Common for migrations, partner feeds, catalog syncs, and compliance exports.

## When not to use it
- Do not treat this capability as a broad catch-all; keep adjacent concerns in separate capabilities.

## Core behaviors
- User uploads file or registers external source.
- Parser and validator build staged records and error report.
- User confirms mapping and execution.
- Apply worker writes valid rows idempotently to target model.
- Invalid rows move to quarantine with actionable diagnostics.
- Export jobs snapshot scoped data and produce downloadable package.

## Typical components
- Job create endpoint for upload and source registration.
- Validation preview endpoint with sampled errors.
- Execute and cancel endpoints.
- Job status and error retrieval endpoints.
- Export generation endpoint with scoped filters and format controls.
- Upload wizard with schema mapping step.
- Validation report with row-level errors.
- Job monitor with progress and retry controls.
- Export builder with data scope and field selection.
- Parser workers per file format.
- Validation and transformation workers.
- Apply/commit worker with idempotent write semantics.
- Error quarantine and redrive worker.
- Export packaging worker.

## Key data concepts
- Job record (status, source, actor, timestamps)
- File manifest and schema version metadata
- Staging tables or object storage area
- Row-level validation and error records
- Mapping configuration and transformation rules
- DLQ/quarantine records for poison rows

## Common workflows
- Full-load batch import.
- Incremental delta import with change keys.
- Event-assisted import where row updates publish domain events.
- Streaming export vs periodic packaged export.

## Integration touchpoints
- Job create endpoint for upload and source registration.
- Validation preview endpoint with sampled errors.
- Execute and cancel endpoints.
- Job status and error retrieval endpoints.
- Export generation endpoint with scoped filters and format controls.

## Risks / failure modes
- Partial writes from worker crashes -> transactional chunk commits and resume markers.
- Duplicate rows from retries -> deterministic upsert keys.
- Schema mismatch on incoming files -> strict version negotiation and mapping templates.
- Poison rows blocking pipeline -> quarantine queue and continue-on-valid strategy.
- Long-running jobs starving queue -> priority classes and concurrency quotas.
- Export overexposure of sensitive data -> policy-scoped field allowlists.
- Scan uploads for malware and unsafe content.
- Enforce least privilege for import and export operations.

## Related archetypes
- CRM: lead and account migration, partner feed sync.
- Inventory/Catalog: supplier catalog import and stock export.
- DMS: batch ingest and compliance export.
- Case/Ticket: historical ticket migration and audit export.

## Related capabilities
- [idempotency-outbox-retries-dlq](idempotency-outbox-retries-dlq.md)
- [audit-log-provenance](audit-log-provenance.md)
- [search-index](search-index.md)
- [custom-fields-extensible-attributes](custom-fields-extensible-attributes.md)


