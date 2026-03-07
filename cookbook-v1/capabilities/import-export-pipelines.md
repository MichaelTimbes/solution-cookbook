# Import / Export Pipelines

## Problem / when to use
- Use when systems must ingest or emit bulk structured data with validation, mapping, and operational controls.
- Common for migrations, partner feeds, catalog syncs, and compliance exports.
- Goal: reliable high-volume transfer with clear error isolation and replay controls.

## Ingredients
### Data model components
- Job record (status, source, actor, timestamps)
- File manifest and schema version metadata
- Staging tables or object storage area
- Row-level validation and error records
- Mapping configuration and transformation rules
- DLQ/quarantine records for poison rows

### API contracts
- Job create endpoint for upload and source registration.
- Validation preview endpoint with sampled errors.
- Execute and cancel endpoints.
- Job status and error retrieval endpoints.
- Export generation endpoint with scoped filters and format controls.

### UI surfaces
- Upload wizard with schema mapping step.
- Validation report with row-level errors.
- Job monitor with progress and retry controls.
- Export builder with data scope and field selection.

### Jobs/workers/async components
- Parser workers per file format.
- Validation and transformation workers.
- Apply/commit worker with idempotent write semantics.
- Error quarantine and redrive worker.
- Export packaging worker.

## Reference flow (happy path + async path)
1. User uploads file or registers external source.
2. Parser and validator build staged records and error report.
3. User confirms mapping and execution.
4. Apply worker writes valid rows idempotently to target model.
5. Invalid rows move to quarantine with actionable diagnostics.
6. Export jobs snapshot scoped data and produce downloadable package.

## Variants
- Full-load batch import.
- Incremental delta import with change keys.
- Event-assisted import where row updates publish domain events.
- Streaming export vs periodic packaged export.

## Failure modes & mitigations
- Partial writes from worker crashes → transactional chunk commits and resume markers.
- Duplicate rows from retries → deterministic upsert keys.
- Schema mismatch on incoming files → strict version negotiation and mapping templates.
- Poison rows blocking pipeline → quarantine queue and continue-on-valid strategy.
- Long-running jobs starving queue → priority classes and concurrency quotas.
- Export overexposure of sensitive data → policy-scoped field allowlists.

## Security/privacy considerations
- Scan uploads for malware and unsafe content.
- Enforce least privilege for import and export operations.
- Encrypt staged files and generated export packages.
- Time-limit download URLs and log all access.

## Observability requirements
### Trace spans
- Job submission to parser start.
- Validation and transformation execution path.
- Commit phase with chunk-level checkpoints.
- Quarantine enqueue and redrive path.

### Metrics
- Job success rate by source type.
- Rows processed per minute.
- Validation error rate by rule.
- Quarantine depth and redrive success rate.
- Export generation latency and size distribution.

### Structured logs/audit events
- Job lifecycle events.
- Mapping configuration changes.
- Validation failure summaries.
- Redrive and replay actions.
- Export requests and download access events.

## Testing checklist
### Unit
- Schema parser and mapper logic.
- Validation rule execution.
- Idempotent upsert key resolution.

### Integration
- End-to-end import with staged apply and quarantine.
- Export pipeline with scoped field controls.
- Resume and retry behavior after worker interruption.

### Failure injection/chaos-lite checks
- Mid-job worker termination.
- Corrupted input file segments.
- Target system latency and transient outages.

## Operational runbook checklist
- Identify stuck jobs and queue pressure.
- Validate parser and validator health.
- Quarantine problematic cohorts and continue safe processing.
- Redrive corrected records in bounded batches.
- Publish post-run summary with success, failure, and remediation counts.

## Adoption notes by archetype
- CRM: lead and account migration, partner feed sync.
- Inventory/Catalog: supplier catalog import and stock export.
- DMS: batch ingest and compliance export.
- Case/Ticket: historical ticket migration and audit export.

## Licensing & source attribution notes
- Keep pattern descriptions as original synthesis.
- Attribute standards and OSS references where used.
- Avoid reproducing vendor import and export docs directly.