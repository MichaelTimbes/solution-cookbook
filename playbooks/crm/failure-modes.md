# CRM Failure Modes and Architectural Mitigations

## Duplicate customer records

Why it happens:
- Weak matching rules at ingestion and inconsistent merge governance.

Impact:
- Fragmented customer history, incorrect ownership, and unreliable reporting.

Mitigation:
- Canonical identity strategy, deterministic matching rules, and lineage-preserving merge workflows.

## Missing auditability

Why it happens:
- Background or bulk updates bypass comprehensive event capture.

Impact:
- Low forensic confidence, governance gaps, and unresolved ownership disputes.

Mitigation:
- Immutable audit events for all create/update/delete and ownership changes, including batch operations.

## Poor search strategy

Why it happens:
- Search projections and schema evolution are unmanaged.

Impact:
- Slow retrieval, poor triage efficiency, and hidden pipeline risk.

Mitigation:
- Search ownership, index lifecycle governance, and saved-view quality controls.

## Uncontrolled stage progression

Why it happens:
- Opportunity transitions are updated outside formal workflow and policy checks.

Impact:
- Forecasting inaccuracies, policy violations, and inconsistent process behavior.

Mitigation:
- Explicit stage-transition graph, approval gates for sensitive changes, and policy-based transition validation.

## Inconsistent access control

Why it happens:
- Role and ownership rules diverge between query, update, and export paths.

Impact:
- Sensitive data exposure or blocked legitimate access.

Mitigation:
- Centralized authorization evaluation and continuous parity checks across all access surfaces.

## Notification storms

Why it happens:
- Multiple automation rules generate overlapping events without deduplication.

Impact:
- Alert fatigue, missed critical actions, and operational noise.

Mitigation:
- Notification policy governance, deduplication controls, route-level throttling, and escalation windows.

## Integration drift and sync lag

Why it happens:
- Incomplete idempotency and weak reconciliation across external boundaries.

Impact:
- Stale account/opportunity status and trust erosion between systems.

Mitigation:
- Idempotent sync contracts, retry-safe eventing, lag monitoring, and scheduled reconciliation reports.
