# Patient Relationship Management Data Model

- Core: `PatientProfile`, `CareContact`, `EngagementInteraction`, `OutreachPlan`
- Metadata: `ConsentState`, `Preference`, `RiskTag`
- Governance: `AccessPolicySnapshot`, `ApprovalDecision`, `AuditEvent`
- Workflow: `FollowUpTask`, `StatusTransition`, `NotificationEvent`
- Integration: `SchedulingSyncRecord`, `CareSystemLink`

Invariants: access checks before retrieval; consent state applied before communication; audit history immutable.
