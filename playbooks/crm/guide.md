---
playbook: Customer Relationship Management System
archetype: crm
required-capabilities:
  - search-filters-saved-views
  - audit-log-provenance
  - approval-workflows-human-in-the-loop
  - notification-messaging-system
  - import-export-pipelines
  - rules-engine-decisioning
optional-capabilities:
  - custom-fields-extensible-attributes
  - dynamic-evaluation-survey-engine
  - notification-preferences-routing
  - template-merge-fields-document-generation
  - idempotency-outbox-retries-dlq
patterns:
  - identity-access-control
  - auditability-traceability
  - discoverability-search-queryability
  - workflow-stateful-progression
  - policy-driven-behavior
  - operational-visibility-observability
---

# Customer Relationship Management Playbook

## Problem Context

Customer Relationship Management (CRM) systems solve the coordination problem between sales, service, and account teams by centralizing customer records, interactions, and pipeline progression. Without a CRM system, teams often operate on fragmented data, producing inconsistent handoffs, unclear ownership, and low visibility into customer history.

Typical real-world examples include:
- lead and opportunity management for sales organizations
- account and contact lifecycle management
- service-case collaboration tied to customer context
- quote and handoff processes to downstream order or billing systems

## Archetype

Primary archetype:
- [CRM](../../cookbook-v1/archetypes/crm.md)

Related archetypes:
- [Case / Ticket System](../../cookbook-v1/archetypes/case-ticket-system.md)
- [Workflow / BPM System](../../cookbook-v1/archetypes/workflow-bpm-system.md)
- [Analytics Portal](../../cookbook-v1/archetypes/analytics-portal.md)

Interaction model:
- CRM owns customer-facing pipeline and relationship state.
- Case/Ticket systems manage service interactions and escalation flows, linked to account context.
- Workflow/BPM governs approval and transition logic for sensitive changes.
- Analytics portals consume CRM data for forecasting, conversion analysis, and operational reporting.

## Foundational Patterns

Key patterns shaping CRM architecture:
- [Identity & Access Control](../../cookbook-v1/foundational-patterns/identity-access-control.md)
- [Auditability / Traceability](../../cookbook-v1/foundational-patterns/auditability-traceability.md)
- [Discoverability (Search & Queryability)](../../cookbook-v1/foundational-patterns/discoverability-search-queryability.md)
- [Workflow / Stateful Progression](../../cookbook-v1/foundational-patterns/workflow-stateful-progression.md)
- [Policy-Driven Behavior (Rules / Decisioning)](../../cookbook-v1/foundational-patterns/policy-driven-behavior.md)
- [Operational Visibility (Observability)](../../cookbook-v1/foundational-patterns/operational-visibility-observability.md)

These patterns matter because CRM platforms must enforce trust boundaries, preserve a full change history, support fast record discovery, control state transitions, execute business rules consistently, and remain observable across integrations.

## Required Capabilities

Core capability pages:
- [Custom Fields / Extensible Attributes](../../cookbook-v1/capabilities/custom-fields-extensible-attributes.md)
- [Dynamic Evaluation / Survey Engine](../../cookbook-v1/capabilities/dynamic-evaluation-survey-engine.md)
- [Template / Merge Fields Document Generation](../../cookbook-v1/capabilities/template-merge-fields-document-generation.md)
- [Search / Filters / Saved Views](../../cookbook-v1/capabilities/search-filters-saved-views.md)
- [Approval Workflows / Human-In-The-Loop](../../cookbook-v1/capabilities/approval-workflows-human-in-the-loop.md)
- [Notification Preferences and Routing](../../cookbook-v1/capabilities/notification-preferences-routing.md)
- [Notification / Messaging System](../../cookbook-v1/capabilities/notification-messaging-system.md)
- [Import / Export Pipelines](../../cookbook-v1/capabilities/import-export-pipelines.md)
- [Audit Log + Provenance](../../cookbook-v1/capabilities/audit-log-provenance.md)
- [Rules Engine / Decisioning](../../cookbook-v1/capabilities/rules-engine-decisioning.md)
- [Idempotency + Outbox + Retries + DLQ](../../cookbook-v1/capabilities/idempotency-outbox-retries-dlq.md)

How capabilities participate:
- Search and saved views support daily pipeline operations and segmentation.
- Audit and provenance preserve accountability for ownership, stage, and policy changes.
- Rules and workflow capabilities enforce allowed transitions and approval gates.
- Messaging capabilities coordinate assignments, escalations, and reminders.
- Import/export and idempotency support safe integration with external systems.
- Extensibility and dynamic evaluation support evolving business models and qualification logic.

## Reference Architecture

Diagrams:
- [System context](diagrams/system-context.mmd)
- [Container view](diagrams/container-view.mmd)
- [Lifecycle flow](diagrams/lifecycle-flow.mmd)

High-level architecture:
- An intake boundary accepts lead, account, and activity inputs from users and integrations.
- Core domain services manage account, contact, lead, opportunity, case, and activity lifecycles.
- A state store persists authoritative records and ownership assignments.
- Search/query services maintain discoverability through indexed views.
- Workflow and rules services govern transitions, approvals, and escalation conditions.
- Notification and messaging services deliver operational events.
- Audit and observability services capture immutable change evidence and operational signals.
- Integration boundaries provide controlled import/export and synchronization.

## System Evolution

Phase 1: central account, contact, and lead repository  
Phase 2: structured pipeline stages and search/saved views  
Phase 3: rules-driven workflow, approvals, and notifications  
Phase 4: deeper integrations, idempotent synchronization, and enrichment  
Phase 5: advanced governance, traceability, and operational optimization

As maturity increases, systems typically move from simple record tracking toward policy-governed, integration-aware, and observable operation.

## Failure Modes

Common architectural risks:
- duplicate records from weak matching and merge strategy
- stage drift from ad-hoc state updates
- over-broad access to sensitive customer data
- notification overload from poorly designed automation
- stale analytics due to integration lag

See detailed analysis in [failure-modes.md](failure-modes.md).
