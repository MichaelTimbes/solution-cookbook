# Case / Ticket System Architecture Composition

## Composition Intent

This playbook composes the Case / Ticket archetype with reusable capabilities to produce a governed service operation platform for intake, triage, assignment, resolution, and closure under SLA constraints.

Primary archetype:
- [Case / Ticket System](../../cookbook/archetypes/case-ticket-system.md)

Related archetypes:
- [Workflow / BPM System](../../cookbook/archetypes/workflow-bpm-system.md)
- [CRM](../../cookbook/archetypes/crm.md)
- [CMS / Wiki / Knowledge Base](../../cookbook/archetypes/cms-wiki-kb.md)

## Logical Components

- Intake boundary service: accepts requests from portal, messaging, and API channels.
- Classification and prioritization service: assigns category, severity, and policy tags.
- Repository / Core State Store service: persists canonical ticket, assignment, and transition state.
- Queue and assignment service: manages ownership, team routing, and workload balancing.
- Ticket lifecycle service: controls state transitions and resolution context.
- SLA policy service: evaluates response and resolution timers against active policy versions.
- Workflow and Orchestration service: executes escalations, approvals, and exception paths.
- Notification and Messaging service: manages requester and internal notification delivery flows.
- Search and reporting query service: provides retrieval, saved views, and operational slices.
- Audit and Provenance service: records immutable events and service-level operational signals.
- Integration and data movement service: handles ingest, export, and external synchronization.

## Capability Mapping

- Intake, classification, and queueing -> [Custom Fields / Extensible Attributes](../../cookbook/capabilities/custom-fields-extensible-attributes.md), [Dynamic Evaluation / Survey Engine](../../cookbook/capabilities/dynamic-evaluation-survey-engine.md)
- Ticket lifecycle and policy logic -> [Rules Engine / Decisioning](../../cookbook/capabilities/rules-engine-decisioning.md), [Approval Workflows / Human-In-The-Loop](../../cookbook/capabilities/approval-workflows-human-in-the-loop.md)
- Search and operational triage -> [Query Filtering](../../cookbook/capabilities/query-filtering.md), [Saved Views](../../cookbook/capabilities/saved-views.md), [Search Index](../../cookbook/capabilities/search-index.md)
- Communication handling -> [Notification Preferences and Routing](../../cookbook/capabilities/notification-preferences-routing.md), [Notification / Messaging System](../../cookbook/capabilities/notification-messaging-system.md)
- Integration boundary and retry safety -> [Import / Export Pipelines](../../cookbook/capabilities/import-export-pipelines.md), [Idempotency + Outbox + Retries + DLQ](../../cookbook/capabilities/idempotency-outbox-retries-dlq.md)
- Process forensics -> [Audit Log + Provenance](../../cookbook/capabilities/audit-log-provenance.md)

## Boundary Principles

- Keep canonical ticket state separate from read-optimized query projections.
- Keep SLA and policy evaluation centralized and versioned.
- Keep workflow orchestration separate from core state mutation paths.
- Keep notification intent separate from channel delivery mechanics.
- Keep audit trails immutable and independently queryable.
- Keep integrations idempotent and monitored for drift.

## Interaction Flow

- Requests enter via intake boundaries and are normalized into canonical ticket records.
- Classification, queue, and assignment policies run before work enters active queues.
- Lifecycle changes publish events consumed by workflow, notification, and reporting services.
- SLA evaluation runs continuously against ticket state and policy timelines.
- Resolution and closure actions trigger communication, audit capture, and export synchronization.

## Workflow / Lifecycle Handshake

- Workflow and orchestration commonly manage approvals, escalations, and exception-handling tasks around ticket work.
- Ticket lifecycle services typically own canonical mutation of ticket status, assignment state, and closure outcomes.
- Workflow completion may trigger lifecycle commands such as escalate, reassign, or close, but workflow state does not by itself represent authoritative ticket truth.

## Read Model Strategy

- Canonical reads usually come from the primary ticket, queue, assignment, and SLA domain records.
- Operational lists, queue boards, and dashboard views often read from projection or read-model tables tuned for triage and workload visibility.
- Search index reads are typically used for discovery, keyword retrieval, and cross-ticket lookup.
- Reporting and compliance summaries are often served from reporting projections rather than mutable operational tables.

## Typical Modular-Monolith Module Boundaries

These are typical in-process module boundaries for this playbook:
- Intake and Classification
- Ticket Lifecycle
- Queue and Assignment
- SLA Policy
- Workflow and Orchestration
- Search and Operations Query
- Notification and Messaging
- Audit and Provenance
- Integration and Data Movement

## Typical V1 Integration Boundaries

- Identity providers commonly supply actor identity and authorization context.
- Messaging, email, or portal channels often provide ticket intake and outbound communication paths.
- CRM or account-context systems often enrich requester and customer data.
- Analytics and reporting systems commonly consume exports or projected summaries.
- Third-party APIs and external operational systems typically connect through adapter boundaries with idempotent event handling and reconciliation awareness.

## Evolution Anchors

- Start with intake, canonical ticket state, and queue assignment controls.
- Add SLA policy evaluation with deterministic escalation and notification behavior.
- Add workflow-driven exception handling and approval gates.
- Add integration synchronization with idempotent processing and reconciliation.
- Add operational governance with search quality, audit depth, and observability maturity.

## Diagram References

- [System context](diagrams/system-context.mmd)
- [Container view](diagrams/container-view.mmd)
- [Lifecycle flow](diagrams/lifecycle-flow.mmd)