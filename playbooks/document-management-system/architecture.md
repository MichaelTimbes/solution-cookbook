# DMS Architecture Composition

## Composition Intent

This architecture composes one primary archetype and multiple reusable capabilities to produce a governed document platform rather than a generic file store.

Primary archetype:
- [Document Management System](../../cookbook-v1/archetypes/document-management-system.md)

Supporting archetypal interactions:
- [Workflow / BPM System](../../cookbook-v1/archetypes/workflow-bpm-system.md) for process transitions.
- [Case / Ticket System](../../cookbook-v1/archetypes/case-ticket-system.md) for evidence-centric operations.
- [CMS / Wiki / Knowledge Base](../../cookbook-v1/archetypes/cms-wiki-kb.md) for curated publication of managed content.

## Logical Components

- Ingestion gateway: validates uploads/source handoff and initiates processing.
- Repository / Core State Store service: manages document object, version chain, and lifecycle state.
- Metadata and classification service: applies schema, taxonomy, and policy tags.
- Search/query service: supports document discovery and saved operational views.
- Workflow and Orchestration service: drives approvals, reviews, escalations, retention actions.
- Notification and Messaging service: emits user/system events for lifecycle and policy changes.
- Audit and Provenance service: records actor/action/object context across state changes.
- Data movement service: handles import/export jobs and reconciliation reporting.

## Capability Mapping

- Repository / Core State Store service -> [Approval Workflows / Human-In-The-Loop](../../cookbook-v1/capabilities/approval-workflows-human-in-the-loop.md)
- Metadata and classification service -> [Template / Merge Fields Document Generation](../../cookbook-v1/capabilities/template-merge-fields-document-generation.md)
- Search/query service -> [Search / Filters / Saved Views](../../cookbook-v1/capabilities/search-filters-saved-views.md)
- Notification and Messaging service -> [Notification / Messaging System](../../cookbook-v1/capabilities/notification-messaging-system.md)
- Audit and Provenance service -> [Audit Log + Provenance](../../cookbook-v1/capabilities/audit-log-provenance.md)
- Data movement service -> [Import / Export Pipelines](../../cookbook-v1/capabilities/import-export-pipelines.md)

## Boundary Principles

- Separate binary storage concerns from metadata/search concerns.
- Keep workflow state explicit and externally observable.
- Treat audit events as immutable evidence, not debug logs.
- Make import/export pathways first-class and policy-governed.
- Ensure access control is evaluated consistently in UI and API paths.

## Interaction Flow

- Ingestion and metadata services validate and enrich document submissions before persistence.
- Repository / Core State Store records canonical document, version, and lifecycle transitions.
- Workflow and orchestration coordinates review, approval, retention, and escalation behaviors.
- Search/query projections update asynchronously to support discovery and operational views.
- Notification and messaging emits lifecycle and policy events to human and system participants.
- Audit and provenance captures immutable transition and access evidence across all lifecycle actions.

## Evolution Anchors

- Start with ingestion + repository + metadata backbone.
- Add search relevance and saved operational views.
- Add workflow-driven approvals and lifecycle transitions.
- Add retention/legal hold policy engines and observability maturity.

## Diagram References

- [System context](diagrams/system-context.mmd)
- [Container view](diagrams/container-view.mmd)
- [Lifecycle flow](diagrams/lifecycle-flow.mmd)
