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

## State Authority

- Authoritative domain state typically lives in `Incident`, `IncidentTask`, `Responder`, `ResponderTeam`, `StatusTransition`, `EscalationTimer`, and `RunbookStepExecution`.
- Supporting authoritative records commonly include `AuditEvent`, `IncidentCommandAssignment`, and correlated `AlertEvent` records within their own concerns.
- Derived or rebuildable forms often include active-incident boards, search documents, responder dashboards, notification delivery views, and post-incident reporting summaries.
- Artifacts may capture evidence, logs, or postmortem attachments, but those records typically do not own incident lifecycle state.
- Search indexes, dashboards, and notifications are projections and should remain conceptually rebuildable from canonical incident records.

## Invariants

- Severity changes require actor attribution.
- Escalation timers align with severity policy.
- Incident timeline events are immutable.