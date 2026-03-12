# Approval Workflow Data Model (Architecture View)

## Core Aggregate Groups

## Core Domain Objects

- `ApprovalRequest`: canonical request under policy-governed lifecycle control.
- `ApprovalStep`: ordered step within a multi-stage approval route.
- `ApproverAssignment`: actor assignment and responsibility context.
- `DecisionRecord`: explicit approve/reject/outcome evidence.
- `RequestAttachment`: evidence or context artifact linked to request.

Purpose:
- Encapsulates decision workflow state from submission through completion.

## Metadata and Classification

- `PolicyRuleVersion`: effective routing/evaluation policy snapshot.
- `PriorityClass`: urgency and SLA classification label.
- `RequestCategory`: taxonomy used for routing and governance.
- `CustomFieldDefinition`: extensible request schema policy.
- `CustomFieldValue`: typed extension values.

Purpose:
- Supports policy-consistent classification and extensible approval metadata.

## Access and Governance

- `AuthorizationSnapshot`: approver eligibility evidence at decision time.
- `RoleAssignment`: scope and permission binding for workflow actions.
- `DelegationRecord`: approved temporary decision delegation context.
- `AuditEvent`: immutable actor-action-object lifecycle evidence.

Purpose:
- Enforces trusted authorization controls and accountable decision lineage.

## Process and Workflow

- `StatusTransition`: explicit lifecycle progression records.
- `EscalationEvent`: timeout/escalation outcome records.
- `DeadlineTimer`: due-date and SLA timing state.
- `NotificationEvent`: reminder and outcome communication intent.

Purpose:
- Drives deterministic progression and escalation behavior under time constraints.

## Interchange and Integrations

- `CallbackRecord`: downstream callback delivery and acknowledgment.
- `ExportJob`: governed outbound decision data movement job.
- `IntegrationSyncCheckpoint`: external synchronization reconciliation cursor.
- `IdempotencyKeyRecord`: replay protection and deduplication ledger.

Purpose:
- Stabilizes downstream propagation and integration reliability.

## Key Relationships

- One `ApprovalRequest` has many `ApprovalStep`, `ApproverAssignment`, and `DecisionRecord` entries.
- One `ApprovalRequest` has many `StatusTransition`, `EscalationEvent`, and `NotificationEvent` records.
- `AuthorizationSnapshot` and `DelegationRecord` bind to relevant decision events.
- `CallbackRecord` references terminal decision outcomes for downstream consumers.
- `AuditEvent` correlates submission, routing, escalation, and completion actions.

## State Authority

- Authoritative domain state typically lives in `ApprovalRequest`, `ApprovalStep`, `ApproverAssignment`, `DecisionRecord`, `StatusTransition`, and `DeadlineTimer`.
- Supporting authoritative records commonly include `AuthorizationSnapshot`, `DelegationRecord`, `AuditEvent`, and callback or synchronization checkpoints within their own concerns.
- Derived or rebuildable forms often include approval inboxes, search documents, notification delivery views, SLA dashboards, and reporting summaries.
- Request attachments or artifacts may be authoritative within their own artifact boundary, but they typically do not own approval lifecycle state.
- Search indexes, dashboards, and notifications are projections and should remain conceptually rebuildable from canonical approval records.

## Invariants

- Decision actions require authorized approvers at decision time.
- Request transitions must follow policy-defined allowed paths.
- Escalation timers must align with current lifecycle state.
- Audit and provenance records are immutable and append-only.
- Callback replays are deduplicated through idempotency controls.
