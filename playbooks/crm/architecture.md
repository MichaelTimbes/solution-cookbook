# CRM Architecture Composition

## Composition Intent

This playbook composes the CRM archetype with cross-cutting capabilities to produce a governed system for customer lifecycle, pipeline progression, and account-centric collaboration.

Primary archetype:
- [CRM](../../cookbook/archetypes/crm.md)

Related archetypes:
- [Case / Ticket System](../../cookbook/archetypes/case-ticket-system.md)
- [Workflow / BPM System](../../cookbook/archetypes/workflow-bpm-system.md)
- [Analytics Platform](../../cookbook/archetypes/analytics-platform.md)

## Logical Components

- Input boundary service: accepts user and integration-originated changes.
- Repository / Core State Store service: persists authoritative customer, pipeline, and ownership state.
- Customer domain service: manages accounts, contacts, relationships, and ownership.
- Pipeline domain service: manages leads, opportunities, stage transitions, and qualification outcomes.
- Activity timeline service: captures tasks, meetings, calls, and interaction history.
- Case linkage service: links service interactions to account and opportunity context.
- Rules and decisioning service: evaluates assignment, scoring, transition, and policy rules.
- Workflow and Orchestration service: coordinates approvals, escalations, and exception paths.
- Search/query service: provides indexed retrieval, filtering, and saved operational views.
- Notification and Messaging service: publishes assignment and lifecycle events with routing controls.
- Audit and Provenance service: records immutable actor-action-object change history.
- Data movement service: handles imports, exports, and reconciliation with external boundaries.

## Capability Mapping

- Customer and pipeline domain services -> [Custom Fields / Extensible Attributes](../../cookbook/capabilities/custom-fields-extensible-attributes.md)
- Pipeline domain and rules services -> [Dynamic Evaluation / Survey Engine](../../cookbook/capabilities/dynamic-evaluation-survey-engine.md), [Rules Engine / Decisioning](../../cookbook/capabilities/rules-engine-decisioning.md)
- Search/query service -> [Query Filtering](../../cookbook/capabilities/query-filtering.md), [Saved Views](../../cookbook/capabilities/saved-views.md), [Search Index](../../cookbook/capabilities/search-index.md)
- Workflow orchestration -> [Approval Workflows / Human-In-The-Loop](../../cookbook/capabilities/approval-workflows-human-in-the-loop.md)
- Notification service -> [Notification Preferences and Routing](../../cookbook/capabilities/notification-preferences-routing.md), [Notification / Messaging System](../../cookbook/capabilities/notification-messaging-system.md)
- Data movement service -> [Import / Export Pipelines](../../cookbook/capabilities/import-export-pipelines.md), [Idempotency + Outbox + Retries + DLQ](../../cookbook/capabilities/idempotency-outbox-retries-dlq.md)
- Audit and Provenance service -> [Audit Log + Provenance](../../cookbook/capabilities/audit-log-provenance.md)

## Boundary Principles

- Keep authoritative record state separate from read-optimized query and search projections.
- Keep workflow orchestration separate from core domain state management.
- Keep rule evaluation explicit and versioned to avoid hidden behavior drift.
- Keep audit events immutable and independently queryable.
- Keep integration boundaries idempotent and observable.
- Keep notification generation separate from delivery policy and channel routing.

## Interaction Flow

- Requests enter through the input boundary and are validated against policy and schema rules.
- Domain services persist canonical state changes and publish lifecycle events.
- Workflow and rules services consume state events and produce governed transition outcomes.
- Search projections and analytics views update asynchronously from canonical change streams.
- Notification and integration services react to events and update external boundaries.
- Audit and observability capture all critical transitions for forensics and operations.

## Workflow / Lifecycle Handshake

- Workflow and orchestration commonly manage approvals, exception paths, and follow-up tasks around customer and pipeline work.
- CRM domain services typically own canonical mutation of accounts, contacts, leads, opportunities, cases, and ownership state.
- Workflow completion may trigger domain commands such as approve stage advancement or reassign ownership, but workflow state does not itself represent authoritative customer or pipeline truth.

## Read Model Strategy

- Canonical reads usually come from the primary CRM domain records for accounts, contacts, leads, opportunities, activities, and cases.
- Operational pipeline lists, team queues, and dashboard views often read from projection or read-model tables tuned for daily sales and service work.
- Search index reads are typically used for discovery, cross-account lookup, and full-text or faceted retrieval.
- Reporting, forecasting, and analytical summaries are often served from reporting projections rather than mutable domain tables.

## Typical Modular-Monolith Module Boundaries

These are typical in-process module boundaries for this playbook:
- Input Boundary
- Customer Domain
- Pipeline Domain
- Activity Timeline
- Case Linkage
- Rules and Decisioning
- Workflow and Orchestration
- Search and Query
- Notification and Messaging
- Audit and Provenance
- Data Movement

## Typical V1 Integration Boundaries

- Identity providers commonly supply user identity, team context, and authorization inputs.
- Marketing automation, support, and billing systems often exchange customer and lifecycle data.
- Messaging and notification providers commonly handle reminders, assignments, and follow-up delivery.
- External systems of record often receive exports or synchronization feeds for downstream processing.
- Third-party APIs typically connect through adapter boundaries with idempotent event handling and reconciliation checks.

## Evolution Anchors

- Start with core account, contact, lead, and opportunity state management.
- Add stage transition controls, search views, and ownership policy enforcement.
- Add workflow-driven approvals and notification routing for high-risk transitions.
- Add import/export synchronization with idempotent and reconciled integration behavior.
- Add governance maturity through audit depth and operational observability baselines.

## Diagram References

- [System context](diagrams/system-context.mmd)
- [Container view](diagrams/container-view.mmd)
- [Lifecycle flow](diagrams/lifecycle-flow.mmd)
