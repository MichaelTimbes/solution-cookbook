# Audit Log and Provenance

## What this capability is
- reconstruct who did what, when, where, and why with sufficient context.

## When to use it
- Use when systems require accountability, investigation support, and compliance evidence.
- Applies to admin actions, financial changes, access events, and workflow decisions.

## When not to use it
- Do not treat this capability as a broad catch-all; keep adjacent concerns in separate capabilities.

## Core behaviors
- Business action occurs in source system.
- Source emits structured audit event with actor and context.
- Audit pipeline persists immutable record and indexes searchable fields.
- Operators query timelines or export event sets.
- Integrity and retention jobs run continuously.

## Typical components
- Append-only audit write contract.
- Query API with filtering and pagination.
- Export API for compliance and legal requests.
- Integrity verification endpoint (hash-chain and checksum where implemented).
- Admin audit explorer with faceted filters.
- Entity-centric timeline views.
- Access-controlled export request panel.
- Alert views for suspicious event patterns.
- Audit ingestion pipeline.
- Indexing, compaction, archival workers.
- Integrity verification job.
- Alerting and anomaly detection worker.

## Key data concepts
- Audit event schema (event id, actor, action, target, timestamp, context)
- Change representation (before and after or patch summary)
- Correlation identifiers (trace id, request id, workflow id)
- Retention and legal hold metadata
- Optional provenance graph links (entity derivation and activity)

## Common workflows
- Centralized audit store across services.
- Domain-local audit stores with federated query.
- Separate high-fidelity forensic stream plus summarized operational stream.
- Provenance graph extension for data lineage-heavy environments.

## Integration touchpoints
- Append-only audit write contract.
- Query API with filtering and pagination.
- Export API for compliance and legal requests.
- Integrity verification endpoint (hash-chain and checksum where implemented).

## Risks / failure modes
- Missing actor and context fields -> schema validation at ingestion.
- Excessive volume impacting primary workload -> asynchronous decoupled pipeline.
- PII leakage in logs -> redaction and tokenization policy.
- Time skew across services -> NTP controls and normalized event time fields.
- Tampering risk in mutable stores -> append-only model and integrity checks.
- Query blind spots from dropped index updates -> lag monitoring and reindex runbook.
- Strict RBAC for audit viewing and exports.
- Encryption at rest and in transit.

## Related archetypes
- CRM: ownership changes, pipeline stage transitions, bulk updates.
- Case/Ticket: assignment changes, SLA events, escalation actions.
- Payments/Billing: charge and refund attempts, dunning and overrides.
- CIAM: authentication events and provisioning changes.

## Related capabilities
- [idempotency-outbox-retries-dlq](idempotency-outbox-retries-dlq.md)
- [import-export-pipelines](import-export-pipelines.md)
- [approval-workflows-human-in-the-loop](approval-workflows-human-in-the-loop.md)
- [notification-messaging-system](notification-messaging-system.md)


