# Approval Workflow Data Model

- Core: `ApprovalRequest`, `ApprovalStep`, `ApproverAssignment`, `Decision`
- Metadata: `PolicyRuleVersion`, `Priority`, `Category`
- Governance: `AuthorizationSnapshot`, `AuditEvent`
- Workflow: `StatusTransition`, `EscalationEvent`, `Deadline`
- Integration: `CallbackRecord`, `ExportRecord`

Invariants: decisions require authorized approver; transition graph enforced; audit is immutable.
