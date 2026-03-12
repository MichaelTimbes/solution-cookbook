# Support Ticket System Data Model (Architecture View)

## Core Aggregate Groups

## Core Domain Objects

- `Ticket`: canonical support request under lifecycle and SLA policy control.
- `Requester`: originator profile and communication context.
- `Agent`: assigned resolver identity.
- `Queue`: operational routing boundary for ticket ownership.
- `Comment`: requester/agent interaction history.
- `ResolutionRecord`: normalized closure rationale and outcome.

Purpose:
- Encapsulates support lifecycle entities from intake through closure.

## Metadata and Classification

- `Category`: issue taxonomy classification.
- `Priority`: urgency and impact policy label.
- `CustomFieldDefinition`: configurable ticket schema controls.
- `CustomFieldValue`: typed values applied by ticket class.
- `ClassificationOutcome`: normalized triage decision outputs.

Purpose:
- Supports policy-consistent triage, segmentation, and operational search.

## Access and Governance

- `RoleAssignment`: role and queue-based visibility context.
- `OwnershipAssignment`: current and historical assignment lineage.
- `SlaPolicyVersion`: effective service-level policy definition.
- `AuditEvent`: immutable actor-action-object evidence.

Purpose:
- Governs trust boundaries, SLA accountability, and compliance traceability.

## Process and Workflow

- `StatusTransition`: explicit lifecycle progression records.
- `EscalationEvent`: policy-triggered escalation outcomes.
- `ApprovalDecision`: human approval outcomes for exception paths.
- `NotificationEvent`: communication intent and delivery reference.

Purpose:
- Controls deterministic lifecycle progression and exception handling.

## Interchange and Integrations

- `InboundChannelEvent`: normalized portal/email/API intake events.
- `ExportJob`: support dataset export state and reconciliation.
- `IntegrationSyncCheckpoint`: external context synchronization cursor.
- `IdempotencyKeyRecord`: replay protection and deduplication state.

Purpose:
- Stabilizes multi-channel intake and external synchronization behavior.

## Key Relationships

- One `Requester` has many `Ticket` records.
- One `Ticket` belongs to one active `Queue` and optional active `Agent`.
- One `Ticket` has many `Comment`, `StatusTransition`, and `NotificationEvent` records.
- One `Ticket` references one effective `SlaPolicyVersion`.
- `AuditEvent` correlates intake, assignment, escalation, and resolution actions.

## State Authority

- Authoritative domain state typically lives in `Ticket`, `Requester`, `Agent`, `Queue`, `OwnershipAssignment`, `ResolutionRecord`, `StatusTransition`, and `SlaPolicyVersion`.
- Supporting authoritative records commonly include `ApprovalDecision`, `EscalationEvent`, `AuditEvent`, and integration checkpoint records within their own concerns.
- Derived or rebuildable forms often include queue dashboards, aging views, notification delivery views, search documents, and reporting summaries.
- Artifacts may store screenshots, logs, or evidence files where needed, but those records typically do not own support-ticket lifecycle state.
- Search indexes, dashboards, and notifications are projections and should remain conceptually rebuildable from canonical support records.

## Invariants

- Ticket status transitions must follow an allowed transition graph.
- SLA timer state must align with current ticket lifecycle state.
- Assignment changes require actor attribution and timestamped lineage.
- Audit and provenance records are immutable and append-only.
- Intake deduplication is enforced for replayed channel events.
