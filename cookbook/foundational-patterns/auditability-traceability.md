# Auditability / Traceability

## Description of the pattern
Auditability / Traceability ensures important actions and state transitions can be reconstructed with actor, time, and context.

## Why it appears across enterprise systems
Regulated workflows, financial operations, and incident response all depend on reliable history. Teams need evidence, not inference.

## Typical implementation capabilities
- [Audit Log + Provenance](../capabilities/audit-log-provenance.md)
- [Idempotency + Outbox + Retries + DLQ](../capabilities/idempotency-outbox-retries-dlq.md)
- [Import / Export Pipelines](../capabilities/import-export-pipelines.md)

## Example archetypes that rely on it
- [Document Management System](../archetypes/document-management-system.md)
- [Payments / Billing](../archetypes/payments-billing.md)
- [Identity / Access (CIAM)](../archetypes/identity-access-ciam.md)

## Common failure modes when ignored
- Inability to explain how state changed
- Compliance exceptions due to missing evidence
- Slow incident resolution from fragmented logs
