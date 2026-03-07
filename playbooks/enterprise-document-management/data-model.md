# Enterprise Document Management Data Model

- Core: `Document`, `DocumentVersion`, `Folder`, `Collection`
- Metadata: `Schema`, `FieldValue`, `ClassificationTag`
- Governance: `AccessPolicy`, `RetentionPolicy`, `AuditEvent`
- Workflow: `LifecycleState`, `ApprovalDecision`, `NotificationEvent`
- Integration: `ImportJob`, `ExportJob`, `SyncRecord`

Invariants: one current version per document; retention supersedes deletion; audit is immutable.
