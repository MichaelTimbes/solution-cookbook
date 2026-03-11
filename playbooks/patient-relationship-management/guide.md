---
playbook: Patient Relationship Management System
archetype: crm
required-capabilities:
  - human-communication
  - query-filtering
  - saved-views
  - search-index
  - notification-messaging-system
  - rules-engine-decisioning
  - audit-log-provenance
  - approval-workflows-human-in-the-loop
optional-capabilities:
  - template-merge-fields-document-generation
patterns:
  - identity-access-control
  - auditability-traceability
  - workflow-stateful-progression
  - discoverability-search-queryability
---

# Patient Relationship Management Playbook

## Problem Context

Patient relationship management systems coordinate patient engagement, care outreach, appointment follow-up, and communication history while enforcing privacy and consent policies.

## Archetype

Primary archetype:
- [CRM](../../cookbook/archetypes/crm.md)

Related archetypes:
- [Workflow / BPM System](../../cookbook/archetypes/workflow-bpm-system.md)
- [Identity / Access (CIAM)](../../cookbook/archetypes/identity-access-ciam.md)

## Foundational Patterns

- [Identity & Access Control](../../cookbook/foundational-patterns/identity-access-control.md)
- [Auditability / Traceability](../../cookbook/foundational-patterns/auditability-traceability.md)
- [Human Communication & Coordination](../../cookbook/foundational-patterns/human-communication-coordination.md)
- [Workflow / Stateful Progression](../../cookbook/foundational-patterns/workflow-stateful-progression.md)
- [Discoverability (Search & Queryability)](../../cookbook/foundational-patterns/discoverability-search-queryability.md)

## Required Capabilities
- [Query Filtering](../../cookbook/capabilities/query-filtering.md)
- [Saved Views](../../cookbook/capabilities/saved-views.md)
- [Search Index](../../cookbook/capabilities/search-index.md)
- [Human Communication](../../cookbook/capabilities/human-communication.md)
- [Notification / Messaging System](../../cookbook/capabilities/notification-messaging-system.md)
- [Rules Engine / Decisioning](../../cookbook/capabilities/rules-engine-decisioning.md)
- [Audit Log + Provenance](../../cookbook/capabilities/audit-log-provenance.md)
- [Approval Workflows / Human-In-The-Loop](../../cookbook/capabilities/approval-workflows-human-in-the-loop.md)

## Reference Architecture

Architecture focuses on patient profile lifecycle, communication preferences, outreach workflows, and policy-gated data access.

## System Evolution

Phase 1: patient profile and interaction timeline  
Phase 2: outreach and follow-up workflows  
Phase 3: policy-gated communication and consent  
Phase 4: care-system integration boundaries  
Phase 5: population engagement analytics

## Failure Modes

Risks include consent handling gaps, misrouted outreach, and unauthorized data access. See [failure-modes.md](failure-modes.md).
