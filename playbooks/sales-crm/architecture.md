# Sales CRM Architecture Composition

## Composition Intent

This playbook composes the CRM archetype for sales operations where opportunity progression, pipeline governance, and accountable relationship management are primary concerns.

Primary archetype:
- [CRM](../../cookbook/archetypes/crm.md)

Related archetypes:
- [Case / Ticket System](../../cookbook/archetypes/case-ticket-system.md)
- [Workflow / BPM System](../../cookbook/archetypes/workflow-bpm-system.md)
- [Document Management System](../../cookbook/archetypes/document-management-system.md)

## Logical Components

- Intake boundary service: accepts lead and relationship events from forms, APIs, and integrations.
- Lead qualification service: evaluates intake quality and routing readiness.
- Repository / Core State Store service: persists canonical lead, account, contact, opportunity, and activity state.
- Opportunity lifecycle service: manages stage transitions and pipeline ownership.
- Workflow and Orchestration service: governs approvals, exception handling, and stage gates.
- Notification and Messaging service: manages follow-up reminders and stakeholder updates.
- Search and reporting query service: supports territory, pipeline, and forecast views.
- Audit and Provenance service: records immutable actor-action-object lifecycle evidence.
- Integration and data movement service: coordinates bidirectional sync and controlled exports.

## Capability Mapping

- Intake and qualification -> [Dynamic Evaluation / Survey Engine](../../cookbook/capabilities/dynamic-evaluation-survey-engine.md), [Custom Fields / Extensible Attributes](../../cookbook/capabilities/custom-fields-extensible-attributes.md)
- Opportunity governance -> [Rules Engine / Decisioning](../../cookbook/capabilities/rules-engine-decisioning.md), [Approval Workflows / Human-In-The-Loop](../../cookbook/capabilities/approval-workflows-human-in-the-loop.md)
- Pipeline visibility -> [Query Filtering](../../cookbook/capabilities/query-filtering.md), [Saved Views](../../cookbook/capabilities/saved-views.md), [Search Index](../../cookbook/capabilities/search-index.md)
- Communication coordination -> [Notification Preferences and Routing](../../cookbook/capabilities/notification-preferences-routing.md), [Notification / Messaging System](../../cookbook/capabilities/notification-messaging-system.md)
- Integration reliability -> [Import / Export Pipelines](../../cookbook/capabilities/import-export-pipelines.md), [Idempotency + Outbox + Retries + DLQ](../../cookbook/capabilities/idempotency-outbox-retries-dlq.md)
- Lifecycle forensics -> [Audit Log + Provenance](../../cookbook/capabilities/audit-log-provenance.md)

## Boundary Principles

- Keep canonical CRM lifecycle state separate from read-optimized forecast projections.
- Keep workflow and orchestration separate from direct lifecycle state mutation.
- Keep notification intent separate from channel delivery execution.
- Keep audit and provenance evidence immutable and independently queryable.
- Keep integration synchronization idempotent and reconciliation-aware.

## Interaction Flow

- Intake boundaries normalize leads and relationship updates.
- Qualification and opportunity services assign ownership and stage context.
- Repository/core state store persists lifecycle transitions and activity updates.
- Workflow and orchestration evaluates stage gates and approval checkpoints.
- Notification and messaging distributes tasks, reminders, and status changes.
- Search/query projections support pipeline visibility and operational reporting.
- Audit and provenance captures immutable lifecycle evidence for governance.

## Workflow / Lifecycle Handshake

- Workflow and orchestration commonly manage approvals, exception handling, and follow-up tasks around pipeline work.
- Sales CRM lifecycle services typically own canonical mutation of lead, account, contact, opportunity, and stage state.
- Workflow completion may trigger domain commands such as advance stage, assign owner, or approve exceptions, but workflow state does not itself represent authoritative sales-lifecycle truth.

## Read Model Strategy

- Canonical reads usually come from the primary lead, account, contact, opportunity, activity, and stage-transition records.
- Pipeline boards, territory views, and forecast worklists often read from projection or read-model tables tuned for daily sales operations.
- Search index reads are typically used for discovery, relationship lookup, and keyword retrieval.
- Reporting and forecast summaries are often served from reporting projections rather than mutable domain tables.

## Typical Modular-Monolith Module Boundaries

These are typical in-process module boundaries for this playbook:
- Intake Boundary
- Lead Qualification
- Opportunity Lifecycle
- Workflow and Orchestration
- Search and Reporting Query
- Notification and Messaging
- Audit and Provenance
- Integration and Data Movement

## Typical V1 Integration Boundaries

- Forms, campaign, and API channels commonly provide lead ingress.
- Adjacent CRM, support, and document systems often exchange relationship context.
- Messaging providers commonly deliver reminders and stakeholder updates.
- Downstream analytics and business systems often consume exports or synchronization feeds.
- External adapters typically use idempotent event handling and reconciliation-aware synchronization.

## Evolution Anchors

- Start with lead/account/contact and opportunity baseline lifecycle.
- Add policy-governed stage progression and approval controls.
- Add exception-aware workflow orchestration and communication routing.
- Add integration synchronization with replay-safe idempotent processing.
- Add observability and governance optimization for forecast confidence.

## Diagram References

- [System context](diagrams/system-context.mmd)
- [Container view](diagrams/container-view.mmd)
- [Lifecycle flow](diagrams/lifecycle-flow.mmd)
