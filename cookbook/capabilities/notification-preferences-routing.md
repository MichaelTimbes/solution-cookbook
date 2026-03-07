# Notification Preferences + Routing

## Problem / when to use
- Use when systems send high-volume transactional and lifecycle notifications across channels.
- Needed to honor user consent and reduce noise while preserving critical delivery.
- Goal: policy-correct delivery with traceable opt-in and opt-out behavior.

## Ingredients
### Data model components
- Preference profile (user, channel, category, frequency, locale)
- Suppression and unsubscribe records
- Channel endpoint registry (email, phone, push token, webhook)
- Routing policy (priority, fallback, quiet hours)
- Delivery event log and status timeline

### API contracts
- Preference read and update endpoints.
- Category and channel subscription endpoints.
- One-click unsubscribe endpoint for supported channels.
- Notification send API with idempotency and policy-evaluation result.

### UI surfaces
- User notification settings page by category and channel.
- Admin policy console for defaults and compliance controls.
- Delivery activity timeline and troubleshooting panel.
- Preference center deep links from outgoing messages.

### Jobs/workers/async components
- Policy evaluation and routing worker.
- Delivery adapter workers per channel.
- Retry and bounce-handling worker.
- Digest/coalescing worker for low-priority events.

## Reference flow (happy path + async path)
1. Business event produces notification intent.
2. Policy engine evaluates user preferences, consent, and quiet hours.
3. Router selects channel sequence and dispatches to adapters.
4. Delivery events are recorded with status updates.
5. Failures retry or fallback to alternate channel per policy.
6. Opt-out and unsubscribe actions immediately update suppression state.

## Variants
- Category-first preference model (marketing, product, billing, security).
- Channel-first model with per-channel granular controls.
- Immediate-send mode for urgent classes with consent guardrails.
- Digest mode for non-urgent activity streams.

## Failure modes & mitigations
- Duplicate notifications from event replay → idempotent send keys.
- Unsubscribe not applied quickly enough → low-latency suppression cache.
- Accidental global opt-out from malformed links → scoped unsubscribe tokens.
- Delivery retries causing channel throttling → adaptive backoff and provider quotas.
- Quiet-hour violations due to timezone errors → canonical timezone handling.
- Preference drift across systems → source-of-truth ownership and sync reconciliation.

## Security/privacy considerations
- Verify ownership before allowing endpoint updates.
- Protect unsubscribe and preference tokens against forgery.
- Minimize personal data in notification payloads.
- Restrict policy overrides and audit all admin changes.

## Observability requirements
### Trace spans
- Event-to-policy-evaluation path.
- Routing decision and channel adapter dispatch.
- Provider delivery callback processing.
- Preference update and suppression write path.

### Metrics
- Delivery success and failure rate by channel.
- Opt-out and unsubscribe rate by category.
- Retry volume and fallback usage.
- Notification latency from event to send.
- Suppression-check hit rate.

### Structured logs/audit events
- Preference and consent changes.
- Policy evaluation outcomes for each send.
- Delivery adapter error classifications.
- Admin override and bulk policy changes.

## Testing checklist
### Unit
- Policy evaluation rules and precedence.
- Channel fallback selection.
- Token validation for preference and unsubscribe links.

### Integration
- End-to-end send with delivery callbacks.
- One-click unsubscribe compliance path.
- Multi-channel fallback and throttling behavior.

### Failure injection/chaos-lite checks
- Provider outage and recovery.
- Delayed callback and duplicate callback handling.
- Consent store latency spikes.

## Operational runbook checklist
- Identify affected channels and provider health.
- Apply temporary rate limits and fallback strategy.
- Verify suppression and unsubscribe integrity.
- Replay failed sends by safe cohorts.
- Confirm recovery via delivery and complaint metrics.

## Adoption notes by archetype
- Case/Ticket: SLA breach and assignment notifications.
- Payments/Billing: invoice and dunning notifications.
- Workflow/BPM: task assignment, reminder, and escalation notices.
- CRM: activity reminders and customer lifecycle events.

## Licensing & source attribution notes
- Keep implementation guidance as synthesized patterns.
- Reference standards and provider behavior docs with attribution.
- Avoid copying provider-specific legal/compliance prose verbatim.
