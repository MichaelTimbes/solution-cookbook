# DMS Workflows

## Core Workflow Set

## 1) Ingestion and Classification

1. Document is submitted through ingestion boundary.
2. Metadata schema is validated and normalized.
3. Classification and tags are applied.
4. Initial version is persisted in repository.
5. Search index is updated asynchronously.

Capabilities involved:
- [Import / Export Pipelines](../../cookbook/capabilities/import-export-pipelines.md)
- [Search / Filters / Saved Views](../../cookbook/capabilities/search-filters-saved-views.md)
- [Audit Log + Provenance](../../cookbook/capabilities/audit-log-provenance.md)

## 2) Review and Approval

1. Draft or new version enters approval process.
2. Workflow routes task to approver(s) based on policy.
3. Approver accepts/rejects/requests changes.
4. State transition and rationale are recorded.
5. Notifications are emitted to stakeholders.

Capabilities involved:
- [Approval Workflows / Human-In-The-Loop](../../cookbook/capabilities/approval-workflows-human-in-the-loop.md)
- [Notification / Messaging System](../../cookbook/capabilities/notification-messaging-system.md)
- [Audit Log + Provenance](../../cookbook/capabilities/audit-log-provenance.md)

## 3) Retrieval and Operational Search

1. User queries repository via search/filters.
2. Authorization constraints are applied.
3. Results are ranked and presented with saved views.
4. User opens specific version or history timeline.

Capabilities involved:
- [Search / Filters / Saved Views](../../cookbook/capabilities/search-filters-saved-views.md)
- [Audit Log + Provenance](../../cookbook/capabilities/audit-log-provenance.md)

## 4) Export and External Sharing

1. Scoped export request is created.
2. Dataset is assembled and validated.
3. Artifacts are generated and packaged.
4. Delivery events are tracked to completion.

Capabilities involved:
- [Import / Export Pipelines](../../cookbook/capabilities/import-export-pipelines.md)
- [Template / Merge Fields Document Generation](../../cookbook/capabilities/template-merge-fields-document-generation.md)
- [Notification / Messaging System](../../cookbook/capabilities/notification-messaging-system.md)

## 5) Retention and Archival

1. Policy engine evaluates retention status.
2. Documents transition to archive/hold/delete states.
3. Exceptions trigger human review workflows.
4. Final actions are audited and reported.

Capabilities involved:
- [Approval Workflows / Human-In-The-Loop](../../cookbook/capabilities/approval-workflows-human-in-the-loop.md)
- [Audit Log + Provenance](../../cookbook/capabilities/audit-log-provenance.md)
- [Notification / Messaging System](../../cookbook/capabilities/notification-messaging-system.md)
