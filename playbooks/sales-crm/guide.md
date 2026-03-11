---
playbook: Sales CRM
archetype: crm
required-capabilities:
  - query-filtering
  - saved-views
  - search-index
  - custom-fields-extensible-attributes
  - human-communication
  - approval-workflows-human-in-the-loop
  - dynamic-evaluation-survey-engine
  - notification-preferences-routing
  - notification-messaging-system
  - rules-engine-decisioning
  - audit-log-provenance
  - import-export-pipelines
  - idempotency-outbox-retries-dlq
optional-capabilities:
  - template-merge-fields-document-generation
patterns:
  - identity-access-control
  - auditability-traceability
  - discoverability-search-queryability
  - workflow-stateful-progression
  - policy-driven-behavior
  - operational-visibility-observability
---

# Sales CRM Playbook

## Problem Context

Sales CRM systems coordinate lead intake, account and contact management, opportunity progression, and pipeline governance. They provide consistent ownership, predictable stage movement, and auditable revenue process controls across sales teams.

Typical real-world examples include B2B sales operations, account executive organizations, and partner-assisted opportunity management environments.

## Archetype

Primary archetype:
- [CRM](../../cookbook/archetypes/crm.md)

Related archetypes:
- [Case / Ticket System](../../cookbook/archetypes/case-ticket-system.md)
- [Workflow / BPM System](../../cookbook/archetypes/workflow-bpm-system.md)
- [Document Management System](../../cookbook/archetypes/document-management-system.md)

Interaction model:
- Sales CRM owns lead-to-opportunity and account relationship progression.
- Case/Ticket systems provide post-sale service context.
- Workflow/BPM governs approvals and exception routing.
- Document management provides quote, proposal, and agreement artifact controls.

## Foundational Patterns

Key patterns shaping sales CRM architecture:
- [Identity & Access Control](../../cookbook/foundational-patterns/identity-access-control.md)
- [Auditability / Traceability](../../cookbook/foundational-patterns/auditability-traceability.md)
- [Discoverability (Search & Queryability)](../../cookbook/foundational-patterns/discoverability-search-queryability.md)
- [Workflow / Stateful Progression](../../cookbook/foundational-patterns/workflow-stateful-progression.md)
- [Human Communication & Coordination](../../cookbook/foundational-patterns/human-communication-coordination.md)
- [Policy-Driven Behavior (Rules / Decisioning)](../../cookbook/foundational-patterns/policy-driven-behavior.md)
- [Operational Visibility (Observability)](../../cookbook/foundational-patterns/operational-visibility-observability.md)

These patterns are essential because sales operations require controlled stage transitions, policy-aware approval checkpoints, and reliable activity lineage for forecast confidence.

## Required Capabilities

Core capability pages:
- [Query Filtering](../../cookbook/capabilities/query-filtering.md)
- [Saved Views](../../cookbook/capabilities/saved-views.md)
- [Search Index](../../cookbook/capabilities/search-index.md)
- [Custom Fields / Extensible Attributes](../../cookbook/capabilities/custom-fields-extensible-attributes.md)
- [Human Communication](../../cookbook/capabilities/human-communication.md)
- [Approval Workflows / Human-In-The-Loop](../../cookbook/capabilities/approval-workflows-human-in-the-loop.md)
- [Dynamic Evaluation / Survey Engine](../../cookbook/capabilities/dynamic-evaluation-survey-engine.md)
- [Notification Preferences and Routing](../../cookbook/capabilities/notification-preferences-routing.md)
- [Notification / Messaging System](../../cookbook/capabilities/notification-messaging-system.md)
- [Rules Engine / Decisioning](../../cookbook/capabilities/rules-engine-decisioning.md)
- [Import / Export Pipelines](../../cookbook/capabilities/import-export-pipelines.md)
- [Audit Log + Provenance](../../cookbook/capabilities/audit-log-provenance.md)
- [Idempotency + Outbox + Retries + DLQ](../../cookbook/capabilities/idempotency-outbox-retries-dlq.md)

How capabilities participate:
- Search and custom fields support segmentation and pipeline visibility.
- Rules and dynamic evaluation govern qualification, scoring, and assignment.
- Approval workflows enforce policy for discounts, stage overrides, and exceptions.
- Human communication capability anchors discussion threads, mentions, and handoff context directly on account and opportunity records.
- Notification and messaging coordinate rep, manager, and stakeholder communication.
- Audit, import/export, and idempotency preserve trustworthy CRM lifecycle history.

## Reference Architecture

Diagrams:
- [System context](diagrams/system-context.mmd)
- [Container view](diagrams/container-view.mmd)
- [Lifecycle flow](diagrams/lifecycle-flow.mmd)

High-level architecture:
- Intake boundaries accept lead and account interactions from forms, integrations, and APIs.
- Core CRM domain services manage leads, accounts, contacts, opportunities, and activities.
- A repository/core state store persists canonical relationship and stage state.
- Search/query services maintain fast pipeline and territory views.
- Workflow and orchestration services execute approval and stage-gating processes.
- Notification and messaging services route opportunity and task updates.
- Audit and provenance services maintain immutable sales process evidence.
- Integration boundaries coordinate downstream analytics and adjacent business systems.

## System Evolution

Phase 1: lead, account, and contact baseline  
Phase 2: opportunity lifecycle and forecasting alignment  
Phase 3: approval controls and governance hardening  
Phase 4: integration-aware synchronization and reliability controls  
Phase 5: observability and data quality optimization

As maturity increases, sales CRM systems evolve from basic record tracking toward governed pipeline orchestration with trusted lifecycle analytics.

## Failure Modes

Common architectural risks:
- duplicate or fragmented account/contact records degrading relationship trust
- inconsistent stage progression causing forecast distortion
- approval bypass paths for pricing or commitment exceptions
- notification drift causing missed follow-up and stale opportunity state
- integration replay creating duplicate activities and updates

See detailed analysis in [failure-modes.md](failure-modes.md).
