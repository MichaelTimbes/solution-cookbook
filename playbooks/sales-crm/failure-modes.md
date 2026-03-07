# Sales CRM Failure Modes and Architectural Mitigations

## Duplicate relationship records

Why it happens:
- Lead and account updates arrive from multiple channels without deterministic matching controls.

Impact:
- Fragmented relationship context, duplicated outreach, and reduced forecast trust.

Mitigation:
- Deterministic identity matching, merge governance workflows, and replay-safe deduplication policies.

## Stage progression inconsistency

Why it happens:
- Opportunity stages are mutated through ad hoc paths outside governed transitions.

Impact:
- Pipeline reporting distortion and unreliable revenue forecasting.

Mitigation:
- Explicit stage transition graph, policy-evaluated progression gates, and approval-enforced exceptions.

## Approval bypass on sensitive actions

Why it happens:
- Discount, commitment, or close-date exceptions occur without required workflow controls.

Impact:
- Margin risk, governance noncompliance, and inconsistent sales practices.

Mitigation:
- Mandatory approval orchestration with immutable decision lineage and policy conformance checks.

## Notification and follow-up drift

Why it happens:
- Reminder and messaging routes diverge from current ownership and stage state.

Impact:
- Missed follow-ups, stale opportunities, and pipeline hygiene degradation.

Mitigation:
- Routing-aware notification governance, reminder reconciliation, and owner-state parity checks.

## Integration replay and synchronization errors

Why it happens:
- Retries and imports are processed without idempotent safeguards.

Impact:
- Duplicate activities, conflicting lifecycle state, and reconciliation overhead.

Mitigation:
- Outbox-based delivery, idempotency keys, DLQ handling, and checkpoint reconciliation processes.

## Search and reporting projection staleness

Why it happens:
- Query projections lag behind canonical lifecycle updates under load.

Impact:
- Inaccurate pipeline views and delayed management intervention.

Mitigation:
- Projection freshness SLOs, lag monitoring, and replayable projection rebuild paths.
