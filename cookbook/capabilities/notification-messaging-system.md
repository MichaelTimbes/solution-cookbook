# Notification / Messaging System

## What this capability is
- durable, policy-aware, traceable message delivery with failure isolation.

## When to use it
- Use when systems need reliable message production and delivery across channels (email, SMS, push, in-app, webhooks, event bus).
- Apply this capability as a shared delivery backbone used by archetype-specific notification policies.

## When not to use it
- Do not treat this capability as a broad catch-all; keep adjacent concerns in separate capabilities.

## Core behaviors
- Producer emits a message intent with correlation metadata.
- Messaging API validates payload and stores envelope with idempotency key.
- Dispatcher selects channel route and enqueues delivery tasks.
- Channel adapter sends message and records attempt outcome.
- Failed attempts retry with bounded backoff; terminal failures move to dead-letter queue.
- Provider callbacks reconcile final delivery status and update observability/audit records.

## Typical components
- Message publish API (sync accept + async delivery lifecycle)
- Bulk publish API for batched sends
- Delivery status query API
- Dead-letter replay API
- Webhook/callback ingestion API for provider delivery receipts
- Operations console for queue depth, failures, and retries
- Message trace view (event to delivery timeline)
- Channel health dashboard
- Replay and redrive controls with approval gates
- Dispatcher worker (route by channel policy)
- Channel adapter workers (email/SMS/push/webhook)
- Retry and backoff worker
- Dead-letter queue worker and redrive processor
- Callback reconciliation worker for external provider receipts

## Key data concepts
- Message envelope (id, type, tenant, priority, correlation ids)
- Recipient endpoint model (channel address/token, verification status)
- Delivery attempt history (status timeline, provider response metadata)
- Deduplication store (idempotency keys, replay window)
- Channel policy profile (throttling, fallback order, blackout windows)

## Common workflows
- Event-bus-first architecture where downstream channel services subscribe.
- Centralized orchestration service with pluggable channel adapters.
- Single-tenant isolated queues for regulated workloads.
- Multi-tenant shared queues with per-tenant throttling partitions.

## Integration touchpoints
- Message publish API (sync accept + async delivery lifecycle)
- Bulk publish API for batched sends
- Delivery status query API
- Dead-letter replay API
- Webhook/callback ingestion API for provider delivery receipts

## Risks / failure modes
- Duplicate sends from retry/replay overlap -> enforce idempotency keys at dispatch and adapter layers.
- Provider outage causing queue buildup -> circuit breakers + channel fallback + queue backpressure controls.
- Callback loss causing stale status -> periodic reconciliation jobs with provider APIs.
- Dead-letter growth without operator visibility -> alerting thresholds and replay runbooks.
- Throttling misconfiguration causing drops -> adaptive rate control and policy validation checks.
- Cross-tenant leakage via queue metadata -> strict tenant partitioning and access controls.
- Encrypt message payloads at rest and in transit.
- Minimize PII in message content and logs.

## Related archetypes
- CRM: lifecycle reminders, assignment notifications, campaign triggers.
- Case/Ticket: SLA warnings, assignment/escalation messages.
- Workflow/BPM: task and timeout notifications.
- CMS/DMS: publish, approval, and retention event notifications.
- Billing: invoice, payment retry, dunning communications.
- Scheduling: booking confirmations, reminders, and change alerts.
- Inventory: low-stock and allocation exception alerts.
- CIAM: verification, MFA, security alerts.
- Analytics: report-ready and threshold alerts.

## Related capabilities
- [notification-preferences-routing](notification-preferences-routing.md)
- [idempotency-outbox-retries-dlq](idempotency-outbox-retries-dlq.md)
- [human-communication](human-communication.md)
- [audit-log-provenance](audit-log-provenance.md)


