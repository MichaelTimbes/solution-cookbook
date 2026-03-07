# Incident Management System Data Model

## Core Aggregate Groups

### Core Domain Objects
- `Incident`
- `IncidentTask`
- `Responder`
- `ResponderTeam`

### Metadata and Classification
- `SeverityLevel`
- `ServiceImpact`
- `AffectedComponent`

### Access and Governance
- `RoleAssignment`
- `IncidentCommandAssignment`
- `AuditEvent`

### Process and Workflow
- `StatusTransition`
- `EscalationTimer`
- `RunbookStepExecution`

### Interchange and Integrations
- `AlertEvent`
- `PagerNotification`
- `PostmortemExport`

## Key Relationships

- One incident has many tasks and timeline events.
- One incident can map to many correlated alert events.
- One responder team can own many incidents.

## Invariants

- Severity changes require actor attribution.
- Escalation timers align with severity policy.
- Incident timeline events are immutable.
