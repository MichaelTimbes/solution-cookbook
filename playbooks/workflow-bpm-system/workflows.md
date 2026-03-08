# Workflow / BPM Workflows

## Core Workflow Set

## 1) Process Modeling and Version Deployment

1. Process model is authored and validated against governance controls.
2. Version is approved and deployed as an immutable runtime definition.
3. Deployment metadata and policy versions are recorded.
4. New instances begin execution against the deployed version.

Capabilities involved:
- [Approval Workflows / Human-In-The-Loop](../../cookbook/capabilities/approval-workflows-human-in-the-loop.md)
- [Rules Engine / Decisioning](../../cookbook/capabilities/rules-engine-decisioning.md)
- [Audit Log + Provenance](../../cookbook/capabilities/audit-log-provenance.md)

## 2) Instance Start and Task Routing

1. Process start request enters API boundary with initial variables.
2. Execution engine initializes workflow state and creates first tasks.
3. Decision rules select branch path and assignees.
4. Notifications are sent to participants or system handlers.

Capabilities involved:
- [Dynamic Evaluation / Survey Engine](../../cookbook/capabilities/dynamic-evaluation-survey-engine.md)
- [Rules Engine / Decisioning](../../cookbook/capabilities/rules-engine-decisioning.md)
- [Notification / Messaging System](../../cookbook/capabilities/notification-messaging-system.md)
- [Notification Preferences and Routing](../../cookbook/capabilities/notification-preferences-routing.md)

## 3) Human Approval and Exception Handling

1. Task is claimed and acted on by an authorized participant.
2. Approval decision updates workflow state and rationale.
3. Rejections or exceptions route to alternate paths.
4. Escalations are triggered when deadlines are exceeded.

Capabilities involved:
- [Approval Workflows / Human-In-The-Loop](../../cookbook/capabilities/approval-workflows-human-in-the-loop.md)
- [Query Filtering](../../cookbook/capabilities/query-filtering.md)
- [Saved Views](../../cookbook/capabilities/saved-views.md)
- [Search Index](../../cookbook/capabilities/search-index.md)
- [Notification / Messaging System](../../cookbook/capabilities/notification-messaging-system.md)
- [Audit Log + Provenance](../../cookbook/capabilities/audit-log-provenance.md)

## 4) Timer, Retry, and Compensation Flow

1. Scheduler emits timer events for reminders and deadlines.
2. Failed side effects trigger retry policy evaluation.
3. Exhausted retries move tasks to dead-letter handling.
4. Compensation actions execute to restore consistent business state.

Capabilities involved:
- [Idempotency + Outbox + Retries + DLQ](../../cookbook/capabilities/idempotency-outbox-retries-dlq.md)
- [Rules Engine / Decisioning](../../cookbook/capabilities/rules-engine-decisioning.md)
- [Notification / Messaging System](../../cookbook/capabilities/notification-messaging-system.md)
- [Audit Log + Provenance](../../cookbook/capabilities/audit-log-provenance.md)

## 5) Completion, Export, and Operational Review

1. Workflow reaches terminal state and captures completion outcome.
2. Completion artifacts and event history are exported as required.
3. Operational views update for throughput and backlog analysis.
4. Analysts review trends and identify process improvement opportunities.

Capabilities involved:
- [Import / Export Pipelines](../../cookbook/capabilities/import-export-pipelines.md)
- [Query Filtering](../../cookbook/capabilities/query-filtering.md)
- [Saved Views](../../cookbook/capabilities/saved-views.md)
- [Search Index](../../cookbook/capabilities/search-index.md)
- [Template / Merge Fields Document Generation](../../cookbook/capabilities/template-merge-fields-document-generation.md)
- [Audit Log + Provenance](../../cookbook/capabilities/audit-log-provenance.md)