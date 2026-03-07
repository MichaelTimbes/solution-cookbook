# Workflow / BPM Architecture Composition

## Composition Intent

This playbook composes the Workflow / BPM archetype with reliability, policy, and observability capabilities to provide durable process orchestration across human and system tasks.

Primary archetype:
- [Workflow / BPM System](../../cookbook-v1/archetypes/workflow-bpm-system.md)

Related archetypes:
- [Case / Ticket System](../../cookbook-v1/archetypes/case-ticket-system.md)
- [Document Management System](../../cookbook-v1/archetypes/document-management-system.md)
- [Identity / Access (CIAM)](../../cookbook-v1/archetypes/identity-access-ciam.md)

## Logical Components

- Process API boundary: receives process-start requests, signals, and task actions.
- Repository / Core State Store service: persists workflow state, task state, and transition history.
- Process definition service: manages process models, versioning, and deployment controls.
- Execution engine: manages workflow state transitions and task lifecycle coordination.
- Task orchestration service: assigns human/system tasks and tracks execution outcomes.
- Decisioning service: evaluates route logic, policies, and conditional branching.
- Scheduler and timer service: emits reminders, deadlines, and escalation triggers.
- Notification and Messaging service: handles process events, participant notifications, and external signals.
- Search and operations query service: supports operational monitoring, filtering, and backlog triage.
- Audit and Provenance service: records immutable process and administrative history.
- Integration and side-effect service: executes external calls with retry-safe semantics.

## Capability Mapping

- Execution and task services -> [Approval Workflows / Human-In-The-Loop](../../cookbook-v1/capabilities/approval-workflows-human-in-the-loop.md)
- Decisioning service -> [Rules Engine / Decisioning](../../cookbook-v1/capabilities/rules-engine-decisioning.md), [Dynamic Evaluation / Survey Engine](../../cookbook-v1/capabilities/dynamic-evaluation-survey-engine.md)
- Notification and signal service -> [Notification / Messaging System](../../cookbook-v1/capabilities/notification-messaging-system.md), [Notification Preferences and Routing](../../cookbook-v1/capabilities/notification-preferences-routing.md)
- Integration service -> [Idempotency + Outbox + Retries + DLQ](../../cookbook-v1/capabilities/idempotency-outbox-retries-dlq.md), [Import / Export Pipelines](../../cookbook-v1/capabilities/import-export-pipelines.md)
- Operations query service -> [Search / Filters / Saved Views](../../cookbook-v1/capabilities/search-filters-saved-views.md)
- Process configurability -> [Custom Fields / Extensible Attributes](../../cookbook-v1/capabilities/custom-fields-extensible-attributes.md)
- Audit and forensics -> [Audit Log + Provenance](../../cookbook-v1/capabilities/audit-log-provenance.md)

## Boundary Principles

- Keep process definitions immutable by version once deployed.
- Keep orchestration state management separate from domain side-effect handlers.
- Keep timer and escalation scheduling deterministic and replay-safe.
- Keep external integration side effects idempotent and observable.
- Keep audit streams immutable and independently queryable.
- Keep operator overrides explicit, authorized, and fully audited.

## Interaction Flow

- Process API accepts start/signal/task requests and validates authorization and schema.
- Execution engine applies versioned process graph rules to determine next transitions.
- Decisioning and scheduling services emit transition triggers and escalation events.
- Notification and integration services consume process events and perform side effects.
- Search and operations projections update asynchronously for dashboards and triage.
- Audit service captures all transitions, overrides, and policy decisions.

## Evolution Anchors

- Start with versioned process definitions, execution state, and task coordination.
- Add policy-driven branching, approval controls, and deterministic transition enforcement.
- Add scheduler, escalation, and notification behavior for long-running reliability.
- Add idempotent integration side-effects with retry, dead-letter, and replay-safe recovery.
- Add observability and governance maturity for operational optimization and forensics.

## Diagram References

- [System context](diagrams/system-context.mmd)
- [Container view](diagrams/container-view.mmd)
- [Lifecycle flow](diagrams/lifecycle-flow.mmd)