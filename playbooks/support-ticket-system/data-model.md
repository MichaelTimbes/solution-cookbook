# Support Ticket System Data Model

## Core Aggregate Groups

### Core Domain Objects
- `Ticket`
- `Requester`
- `Agent`
- `Queue`
- `Comment`

### Metadata and Classification
- `Category`
- `Priority`
- `Tag`
- `CustomFieldValue`

### Access and Governance
- `RoleAssignment`
- `OwnershipChange`
- `AuditEvent`

### Process and Workflow
- `StatusTransition`
- `SlaTimer`
- `EscalationEvent`

### Interchange and Integrations
- `InboundMessage`
- `OutboundNotification`
- `IntegrationSyncRecord`

## Key Relationships

- One requester has many tickets.
- One ticket belongs to one active queue and optional active agent.
- One ticket has many comments and status transitions.

## Invariants

- Status transitions must follow configured graph.
- Assignment changes require actor attribution.
- Audit records are immutable and append-only.
