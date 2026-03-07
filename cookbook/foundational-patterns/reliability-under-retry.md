# Reliability Under Retry (Idempotency / Outbox)

## Description of the pattern
Reliability Under Retry ensures correct outcomes when operations are retried, duplicated, reordered, or partially failed.

## Why it appears across enterprise systems
Distributed systems naturally produce transient failure and at-least-once delivery. Reliability requires explicit correctness patterns, not optimistic assumptions.

## Typical implementation capabilities
- [Idempotency + Outbox + Retries + DLQ](../capabilities/idempotency-outbox-retries-dlq.md)
- [Notification / Messaging System](../capabilities/notification-messaging-system.md)
- [Audit Log + Provenance](../capabilities/audit-log-provenance.md)

## Example archetypes that rely on it
- [Payments / Billing](../archetypes/payments-billing.md)
- [Workflow / BPM System](../archetypes/workflow-bpm-system.md)
- [Inventory / Catalog](../archetypes/inventory-catalog.md)

## Common failure modes when ignored
- Duplicate side effects (charges, updates, notifications)
- Lost updates after crash boundaries
- Dead-letter growth without safe replay strategy
