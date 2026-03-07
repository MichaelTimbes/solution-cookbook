# Incident Management System Failure Modes

- **Alert flood amplification**
  - Cause: noisy alert sources and weak correlation.
  - Impact: responder overload.
  - Mitigation: event deduplication and severity gating.

- **Escalation delays**
  - Cause: misconfigured timer policy.
  - Impact: longer mean time to mitigation.
  - Mitigation: timer policy validation and drift monitoring.

- **Timeline gaps**
  - Cause: missing event ingestion from tools.
  - Impact: weak post-incident analysis.
  - Mitigation: mandatory timeline events and reconciliation.

- **Duplicate side effects**
  - Cause: replay without idempotency.
  - Impact: repeated notifications and tasks.
  - Mitigation: idempotency keys and replay-safe handlers.
