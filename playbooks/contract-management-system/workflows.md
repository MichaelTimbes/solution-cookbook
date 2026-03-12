# Contract Management Workflows

## Core Workflow Set

## Typical Workflow Units

In contract systems, workflows usually operate at a narrower scope than the full contract lifecycle. They commonly orchestrate tasks and approvals around a particular lifecycle moment, while the canonical lifecycle state remains owned by the contract lifecycle domain.

A review workflow is usually associated with a specific `ContractVersion` because comments, redlines, and review tasks are tied to a particular negotiated draft.

An approval workflow is usually associated with a lifecycle gate such as draft approval, legal approval, or execution approval. It helps determine whether a transition may proceed, but it does not itself become the source of truth for contract lifecycle state.

An amendment workflow is commonly triggered when a new version of an existing contract is created. It coordinates drafting, review, and approval work for the amendment path while the parent `Contract` continues to own the broader agreement lifecycle.

A renewal workflow is commonly triggered by lifecycle dates or obligation deadlines. It helps coordinate reminders, reviews, and renewal decisions, while lifecycle transitions such as renew, expire, or terminate remain the responsibility of the Contract Lifecycle domain.

## 1) Draft Intake and Template-Driven Authoring

1. Contract request is submitted with contextual metadata.
2. Approved template and clause sets are selected under policy controls.
3. Draft version is generated and assigned ownership.
4. Draft enters controlled review lifecycle.

Capabilities involved:
- [Template / Merge Fields Document Generation](../../cookbook/capabilities/template-merge-fields-document-generation.md)
- [Dynamic Evaluation / Survey Engine](../../cookbook/capabilities/dynamic-evaluation-survey-engine.md)
- [Custom Fields / Extensible Attributes](../../cookbook/capabilities/custom-fields-extensible-attributes.md)
- [Audit Log + Provenance](../../cookbook/capabilities/audit-log-provenance.md)

## 2) Review, Negotiation, and Redline Governance

1. Review participants are assigned based on policy and risk category.
2. Clause-level changes are proposed and tracked as versioned updates.
3. Negotiation rounds continue until acceptance criteria are satisfied.
4. Approved draft advances to execution readiness checks.

Capabilities involved:
- [Rules Engine / Decisioning](../../cookbook/capabilities/rules-engine-decisioning.md)
- [Approval Workflows / Human-In-The-Loop](../../cookbook/capabilities/approval-workflows-human-in-the-loop.md)
- [Query Filtering](../../cookbook/capabilities/query-filtering.md)
- [Saved Views](../../cookbook/capabilities/saved-views.md)
- [Search Index](../../cookbook/capabilities/search-index.md)
- [Audit Log + Provenance](../../cookbook/capabilities/audit-log-provenance.md)

## 3) Approval and Execution Control

1. Execution preconditions trigger final approval routing.
2. Required approvers render decision outcomes with rationale.
3. Approved contracts proceed to signature and execution capture.
4. Execution evidence is persisted with immutable lineage.

Capabilities involved:
- [Approval Workflows / Human-In-The-Loop](../../cookbook/capabilities/approval-workflows-human-in-the-loop.md)
- [Notification Preferences and Routing](../../cookbook/capabilities/notification-preferences-routing.md)
- [Notification / Messaging System](../../cookbook/capabilities/notification-messaging-system.md)
- [Audit Log + Provenance](../../cookbook/capabilities/audit-log-provenance.md)

## 4) Obligation Tracking and Deadline Notifications

1. Executed terms generate obligation schedules.
2. Deadlines are monitored and routed to accountable owners.
3. Completion evidence is recorded against obligation milestones.
4. Overdue paths trigger escalation workflows.

Capabilities involved:
- [Query Filtering](../../cookbook/capabilities/query-filtering.md)
- [Saved Views](../../cookbook/capabilities/saved-views.md)
- [Search Index](../../cookbook/capabilities/search-index.md)
- [Notification Preferences and Routing](../../cookbook/capabilities/notification-preferences-routing.md)
- [Notification / Messaging System](../../cookbook/capabilities/notification-messaging-system.md)
- [Audit Log + Provenance](../../cookbook/capabilities/audit-log-provenance.md)

## 5) Renewal, Amendment, and Export Synchronization

1. Renewal windows and amendment triggers are evaluated by policy.
2. Lifecycle branch routes to renew, amend, or terminate actions.
3. Downstream exports and integration updates execute idempotently.
4. Reconciliation confirms lifecycle parity across systems.

Capabilities involved:
- [Import / Export Pipelines](../../cookbook/capabilities/import-export-pipelines.md)
- [Idempotency + Outbox + Retries + DLQ](../../cookbook/capabilities/idempotency-outbox-retries-dlq.md)
- [Rules Engine / Decisioning](../../cookbook/capabilities/rules-engine-decisioning.md)
- [Audit Log + Provenance](../../cookbook/capabilities/audit-log-provenance.md)