# Sales CRM Data Model (Architecture View)

## Core Aggregate Groups

## Core Domain Objects

- `Lead`: candidate demand signal entering qualification process.
- `Account`: organizational relationship anchor.
- `Contact`: person-level relationship and communication profile.
- `Opportunity`: pipeline entity under governed stage progression.
- `Activity`: interaction timeline artifact (call, email, meeting, task).

Purpose:
- Encapsulates sales relationship and opportunity lifecycle state.

## Metadata and Classification

- `LeadScore`: qualification outcome and fit indicator.
- `OpportunityStage`: normalized pipeline stage definition.
- `Segment`: territory or market partition context.
- `CustomFieldDefinition`: extensible schema policy.
- `CustomFieldValue`: typed extension values.

Purpose:
- Supports qualification governance, segmentation, and adaptive CRM schema.

## Access and Governance

- `RoleAssignment`: role-based scope and ownership authority.
- `OwnershipAssignment`: assignment lineage for account/opportunity entities.
- `ApprovalDecision`: approval outcomes for discounts and stage exceptions.
- `AuditEvent`: immutable actor-action-object lifecycle evidence.

Purpose:
- Enforces governance controls and accountable revenue process history.

## Process and Workflow

- `StageTransition`: explicit stage progression records.
- `QualificationEvaluation`: dynamic qualification decision output.
- `ReminderSchedule`: follow-up and time-bound action policy.
- `NotificationEvent`: communication intent and delivery references.

Purpose:
- Drives predictable opportunity progression and disciplined follow-up workflows.

## Interchange and Integrations

- `InboundIntegrationEvent`: normalized external CRM update message.
- `ExportJob`: governed outbound data movement job.
- `IntegrationSyncCheckpoint`: synchronization cursor and checkpoint.
- `IdempotencyKeyRecord`: replay protection and deduplication ledger.

Purpose:
- Stabilizes cross-system synchronization and prevents duplicate lifecycle side effects.

## Key Relationships

- One `Account` has many `Contact` and `Opportunity` records.
- One `Opportunity` has many `Activity`, `StageTransition`, and `NotificationEvent` records.
- One `Lead` may convert into linked `Account`, `Contact`, and `Opportunity` entities.
- `ApprovalDecision` records are linked to relevant stage or pricing exceptions.
- `AuditEvent` correlates ownership, stage, and communication transitions.

## Invariants

- Opportunity stage transitions must follow policy-defined allowed paths.
- Ownership changes require actor attribution and timestamped lineage.
- Approval-required transitions cannot complete without decision records.
- Audit and provenance records are immutable and append-only.
- Integration replays are deduplicated using idempotency controls.
