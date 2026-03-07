# Records Management Data Model

- Core: `Record`, `RecordSeries`, `RecordVersion`, `DispositionOrder`
- Metadata: `RetentionCode`, `HoldTag`, `Classification`
- Governance: `HoldPolicy`, `RetentionPolicy`, `AuditEvent`
- Workflow: `DispositionApproval`, `StatusTransition`, `NotificationEvent`
- Integration: `ArchiveTransfer`, `RegulatoryExport`

Invariants: legal hold blocks disposition; retention policy version is persisted with record; disposition is auditable.
