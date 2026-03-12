# Business Process Automation Data Model

## Core Aggregate Groups

### Core Domain Objects
- `ProcessDefinition`
- `ProcessVersion`
- `Instance`
- `Task`

### Metadata and Classification
- `DecisionInput`
- `DecisionOutcome`

### Access and Governance
- `OverrideAction`
- `AuditEvent`

### Process and Workflow
- `TransitionRecord`
- `TimerEvent`
- `CompensationRecord`

### Interchange and Integrations
- `IntegrationTask`
- `RetryAttempt`
- `DeadLetterRecord`

## State Authority

- Authoritative domain state typically lives in `ProcessDefinition`, `ProcessVersion`, `Instance`, `Task`, `TransitionRecord`, `TimerEvent`, and `CompensationRecord`.
- Supporting authoritative records commonly include `DecisionInput`, `DecisionOutcome`, `OverrideAction`, `AuditEvent`, `RetryAttempt`, and `DeadLetterRecord` within their own concerns.
- Derived or rebuildable forms often include backlog dashboards, search documents, notification delivery views, process-health summaries, and reporting aggregates.
- Artifacts or generated outputs may be authoritative within their own artifact boundary, but they typically do not own automation lifecycle state.
- Search indexes, dashboards, and notifications are projections and should remain conceptually rebuildable from canonical automation records.