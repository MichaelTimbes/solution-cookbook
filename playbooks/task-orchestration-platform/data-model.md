# Task Orchestration Platform Data Model

- Core: `TaskDefinition`, `TaskRun`, `Dependency`, `ExecutionWorker`
- Metadata: `Priority`, `QueueTag`, `Constraint`
- Governance: `OverrideAction`, `AuditEvent`
- Workflow: `RunStateTransition`, `RetryAttempt`, `EscalationEvent`
- Integration: `SignalEvent`, `CallbackRecord`
