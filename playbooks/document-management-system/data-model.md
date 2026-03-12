# DMS Data Model (Architecture View)

## Core Aggregate Groups

## Document Aggregate

- `Document`
- `DocumentVersion`
- `DocumentContentReference`
- `DocumentLifecycleState`

Purpose:
- Represents canonical document identity, version lineage, and state progression.

## Metadata and Classification Aggregate

- `MetadataSchema`
- `MetadataFieldDefinition`
- `MetadataValue`
- `ClassificationTag`

Purpose:
- Enables consistent indexing, filtering, retention, and policy evaluation.

## Access and Governance Aggregate

- `AccessPolicy`
- `AccessGrant`
- `RetentionPolicy`
- `LegalHold`

Purpose:
- Enforces who can access content and how long content remains active.

## Process and Activity Aggregate

- `WorkflowInstanceReference`
- `ApprovalDecision`
- `NotificationEvent`
- `AuditEvent`

Purpose:
- Connects document lifecycle transitions to approvals, communication, and forensic history.

## Interchange Aggregate

- `ImportJob`
- `ExportJob`
- `ExportArtifact`

Purpose:
- Governs boundary-crossing data movement with policy controls and status tracking.

## Key Relationships

- One `Document` has many `DocumentVersion` records.
- `DocumentVersion` references metadata values bound to active schema definitions.
- `Document` is evaluated by access and retention policies at request time.
- Workflow decisions and notifications reference document and version IDs.
- Audit events correlate ingestion, retrieval, approval, and export actions.

## State Authority

- Authoritative domain state typically lives in `Document`, `DocumentVersion`, `DocumentContentReference`, `DocumentLifecycleState`, `MetadataSchema`, `MetadataValue`, `AccessPolicy`, `RetentionPolicy`, and `LegalHold`.
- Supporting authoritative records commonly include `ApprovalDecision`, `WorkflowInstanceReference`, `AuditEvent`, `ImportJob`, `ExportJob`, and artifact/content linkage records within their own concerns.
- Derived or rebuildable forms often include search documents, operational inboxes, retention dashboards, notification delivery views, and reporting summaries.
- Artifact and content-reference records may authoritatively locate files and versioned binaries, but they typically do not own business lifecycle policy or document-state truth on their own.
- Search indexes, dashboards, and notification views are projections and should remain conceptually rebuildable from canonical repository and policy records.

## Invariants

- Exactly one current version per document within active state.
- Version history is append-only once published.
- Access checks apply before content access and before metadata-sensitive query results.
- Retention and legal hold status always supersede standard deletion paths.
- Export jobs are scoped and auditable.
