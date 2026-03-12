# Enterprise Document Management Data Model

## Core Aggregate Groups

### Core Domain Objects
- `Document`
- `DocumentVersion`
- `Folder`
- `Collection`

### Metadata and Classification
- `Schema`
- `FieldValue`
- `ClassificationTag`

### Access and Governance
- `AccessPolicy`
- `RetentionPolicy`
- `AuditEvent`

### Process and Workflow
- `LifecycleState`
- `ApprovalDecision`
- `NotificationEvent`

### Interchange and Integrations
- `ImportJob`
- `ExportJob`
- `SyncRecord`

## State Authority

- Authoritative domain state typically lives in `Document`, `DocumentVersion`, `Folder`, `Collection`, `Schema`, `FieldValue`, `AccessPolicy`, and `RetentionPolicy`.
- Supporting authoritative records commonly include `ApprovalDecision`, `LifecycleState`, `AuditEvent`, and synchronization checkpoints within their own concerns.
- Derived or rebuildable forms often include search documents, governance inboxes, notification delivery views, retention dashboards, and reporting summaries.
- Artifact or content-reference records may authoritatively locate files and binaries, but they typically do not own enterprise document lifecycle policy on their own.
- Search indexes, dashboards, and notifications are projections and should remain conceptually rebuildable from canonical repository and governance records.

## Invariants

- One current version exists per active document.
- Retention policy supersedes ordinary deletion paths.
- Lifecycle and approval actions retain immutable audit evidence.
- Integration exports remain scoped, attributable, and replay-safe.