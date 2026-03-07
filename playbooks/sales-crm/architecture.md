# Sales CRM Architecture Composition

## Composition Intent

This playbook composes the CRM archetype for sales operations where opportunity progression, pipeline governance, and accountable relationship management are primary concerns.

Primary archetype:
- [CRM](../../cookbook-v1/archetypes/crm.md)

Related archetypes:
- [Case / Ticket System](../../cookbook-v1/archetypes/case-ticket-system.md)
- [Workflow / BPM System](../../cookbook-v1/archetypes/workflow-bpm-system.md)
- [Document Management System](../../cookbook-v1/archetypes/document-management-system.md)

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

- Intake and qualification -> [Dynamic Evaluation / Survey Engine](../../cookbook-v1/capabilities/dynamic-evaluation-survey-engine.md), [Custom Fields / Extensible Attributes](../../cookbook-v1/capabilities/custom-fields-extensible-attributes.md)
- Opportunity governance -> [Rules Engine / Decisioning](../../cookbook-v1/capabilities/rules-engine-decisioning.md), [Approval Workflows / Human-In-The-Loop](../../cookbook-v1/capabilities/approval-workflows-human-in-the-loop.md)
- Pipeline visibility -> [Search / Filters / Saved Views](../../cookbook-v1/capabilities/search-filters-saved-views.md)
- Communication coordination -> [Notification Preferences and Routing](../../cookbook-v1/capabilities/notification-preferences-routing.md), [Notification / Messaging System](../../cookbook-v1/capabilities/notification-messaging-system.md)
- Integration reliability -> [Import / Export Pipelines](../../cookbook-v1/capabilities/import-export-pipelines.md), [Idempotency + Outbox + Retries + DLQ](../../cookbook-v1/capabilities/idempotency-outbox-retries-dlq.md)
- Lifecycle forensics -> [Audit Log + Provenance](../../cookbook-v1/capabilities/audit-log-provenance.md)

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
