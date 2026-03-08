# Notification Preferences and Routing

primary-role: policy-control
secondary-role: interaction

## What this capability is
- policy-correct delivery with traceable opt-in and opt-out behavior.

## When to use it
- Use when systems send high-volume transactional and lifecycle notifications across channels.
- Needed to honor user consent and reduce noise while preserving critical delivery.

## When not to use it
- Do not treat this capability as a broad catch-all; keep adjacent concerns in separate capabilities.

## Core behaviors
- Business event produces notification intent.
- Policy engine evaluates user preferences, consent, and quiet hours.
- Router selects channel sequence and dispatches to adapters.
- Delivery events are recorded with status updates.
- Failures retry or fallback to alternate channel per policy.
- Opt-out and unsubscribe actions immediately update suppression state.

## Typical components
- Preference read and update endpoints.
- Category and channel subscription endpoints.
- One-click unsubscribe endpoint for supported channels.
- Notification send API with idempotency and policy-evaluation result.
- User notification settings page by category and channel.
- Admin policy console for defaults and compliance controls.
- Delivery activity timeline and troubleshooting panel.
- Preference center deep links from outgoing messages.
- Policy evaluation and routing worker.
- Delivery adapter workers per channel.
- Retry and bounce-handling worker.
- Digest/coalescing worker for low-priority events.

## Key data concepts
- Preference profile (user, channel, category, frequency, locale)
- Suppression and unsubscribe records
- Channel endpoint registry (email, phone, push token, webhook)
- Routing policy (priority, fallback, quiet hours)
- Delivery event log and status timeline

## Common workflows
- Category-first preference model (marketing, product, billing, security).
- Channel-first model with per-channel granular controls.
- Immediate-send mode for urgent classes with consent guardrails.
- Digest mode for non-urgent activity streams.

## Integration touchpoints
- Preference read and update endpoints.
- Category and channel subscription endpoints.
- One-click unsubscribe endpoint for supported channels.
- Notification send API with idempotency and policy-evaluation result.

## Risks / failure modes
- Duplicate notifications from event replay -> idempotent send keys.
- Unsubscribe not applied quickly enough -> low-latency suppression cache.
- Accidental global opt-out from malformed links -> scoped unsubscribe tokens.
- Delivery retries causing channel throttling -> adaptive backoff and provider quotas.
- Quiet-hour violations due to timezone errors -> canonical timezone handling.
- Preference drift across systems -> source-of-truth ownership and sync reconciliation.
- Verify ownership before allowing endpoint updates.
- Protect unsubscribe and preference tokens against forgery.

## Related archetypes
- Case/Ticket: SLA breach and assignment notifications.
- Payments/Billing: invoice and dunning notifications.
- Workflow/BPM: task assignment, reminder, and escalation notices.
- CRM: activity reminders and customer lifecycle events.

## Related capabilities
- [notification-messaging-system](notification-messaging-system.md)
- [human-communication](human-communication.md)
- [approval-workflows-human-in-the-loop](approval-workflows-human-in-the-loop.md)
- [rules-engine-decisioning](rules-engine-decisioning.md)


