---
playbook: Legal Case Management System
archetype: case-ticket-system
required-capabilities:
  - human-communication
  - approval-workflows-human-in-the-loop
  - audit-log-provenance
  - query-filtering
  - saved-views
  - search-index
  - rules-engine-decisioning
  - notification-messaging-system
optional-capabilities:
  - template-merge-fields-document-generation
patterns:
  - auditability-traceability
  - identity-access-control
  - workflow-stateful-progression
  - policy-driven-behavior
---

# Legal Case Management Playbook

## Problem Context

Legal case management systems coordinate intake, evidence handling, legal review, approvals, and closure for legal matters. They prioritize chain-of-custody, controlled access, and defensible audit history.

## Archetype

Primary archetype:
- [Case / Ticket System](../../cookbook/archetypes/case-ticket-system.md)

Related archetypes:
- [Document Management System](../../cookbook/archetypes/document-management-system.md)
- [Workflow / BPM System](../../cookbook/archetypes/workflow-bpm-system.md)

## Foundational Patterns

- [Auditability / Traceability](../../cookbook/foundational-patterns/auditability-traceability.md)
- [Identity & Access Control](../../cookbook/foundational-patterns/identity-access-control.md)
- [Human Communication & Coordination](../../cookbook/foundational-patterns/human-communication-coordination.md)
- [Workflow / Stateful Progression](../../cookbook/foundational-patterns/workflow-stateful-progression.md)
- [Policy-Driven Behavior (Rules / Decisioning)](../../cookbook/foundational-patterns/policy-driven-behavior.md)

## Required Capabilities

- [Approval Workflows / Human-In-The-Loop](../../cookbook/capabilities/approval-workflows-human-in-the-loop.md)
- [Human Communication](../../cookbook/capabilities/human-communication.md)
- [Audit Log + Provenance](../../cookbook/capabilities/audit-log-provenance.md)
- [Query Filtering](../../cookbook/capabilities/query-filtering.md)
- [Saved Views](../../cookbook/capabilities/saved-views.md)
- [Search Index](../../cookbook/capabilities/search-index.md)
- [Rules Engine / Decisioning](../../cookbook/capabilities/rules-engine-decisioning.md)
- [Notification / Messaging System](../../cookbook/capabilities/notification-messaging-system.md)

## Reference Architecture

See [system-context](diagrams/system-context.mmd), [container-view](diagrams/container-view.mmd), and [lifecycle-flow](diagrams/lifecycle-flow.mmd).

## System Evolution

Phase 1: matter intake and assignment  
Phase 2: evidence and document linkage  
Phase 3: review and approval controls  
Phase 4: external counsel and regulator integration  
Phase 5: advanced governance and legal analytics

## Failure Modes

Risks include evidence lineage gaps, unauthorized access, policy drift in approvals, and incomplete closure records. See [failure-modes.md](failure-modes.md).
