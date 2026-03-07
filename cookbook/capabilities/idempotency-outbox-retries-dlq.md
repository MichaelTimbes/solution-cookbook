# Idempotency + Outbox + Retries + DLQ

## Problem / when to use
- Use when requests or messages may be retried, duplicated, or partially failed.
- Critical for payments, workflow side effects, imports, and cross-service integration.
- Goal: exactly-correct business outcomes under at-least-once delivery conditions.

## Ingredients
### Data model components
- Idempotency key store (key, request hash, response snapshot, expiry)
- Business state tables (domain records)
- Outbox table (event id, aggregate id, event type, payload, status, timestamps)
- Consumer dedupe table (message id, consumer name, processed_at)
- DLQ metadata table or broker-native DLQ attributes

### API contracts
- Idempotency-Key header for mutation endpoints.
- Stable error model for duplicate or hash-mismatch requests.
- Event envelope contract (event id, causation id, correlation id, schema version).
- Retryable vs non-retryable error classification.

### UI surfaces
- Operator view for retry status and DLQ depth.
- Request detail page showing idempotency key lineage.
- Replay and redrive action UI with guardrails and approval hooks.

### Jobs/workers/async components
- Outbox relay publisher.
- Consumer with idempotent processing guard.
- Retry worker with exponential backoff and jitter.
- DLQ redrive worker with policy checks.

## Reference flow (happy path + async path)
1. Client sends mutation with idempotency key.
2. API validates hash and writes business state plus outbox record in one transaction.
3. Outbox relay publishes event to broker.
4. Consumer checks dedupe store and applies side effect once.
5. Failures retry per policy; poison messages move to DLQ.
6. Operator redrives DLQ after remediation.

## Variants
- CDC-based outbox relay vs polling relay.
- API idempotency at gateway vs service layer.
- Broker-native DLQ vs application-managed quarantine store.
- Strict response replay vs accepted-and-processing asynchronous acknowledgement.

## Failure modes & mitigations
- Same key with different payload → reject via request hash comparison.
- Relay publishes duplicate event → require consumer dedupe.
- Dedupe store unavailable → fail closed for side-effecting consumers.
- Retry storm during dependency outage → circuit-break plus capped backoff.
- DLQ misrouting due to bad retry policy → validate policy with canary workloads.
- Replays violating ordering constraints → partition by aggregate id.
- Outbox growth due to stuck publisher → monitor lag and apply backlog runbooks.
- Expired idempotency keys causing late duplicates → set TTL based on business risk window.

## Security/privacy considerations
- Treat idempotency keys as sensitive metadata.
- Encrypt payloads at rest where they include PII.
- Restrict replay and redrive actions to privileged roles.
- Log redrive actor, reason, and affected message IDs.

## Observability requirements
### Trace spans
- API mutation handling with idempotency decision.
- Transaction commit with outbox write.
- Outbox publish attempt and broker ack.
- Consumer dedupe check and side-effect execution.
- DLQ enqueue and redrive execution.

### Metrics
- Idempotency hit ratio.
- Outbox publish lag.
- Duplicate-detection count by consumer.
- Retry count and terminal failure rate.
- DLQ depth and redrive success rate.

### Structured logs/audit events
- Idempotency decision logs (new, replay, hash mismatch).
- Outbox state transitions.
- Consumer dedupe outcomes.
- Retry attempt history.
- DLQ and redrive audit events.

## Testing checklist
### Unit
- Idempotency hash validation logic.
- Retry classifier and backoff policy.
- Dedupe guard behavior for duplicate inputs.

### Integration
- End-to-end transaction + outbox + consumer pipeline.
- Duplicate publish simulation.
- Broker outage and recovery scenario.

### Failure injection/chaos-lite checks
- Crash after DB commit but before publish.
- Crash after publish but before consumer ack.
- Dependency timeout during retry burst.
- Redrive under partial dependency recovery.

## Operational runbook checklist
- Confirm outage domain and pause unsafe replays.
- Check outbox lag, retry saturation, and DLQ depth.
- Classify failed messages by root cause.
- Apply fix, then controlled redrive by cohort.
- Verify no duplicate business side effects.
- Close incident with postmortem and policy updates.

## Adoption notes by archetype
- CRM: integration reliability for lead and opportunity sync.
- Case/Ticket: dedupe inbound ticket creation and escalation events.
- Payments/Billing: prevent duplicate charges and reconcile webhook retries.
- DMS and workflow systems: safe replay of document and task events.

## Licensing & source attribution notes
- Pattern definitions should be written as original synthesis.
- Cite standards, pattern sources, and implementation references.
- Avoid reproducing proprietary documentation text.
