# Approval Workflow Failure Modes and Architectural Mitigations

## Unauthorized decision actions

Why it happens:
- Decision endpoints accept actions without strict approver eligibility validation.

Impact:
- Governance breach and invalid approval outcomes.

Mitigation:
- Authorization snapshot validation, role-bound decision controls, and immutable actor lineage.

## Stuck approvals and escalation drift

Why it happens:
- Timer and escalation policies are misconfigured or not synchronized with workflow state.

Impact:
- Delayed outcomes, SLA breaches, and queue congestion.

Mitigation:
- Deterministic timer governance, escalation parity checks, and overdue queue controls.

## Duplicate callback and export side effects

Why it happens:
- Retry behavior replays terminal decisions without idempotent safeguards.

Impact:
- Conflicting downstream state and duplicate business actions.

Mitigation:
- Outbox delivery, idempotency keys, DLQ management, and reconciliation checkpoints.

## Notification routing misalignment

Why it happens:
- Notification routes do not reflect assignment changes and escalation ownership.

Impact:
- Missed decision windows and reduced approval throughput.

Mitigation:
- Routing-aware notification policies and assignment-notification parity checks.

## Queue visibility degradation

Why it happens:
- Search projections and saved views lag behind canonical request transitions.

Impact:
- Hidden backlog and delayed operational intervention.

Mitigation:
- Projection freshness SLOs, replayable index rebuild controls, and queue governance dashboards.

## Policy and workflow drift

Why it happens:
- Rule updates are applied without synchronized workflow transition constraints.

Impact:
- Inconsistent routing outcomes and unpredictable approval behavior.

Mitigation:
- Versioned policy rollout, transition parity validation, and drift monitoring.
