# DMS Architecture Composition

## Composition Intent

This architecture composes one primary archetype and multiple reusable capabilities to describe a document platform with stronger governance, retrieval, and lifecycle expectations than a generic file store.

Primary archetype:
- [Document Management System](../../cookbook/archetypes/document-management-system.md)

Supporting archetypal interactions:
- [Workflow / BPM System](../../cookbook/archetypes/workflow-bpm-system.md) for process transitions.
- [Case / Ticket System](../../cookbook/archetypes/case-ticket-system.md) for evidence-centric operations.
- [CMS / Wiki / Knowledge Base](../../cookbook/archetypes/cms-wiki-kb.md) for curated publication of managed content.

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

- Repository / Core State Store service -> [Artifact Repository](../../cookbook/capabilities/artifact-repository.md)
- Metadata and classification service -> [Template / Merge Fields Document Generation](../../cookbook/capabilities/template-merge-fields-document-generation.md)
- Search/query service -> [Query Filtering](../../cookbook/capabilities/query-filtering.md), [Saved Views](../../cookbook/capabilities/saved-views.md), [Search Index](../../cookbook/capabilities/search-index.md)
- Workflow and Orchestration service -> [Approval Workflows / Human-In-The-Loop](../../cookbook/capabilities/approval-workflows-human-in-the-loop.md), [Human Communication](../../cookbook/capabilities/human-communication.md)
- Notification and Messaging service -> [Notification / Messaging System](../../cookbook/capabilities/notification-messaging-system.md)
- Audit and Provenance service -> [Audit Log + Provenance](../../cookbook/capabilities/audit-log-provenance.md)
- Data movement service -> [Import / Export Pipelines](../../cookbook/capabilities/import-export-pipelines.md)

## Boundary Principles

- Binary storage concerns are typically kept distinct from metadata and query concerns.
- Workflow state is often kept explicit and externally observable.
- Audit events are typically treated as immutable evidence rather than transient debug data.
- Import/export pathways are often modeled as explicit, policy-governed boundaries.
- Access control evaluation is typically kept consistent across UI and API paths.

## Interaction Flow

- Ingestion and metadata services validate and enrich document submissions before persistence.
- Repository / Core State Store records canonical document, version, and lifecycle transitions.
- Workflow and orchestration coordinates review, approval, retention, and escalation behaviors.
- Search/query projections update asynchronously to support discovery and operational views.
- Notification and messaging emits lifecycle and policy events to human and system participants.
- Audit and provenance captures immutable transition and access evidence across all lifecycle actions.

## Workflow / Lifecycle Handshake

- Workflow and orchestration commonly manage review, approval, escalation, and retention-related tasks around documents.
- Repository and lifecycle services typically own canonical mutation of document identity, version lineage, and lifecycle state.
- Workflow completion may trigger domain commands such as publish, archive, or request revision, but workflow state does not itself represent authoritative document truth.

## Read Model Strategy

- Canonical reads usually come from the primary document, version, metadata, access, and retention records.
- Operational lists, inboxes, and policy work queues often read from projection or read-model tables tuned for review and governance work.
- Search index reads are typically used for discovery, full-text retrieval, and faceted lookup.
- Reporting and compliance summaries are often served from reporting projections rather than mutable repository tables.

## Typical Modular-Monolith Module Boundaries

These are typical in-process module boundaries for this playbook:
- Ingestion Gateway
- Repository and Lifecycle
- Metadata and Classification
- Search and Query
- Workflow and Orchestration
- Notification and Messaging
- Audit and Provenance
- Data Movement

## Typical V1 Integration Boundaries

- Identity providers commonly supply actor identity and access context.
- File storage or object storage boundaries commonly persist binary document content.
- OCR, extraction, or malware scanning services often enrich or validate inbound content.
- Messaging providers commonly deliver review, policy, and lifecycle notifications.
- External partner systems and third-party APIs typically connect through adapter boundaries with idempotent event handling and reconciliation awareness.

## Evolution Anchors

- Start with ingestion + repository + metadata backbone.
- Add search relevance and saved operational views.
- Add workflow-driven approvals and lifecycle transitions.
- Add retention/legal hold policy engines and observability maturity.

## Diagram References

- [System context](diagrams/system-context.mmd)
- [Container view](diagrams/container-view.mmd)
- [Lifecycle flow](diagrams/lifecycle-flow.mmd)

