# Operational Visibility (Observability)

## Description of the pattern
Operational Visibility provides insight into runtime behavior through traces, metrics, logs, and actionable health indicators.

## Why it appears across enterprise systems
As systems scale and decouple, correctness and reliability cannot be inferred from code alone. Teams need production feedback loops.

## Typical implementation capabilities
- [Audit Log + Provenance](../capabilities/audit-log-provenance.md)
- [Idempotency + Outbox + Retries + DLQ](../capabilities/idempotency-outbox-retries-dlq.md)
- [Notification / Messaging System](../capabilities/notification-messaging-system.md)

## Example archetypes that rely on it
- [Analytics Platform](../archetypes/analytics-platform.md)
- [Workflow / BPM System](../archetypes/workflow-bpm-system.md)
- [Identity / Access (CIAM)](../archetypes/identity-access-ciam.md)

## Common failure modes when ignored
- Invisible degradation before user impact is obvious
- Slow root-cause analysis during incidents
- Repeated outages due to missing feedback instrumentation
