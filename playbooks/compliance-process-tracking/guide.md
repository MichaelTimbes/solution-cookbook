---
playbook: Compliance Process Tracking System
archetype: workflow-bpm-system
required-capabilities:
  - approval-workflows-human-in-the-loop
  - human-communication
  - rules-engine-decisioning
  - audit-log-provenance
- query-filtering
- saved-views
- search-index
  - notification-messaging-system
optional-capabilities:
  - template-merge-fields-document-generation
patterns:
  - policy-driven-behavior
  - auditability-traceability
  - workflow-stateful-progression
  - operational-visibility-observability
---

# Compliance Process Tracking Playbook

## Problem Context

Compliance process tracking systems orchestrate policy checks, control attestations, remediation actions, and evidence-based closure across regulated workflows.

## Archetype

Primary archetype:
- [Workflow / BPM System](../../cookbook/archetypes/workflow-bpm-system.md)

Related archetypes:
- [Case / Ticket System](../../cookbook/archetypes/case-ticket-system.md)
- [Analytics Platform](../../cookbook/archetypes/analytics-platform.md)

## Foundational Patterns

- [Policy-Driven Behavior (Rules / Decisioning)](../../cookbook/foundational-patterns/policy-driven-behavior.md)
- [Auditability / Traceability](../../cookbook/foundational-patterns/auditability-traceability.md)
- [Workflow / Stateful Progression](../../cookbook/foundational-patterns/workflow-stateful-progression.md)
- [Operational Visibility (Observability)](../../cookbook/foundational-patterns/operational-visibility-observability.md)
- [Human Communication & Coordination](../../cookbook/foundational-patterns/human-communication-coordination.md)

## Required Capabilities

- [Approval Workflows / Human-In-The-Loop](../../cookbook/capabilities/approval-workflows-human-in-the-loop.md)
- [Human Communication](../../cookbook/capabilities/human-communication.md)
- [Rules Engine / Decisioning](../../cookbook/capabilities/rules-engine-decisioning.md)
- [Audit Log + Provenance](../../cookbook/capabilities/audit-log-provenance.md)
- [Query Filtering](../../cookbook/capabilities/query-filtering.md)
- [Saved Views](../../cookbook/capabilities/saved-views.md)
- [Search Index](../../cookbook/capabilities/search-index.md)
- [Notification / Messaging System](../../cookbook/capabilities/notification-messaging-system.md)
