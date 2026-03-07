# Support Ticket System Failure Modes

- **Queue saturation**
  - Cause: uneven routing and weak prioritization.
  - Impact: response delays and SLA breaches.
  - Mitigation: adaptive routing rules and backlog thresholds.

- **Duplicate ticket creation**
  - Cause: retry events without deduplication.
  - Impact: fragmented case history.
  - Mitigation: idempotency keys and merge workflows.

- **Notification gaps**
  - Cause: asynchronous failure in delivery paths.
  - Impact: missed customer updates.
  - Mitigation: delivery tracking and fallback channels.

- **Policy drift**
  - Cause: unversioned SLA and routing policy changes.
  - Impact: inconsistent handling.
  - Mitigation: versioned policy rollout and audit checks.
