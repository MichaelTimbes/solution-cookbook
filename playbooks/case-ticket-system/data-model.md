# Case / Ticket System Data Model (Architecture View)

## Core Aggregate Groups

## Core Domain Objects

- `Ticket`: canonical work item under lifecycle and SLA control.
- `Case`: optional higher-order grouping for related ticket threads.
- `Requester`: originator context for the ticket.
- `Agent`: operator assigned to resolution activity.
- `Queue`: operational routing boundary for ticket ownership.
- `Team`: collaborative ownership group for queues and assignments.
- `Comment`: user or agent-authored interaction record.
- `Communication`: outbound or inbound delivery record linked to ticket context.

Purpose:
- Encapsulates intake-through-closure entities and operational ownership.

## Metadata and Classification

- `Category`: hierarchical issue taxonomy.
- `Priority`: policy-aligned urgency and impact level.
- `CustomFieldDefinition`: extensible field schema for ticket classes.
- `CustomFieldValue`: typed values associated with ticket entities.
- `ClassificationOutcome`: structured triage/evaluation result.

Purpose:
- Supports consistent triage, searchability, and configurable intake behavior.

## Access and Governance

- `RoleAssignment`: role and queue-based access scope.
- `OwnershipAssignment`: current and historical assignment lineage.
- `SlaPolicyVersion`: effective SLA rules and calendars.
- `AuditEvent`: immutable actor-action-object history records.

Purpose:
- Enforces trust boundaries, policy governance, and forensics.

## Process and Workflow

- `StatusTransition`: explicit lifecycle progression records.
- `WorkflowInstanceReference`: orchestration state for escalations and approvals.
- `ApprovalDecision`: human approval outcomes with rationale.
- `EscalationEvent`: policy-triggered escalation actions.
- `NotificationEvent`: communication intent and delivery outcome reference.

Purpose:
- Tracks lifecycle control, exception handling, and communication flow.

## Interchange and Integrations

- `ImportJob`: ticket ingestion batch and reconciliation status.
- `ExportJob`: scoped extraction and delivery status.
- `IntegrationSyncCheckpoint`: synchronization cursor and lag tracking.
- `IdempotencyKeyRecord`: deduplication and retry-safe processing record.

Purpose:
- Governs safe data interchange and resilience at integration boundaries.

## Key Relationships

- One `Requester` has many `Ticket` records.
- One `Ticket` belongs to one active `Queue` and may reference one active `Agent`.
- One `Ticket` has many `Comment`, `Communication`, and `StatusTransition` records.
- One `Ticket` references an effective `SlaPolicyVersion`.
- Workflow, escalation, and notification entities reference canonical ticket identifiers.
- Audit events correlate state, policy, assignment, and communication changes.

## Invariants

- Ticket status must follow an allowed transition graph.
- SLA timer state must align with ticket lifecycle state.
- Assignment changes require actor attribution and timestamped lineage.
- External communication outcomes must retain delivery state history.
- Reopen actions must preserve prior closure and resolution context.
- Audit records are immutable and append-only.
- Integration upserts are idempotent within defined deduplication windows.

## Authoritative vs Projection Guidance

- Authoritative entities: `Ticket`, `Case`, `Requester`, `Queue`, `Agent`, `StatusTransition`, `SlaPolicyVersion`.
- Projection entities: queue dashboards, SLA summary views, search indexes, reporting snapshots.
- Keep projection rebuild paths explicit to preserve recoverability and consistency behavior.