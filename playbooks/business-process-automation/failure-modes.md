# Business Process Automation Failure Modes

- Stuck instances -> missing signals -> timeout and recovery paths.
- Duplicate side effects -> replay without idempotency -> dedupe keys.
- Dead-letter growth -> silent failures -> queue observability.
- Policy rollout mismatch -> inconsistent outcomes -> versioned decision controls.
