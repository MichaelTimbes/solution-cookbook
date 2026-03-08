# Sales CRM Workflows

## Core Workflow Set

## 1) Lead Intake and Qualification

1. Lead enters from forms, campaigns, partner feeds, or API channels.
2. Intake validation applies required schema and deduplication controls.
3. Qualification rules evaluate fit, urgency, and assignment routing.
4. Qualified lead routes into accountable owner workflow.

Capabilities involved:
- [Dynamic Evaluation / Survey Engine](../../cookbook/capabilities/dynamic-evaluation-survey-engine.md)
- [Rules Engine / Decisioning](../../cookbook/capabilities/rules-engine-decisioning.md)
- [Custom Fields / Extensible Attributes](../../cookbook/capabilities/custom-fields-extensible-attributes.md)
- [Audit Log + Provenance](../../cookbook/capabilities/audit-log-provenance.md)

## 2) Opportunity Creation and Stage Progression

1. Qualified lead converts to account/contact/opportunity records.
2. Opportunity progresses through policy-defined stage transitions.
3. Ownership and next-action tasks are updated by lifecycle events.
4. Pipeline and forecast views refresh from lifecycle projections.

Capabilities involved:
- [Query Filtering](../../cookbook/capabilities/query-filtering.md)
- [Saved Views](../../cookbook/capabilities/saved-views.md)
- [Search Index](../../cookbook/capabilities/search-index.md)
- [Rules Engine / Decisioning](../../cookbook/capabilities/rules-engine-decisioning.md)
- [Notification / Messaging System](../../cookbook/capabilities/notification-messaging-system.md)
- [Audit Log + Provenance](../../cookbook/capabilities/audit-log-provenance.md)

## 3) Approval and Exception Governance

1. Policy-sensitive actions (discount, stage bypass, close-date override) trigger approval flows.
2. Approvers review context and approve or reject exception requests.
3. Outcomes update opportunity state and lifecycle constraints.
4. Decision lineage is retained for governance and forecast trust.

Capabilities involved:
- [Approval Workflows / Human-In-The-Loop](../../cookbook/capabilities/approval-workflows-human-in-the-loop.md)
- [Notification Preferences and Routing](../../cookbook/capabilities/notification-preferences-routing.md)
- [Notification / Messaging System](../../cookbook/capabilities/notification-messaging-system.md)
- [Audit Log + Provenance](../../cookbook/capabilities/audit-log-provenance.md)

## 4) Communication and Follow-Up Orchestration

1. Follow-up schedules generate reminders and activity commitments.
2. Stakeholder updates are routed to appropriate channels and recipients.
3. Activity outcomes are captured as part of canonical opportunity history.
4. Missed follow-ups are surfaced in operational views.

Capabilities involved:
- [Notification Preferences and Routing](../../cookbook/capabilities/notification-preferences-routing.md)
- [Notification / Messaging System](../../cookbook/capabilities/notification-messaging-system.md)
- [Query Filtering](../../cookbook/capabilities/query-filtering.md)
- [Saved Views](../../cookbook/capabilities/saved-views.md)
- [Search Index](../../cookbook/capabilities/search-index.md)
- [Audit Log + Provenance](../../cookbook/capabilities/audit-log-provenance.md)

## 5) Export and Integration Synchronization

1. CRM snapshots and deltas are packaged for downstream systems.
2. Export and sync jobs execute under idempotent delivery controls.
3. Retry and DLQ handling captures unresolved integration failures.
4. Reconciliation checkpoints confirm lifecycle consistency.

Capabilities involved:
- [Import / Export Pipelines](../../cookbook/capabilities/import-export-pipelines.md)
- [Idempotency + Outbox + Retries + DLQ](../../cookbook/capabilities/idempotency-outbox-retries-dlq.md)
- [Notification / Messaging System](../../cookbook/capabilities/notification-messaging-system.md)
- [Audit Log + Provenance](../../cookbook/capabilities/audit-log-provenance.md)
