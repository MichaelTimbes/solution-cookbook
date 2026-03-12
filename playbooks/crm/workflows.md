# CRM Workflows

## Core Workflow Set

## Typical Workflow Units

Workflows in this playbook usually represent bounded process units inside broader relationship and pipeline lifecycles rather than the full customer lifecycle itself.

- Lead qualification workflow: intake, scoring, routing, and qualification decisions.
- Opportunity approval workflow: governed stage advancement for sensitive commercial transitions.
- External synchronization workflow: export, reconciliation, and retry-safe propagation to downstream systems.

## 1) Lead Intake and Qualification

1. A lead is created from user entry or integration import.
2. Required fields and policy checks are evaluated.
3. Qualification logic scores and classifies the lead.
4. Lead ownership is assigned or routed to a team queue.
5. Notifications are sent for follow-up actions.

Capabilities involved:
- [Import / Export Pipelines](../../cookbook/capabilities/import-export-pipelines.md)
- [Dynamic Evaluation / Survey Engine](../../cookbook/capabilities/dynamic-evaluation-survey-engine.md)
- [Rules Engine / Decisioning](../../cookbook/capabilities/rules-engine-decisioning.md)
- [Notification / Messaging System](../../cookbook/capabilities/notification-messaging-system.md)
- [Audit Log + Provenance](../../cookbook/capabilities/audit-log-provenance.md)

## 2) Lead Conversion to Opportunity

1. Conversion eligibility is checked against policy and completeness criteria.
2. Lead is converted into account, contact, and opportunity references.
3. Ownership and stage are initialized based on routing and territory rules.
4. Conversion events are emitted for downstream synchronization.

Capabilities involved:
- [Rules Engine / Decisioning](../../cookbook/capabilities/rules-engine-decisioning.md)
- [Custom Fields / Extensible Attributes](../../cookbook/capabilities/custom-fields-extensible-attributes.md)
- [Idempotency + Outbox + Retries + DLQ](../../cookbook/capabilities/idempotency-outbox-retries-dlq.md)
- [Audit Log + Provenance](../../cookbook/capabilities/audit-log-provenance.md)

## 3) Opportunity Progression and Approval

1. Opportunity advances through defined stages.
2. Sensitive transitions trigger workflow approval gates.
3. Approval outcomes update stage state and rationale.
4. Stakeholders receive notifications for accepted, rejected, or escalated decisions.

Capabilities involved:
- [Approval Workflows / Human-In-The-Loop](../../cookbook/capabilities/approval-workflows-human-in-the-loop.md)
- [Rules Engine / Decisioning](../../cookbook/capabilities/rules-engine-decisioning.md)
- [Notification Preferences and Routing](../../cookbook/capabilities/notification-preferences-routing.md)
- [Notification / Messaging System](../../cookbook/capabilities/notification-messaging-system.md)
- [Audit Log + Provenance](../../cookbook/capabilities/audit-log-provenance.md)

## 4) Operational Search and Pipeline Management

1. Users query records using filters and saved views.
2. Access policies scope visible rows and fields.
3. Teams triage pipeline items and schedule follow-up activities.
4. Query and action events are recorded for governance and observability.

Capabilities involved:
- [Query Filtering](../../cookbook/capabilities/query-filtering.md)
- [Saved Views](../../cookbook/capabilities/saved-views.md)
- [Search Index](../../cookbook/capabilities/search-index.md)
- [Custom Fields / Extensible Attributes](../../cookbook/capabilities/custom-fields-extensible-attributes.md)
- [Audit Log + Provenance](../../cookbook/capabilities/audit-log-provenance.md)

## 5) Export and External Synchronization

1. Export or sync requests are scoped by policy.
2. Canonical records are transformed into external integration contracts.
3. Delivery and retries are tracked to completion.
4. Reconciliation checks detect drift and partial failures.

Capabilities involved:
- [Import / Export Pipelines](../../cookbook/capabilities/import-export-pipelines.md)
- [Idempotency + Outbox + Retries + DLQ](../../cookbook/capabilities/idempotency-outbox-retries-dlq.md)
- [Notification / Messaging System](../../cookbook/capabilities/notification-messaging-system.md)
- [Audit Log + Provenance](../../cookbook/capabilities/audit-log-provenance.md)
