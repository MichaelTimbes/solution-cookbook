# Sales CRM Data Model

- Core: `Account`, `Contact`, `Lead`, `Opportunity`, `Quote`, `Activity`
- Metadata: `SegmentTag`, `Score`, `CustomFieldValue`
- Governance: `OwnerAssignment`, `RoleAssignment`, `AuditEvent`
- Workflow: `StageTransition`, `ApprovalDecision`, `Task`
- Integration: `SyncCheckpoint`, `ExportJob`

Invariants: one active owner per opportunity; stage transitions follow policy graph; audit history is append-only.
