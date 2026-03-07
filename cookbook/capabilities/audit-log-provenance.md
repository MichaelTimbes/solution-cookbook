# Audit Log + Provenance

## Problem / when to use
- Use when systems require accountability, investigation support, and compliance evidence.
- Applies to admin actions, financial changes, access events, and workflow decisions.
- Goal: reconstruct who did what, when, where, and why with sufficient context.

## Ingredients
### Data model components
- Audit event schema (event id, actor, action, target, timestamp, context)
- Change representation (before and after or patch summary)
- Correlation identifiers (trace id, request id, workflow id)
- Retention and legal hold metadata
- Optional provenance graph links (entity derivation and activity)

### API contracts
- Append-only audit write contract.
- Query API with filtering and pagination.
- Export API for compliance and legal requests.
- Integrity verification endpoint (hash-chain and checksum where implemented).

### UI surfaces
- Admin audit explorer with faceted filters.
- Entity-centric timeline views.
- Access-controlled export request panel.
- Alert views for suspicious event patterns.

### Jobs/workers/async components
- Audit ingestion pipeline.
- Indexing, compaction, archival workers.
- Integrity verification job.
- Alerting and anomaly detection worker.

## Reference flow (happy path + async path)
1. Business action occurs in source system.
2. Source emits structured audit event with actor and context.
3. Audit pipeline persists immutable record and indexes searchable fields.
4. Operators query timelines or export event sets.
5. Integrity and retention jobs run continuously.

## Variants
- Centralized audit store across services.
- Domain-local audit stores with federated query.
- Separate high-fidelity forensic stream plus summarized operational stream.
- Provenance graph extension for data lineage-heavy environments.

## Failure modes & mitigations
- Missing actor and context fields → schema validation at ingestion.
- Excessive volume impacting primary workload → asynchronous decoupled pipeline.
- PII leakage in logs → redaction and tokenization policy.
- Time skew across services → NTP controls and normalized event time fields.
- Tampering risk in mutable stores → append-only model and integrity checks.
- Query blind spots from dropped index updates → lag monitoring and reindex runbook.

## Security/privacy considerations
- Strict RBAC for audit viewing and exports.
- Encryption at rest and in transit.
- Data minimization and purpose-limited retention.
- Separate credentials and network paths for audit systems.

## Observability requirements
### Trace spans
- Source action to audit write path.
- Audit ingestion and indexing spans.
- Export generation flow.

### Metrics
- Audit ingest throughput.
- Ingest and index lag.
- Event schema validation failure rate.
- Export request volume and latency.
- Integrity check pass and fail rate.

### Structured logs/audit events
- All privileged configuration changes.
- All access grant and revoke events.
- Financial and policy-impacting state changes.
- Audit export and download actions.

## Testing checklist
### Unit
- Event schema validation.
- Redaction and tokenization logic.
- Retention policy evaluator.

### Integration
- End-to-end action to searchable audit event.
- Export pipeline with access controls.
- Cross-service correlation using shared trace and request IDs.

### Failure injection/chaos-lite checks
- Ingestion backlog simulation.
- Indexer outage and replay.
- Corrupted event payload handling.

## Operational runbook checklist
- Confirm ingest and indexing pipeline health.
- Triage schema failures and quarantine invalid events.
- Execute reindex and replay for lagged windows.
- Validate integrity reports and investigate mismatches.
- Handle legal and compliance export requests with dual control.

## Adoption notes by archetype
- CRM: ownership changes, pipeline stage transitions, bulk updates.
- Case/Ticket: assignment changes, SLA events, escalation actions.
- Payments/Billing: charge and refund attempts, dunning and overrides.
- CIAM: authentication events and provisioning changes.

## Licensing & source attribution notes
- Use original synthesis for architecture and controls.
- Reference standards and OSS guidance with attribution.
- Do not copy vendor-specific policy wording directly.