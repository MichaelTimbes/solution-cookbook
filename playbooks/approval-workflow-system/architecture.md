# Approval Workflow Architecture Composition

## Composition Intent

This playbook composes the Workflow / BPM archetype for decision-centric operations where policy-governed approvals, escalation control, and immutable decision traceability are primary concerns.

Primary archetype:
- [Workflow / BPM System](../../cookbook-v1/archetypes/workflow-bpm-system.md)

Related archetypes:
- [Case / Ticket System](../../cookbook-v1/archetypes/case-ticket-system.md)
- [Identity / Access (CIAM)](../../cookbook-v1/archetypes/identity-access-ciam.md)
- [Document Management System](../../cookbook-v1/archetypes/document-management-system.md)

## Logical Components

- Intake boundary service: accepts approval requests from UI, API, and integration channels.
- Policy evaluation service: determines routing, priority, and approval path constraints.
- Repository / Core State Store service: persists canonical request, assignment, and decision state.
- Approval routing service: assigns approvers and manages multi-step progression.
- Workflow and Orchestration service: coordinates timer-based escalation and exception handling.
- Notification and Messaging service: issues reminders, escalations, and outcome communications.
- Search and reporting query service: supports queue management and SLA visibility.
- Audit and Provenance service: records immutable actor-action-object decision evidence.
- Integration and data movement service: executes callback delivery and export synchronization.

## Capability Mapping

- Request capture and qualification -> [Dynamic Evaluation / Survey Engine](../../cookbook-v1/capabilities/dynamic-evaluation-survey-engine.md), [Custom Fields / Extensible Attributes](../../cookbook-v1/capabilities/custom-fields-extensible-attributes.md)
- Policy routing controls -> [Rules Engine / Decisioning](../../cookbook-v1/capabilities/rules-engine-decisioning.md), [Approval Workflows / Human-In-The-Loop](../../cookbook-v1/capabilities/approval-workflows-human-in-the-loop.md)
- Queue visibility -> [Search / Filters / Saved Views](../../cookbook-v1/capabilities/search-filters-saved-views.md)
- Escalation communication -> [Notification Preferences and Routing](../../cookbook-v1/capabilities/notification-preferences-routing.md), [Notification / Messaging System](../../cookbook-v1/capabilities/notification-messaging-system.md)
- Callback reliability -> [Import / Export Pipelines](../../cookbook-v1/capabilities/import-export-pipelines.md), [Idempotency + Outbox + Retries + DLQ](../../cookbook-v1/capabilities/idempotency-outbox-retries-dlq.md)
- Decision forensics -> [Audit Log + Provenance](../../cookbook-v1/capabilities/audit-log-provenance.md)

## Boundary Principles

- Keep canonical request lifecycle state separate from read-optimized queue projections.
- Keep workflow and orchestration separate from direct request mutation paths.
- Keep notification intent separate from delivery channel execution.
- Keep audit and provenance records immutable and independently queryable.
- Keep callback and export processing idempotent and replay-safe.

## Interaction Flow

- Intake boundaries normalize request submissions and policy-relevant metadata.
- Policy evaluation and routing establish approver sequence and deadlines.
- Repository/core state store persists request transitions and decision outcomes.
- Workflow and orchestration drives escalation timers and exception routes.
- Notification and messaging communicates pending actions and final decisions.
- Search/query projections support queue operations and SLA monitoring.
- Audit and provenance captures immutable approval lifecycle evidence.

## Evolution Anchors

- Start with request intake, assignment, and canonical decision lifecycle state.
- Add deterministic policy routing and multi-step approval governance.
- Add escalation orchestration and channel-aware notification controls.
- Add idempotent callback and integration synchronization behaviors.
- Add observability and governance optimization for approval throughput.

## Diagram References

- [System context](diagrams/system-context.mmd)
- [Container view](diagrams/container-view.mmd)
- [Lifecycle flow](diagrams/lifecycle-flow.mmd)
