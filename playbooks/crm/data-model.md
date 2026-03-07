# CRM Data Model (Architecture View)

## Core Aggregate Groups

## Core Domain Objects

- `Account`: authoritative representation of a customer organization or business entity.
- `Contact`: person-level relationship anchored to an account.
- `Lead`: pre-conversion prospect record.
- `Opportunity`: qualified commercial pursuit with stage progression.
- `Activity`: interaction events such as tasks, calls, meetings, and notes.
- `Case`: service interaction linked to account and contact context.
- `Quote`: commercial artifact linked to one opportunity.

Purpose:
- Encapsulates customer lifecycle entities and commercial progression.

## Metadata and Classification

- `CustomFieldDefinition`: extensible schema elements governed by policy.
- `CustomFieldValue`: typed values attached to core entities.
- `QualificationResult`: structured evaluation outcomes used in conversion and routing.
- `SegmentTag`: classification tags for operational and analytical segmentation.

Purpose:
- Enables extensibility, standardized qualification, and searchable segmentation.

## Access and Governance

- `User`: actor identity for ownership and actions.
- `Team`: shared ownership and collaboration boundary.
- `RoleAssignment`: role-based and ownership overlays for visibility and action permissions.
- `AccessPolicySnapshot`: policy context used during authorization decisions.
- `AuditEvent`: immutable record of actor-action-object transitions.

Purpose:
- Enforces trust boundaries, accountability, and policy-consistent access.

## Process and Workflow

- `WorkflowInstanceReference`: orchestration state for governed processes.
- `ApprovalDecision`: human approval outcomes with rationale.
- `StageTransition`: explicit opportunity state transition records.
- `AssignmentEvent`: routing and ownership change history.
- `NotificationEvent`: message intent and delivery outcome reference.

Purpose:
- Tracks process progression, approvals, and operational coordination.

## Interchange and Integrations

- `ImportJob`: ingestion batch identity, status, and reconciliation summary.
- `ExportJob`: scoped export identity, policy, and completion status.
- `IntegrationSyncCheckpoint`: synchronization cursor and lag tracking.
- `IdempotencyKeyRecord`: duplicate protection keying and processing outcome.

Purpose:
- Governs safe data movement and integration reliability.

## Key Relationships

- One `Account` has many `Contact`, `Opportunity`, `Activity`, and `Case` records.
- One `Lead` can convert to at most one `Opportunity`.
- One `Opportunity` has many `Activity` and optional `Quote` records.
- `WorkflowInstanceReference`, `ApprovalDecision`, and `StageTransition` reference canonical domain IDs.
- `AuditEvent` correlates changes across domain, process, and integration aggregates.
- `CustomFieldValue` binds to `CustomFieldDefinition` and target entity identifiers.

## Invariants

- Converted leads are immutable except controlled audit-safe corrections.
- Opportunity stage transitions must follow an allowed state graph.
- Exactly one active owner exists for each lead, opportunity, and case at a time.
- Access checks are evaluated before retrieval and before mutation.
- Audit records are append-only and immutable.
- Integration upserts are idempotent within defined deduplication windows.

## Authoritative vs Projection Guidance

- Authoritative entities: `Account`, `Contact`, `Lead`, `Opportunity`, `Case`, `Activity`, `Quote`.
- Projection entities: search indexes, saved-view materializations, analytical summaries.
- Keep projection rebuild pathways explicit to preserve recovery and consistency behavior.
