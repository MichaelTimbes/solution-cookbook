# Idempotency, Outbox, Retries, and DLQ

## What this capability is
- exactly-correct business outcomes under at-least-once delivery conditions.

## When to use it
- Use when requests or messages may be retried, duplicated, or partially failed.
- Critical for payments, workflow side effects, imports, and cross-service integration.

## When not to use it
- Do not treat this capability as a broad catch-all; keep adjacent concerns in separate capabilities.

## Core behaviors
- Client sends mutation with idempotency key.
- API validates hash and writes business state plus outbox record in one transaction.
- Outbox relay publishes event to broker.
- Consumer checks dedupe store and applies side effect once.
- Failures retry per policy; poison messages move to DLQ.
- Operator redrives DLQ after remediation.

## Typical components
- Idempotency-Key header for mutation endpoints.
- Stable error model for duplicate or hash-mismatch requests.
- Event envelope contract (event id, causation id, correlation id, schema version).
- Retryable vs non-retryable error classification.
- Operator view for retry status and DLQ depth.
- Request detail page showing idempotency key lineage.
- Replay and redrive action UI with guardrails and approval hooks.
- Outbox relay publisher.
- Consumer with idempotent processing guard.
- Retry worker with exponential backoff and jitter.
- DLQ redrive worker with policy checks.

## Key data concepts
- Idempotency key store (key, request hash, response snapshot, expiry)
- Business state tables (domain records)
- Outbox table (event id, aggregate id, event type, payload, status, timestamps)
- Consumer dedupe table (message id, consumer name, processed_at)
- DLQ metadata table or broker-native DLQ attributes

## Common workflows
- CDC-based outbox relay vs polling relay.
- API idempotency at gateway vs service layer.
- Broker-native DLQ vs application-managed quarantine store.
- Strict response replay vs accepted-and-processing asynchronous acknowledgement.

## Integration touchpoints
- Idempotency-Key header for mutation endpoints.
- Stable error model for duplicate or hash-mismatch requests.
- Event envelope contract (event id, causation id, correlation id, schema version).
- Retryable vs non-retryable error classification.

## Risks / failure modes
- Same key with different payload -> reject via request hash comparison.
- Relay publishes duplicate event -> require consumer dedupe.
- Dedupe store unavailable -> fail closed for side-effecting consumers.
- Retry storm during dependency outage -> circuit-break plus capped backoff.
- DLQ misrouting due to bad retry policy -> validate policy with canary workloads.
- Replays violating ordering constraints -> partition by aggregate id.
- Outbox growth due to stuck publisher -> monitor lag and apply backlog runbooks.
- Expired idempotency keys causing late duplicates -> set TTL based on business risk window.
- Treat idempotency keys as sensitive metadata.
- Encrypt payloads at rest where they include PII.

## Related archetypes
- CRM: integration reliability for lead and opportunity sync.
- Case/Ticket: dedupe inbound ticket creation and escalation events.
- Payments/Billing: prevent duplicate charges and reconcile webhook retries.
- DMS and workflow systems: safe replay of document and task events.

## Related capabilities
- [notification-messaging-system](notification-messaging-system.md)
- [import-export-pipelines](import-export-pipelines.md)
- [audit-log-provenance](audit-log-provenance.md)
- [approval-workflows-human-in-the-loop](approval-workflows-human-in-the-loop.md)


