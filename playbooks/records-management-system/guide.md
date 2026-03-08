---
playbook: Records Management System
archetype: document-management-system
required-capabilities:
  - human-communication
  - audit-log-provenance
- query-filtering
- saved-views
- search-index
  - approval-workflows-human-in-the-loop
  - rules-engine-decisioning
  - import-export-pipelines
optional-capabilities:
  - template-merge-fields-document-generation
patterns:
  - auditability-traceability
  - data-movement
  - policy-driven-behavior
  - workflow-stateful-progression
---

# Records Management System Playbook

## Problem Context

Records management systems govern retention, legal hold, classification, and disposition of official records across regulatory and organizational policies.

## Archetype

Primary archetype:
- [Document Management System](../../cookbook/archetypes/document-management-system.md)

Related archetypes:
- [Workflow / BPM System](../../cookbook/archetypes/workflow-bpm-system.md)
- [Case / Ticket System](../../cookbook/archetypes/case-ticket-system.md)

## Foundational Patterns

- [Auditability / Traceability](../../cookbook/foundational-patterns/auditability-traceability.md)
- [Human Communication & Coordination](../../cookbook/foundational-patterns/human-communication-coordination.md)
- [Data Movement (Import / Export)](../../cookbook/foundational-patterns/data-movement.md)
- [Policy-Driven Behavior (Rules / Decisioning)](../../cookbook/foundational-patterns/policy-driven-behavior.md)
- [Workflow / Stateful Progression](../../cookbook/foundational-patterns/workflow-stateful-progression.md)

## Required Capabilities

- [Audit Log + Provenance](../../cookbook/capabilities/audit-log-provenance.md)
- [Human Communication](../../cookbook/capabilities/human-communication.md)
- [Query Filtering](../../cookbook/capabilities/query-filtering.md)
- [Saved Views](../../cookbook/capabilities/saved-views.md)
- [Search Index](../../cookbook/capabilities/search-index.md)
- [Approval Workflows / Human-In-The-Loop](../../cookbook/capabilities/approval-workflows-human-in-the-loop.md)
- [Rules Engine / Decisioning](../../cookbook/capabilities/rules-engine-decisioning.md)
- [Import / Export Pipelines](../../cookbook/capabilities/import-export-pipelines.md)

## Reference Architecture

Architecture emphasizes retention policy service, legal hold workflow, immutable audit, and records disposition controls.

## System Evolution

Phase 1: records classification and retention assignment  
Phase 2: legal hold and exception workflows  
Phase 3: disposition approvals and reporting  
Phase 4: cross-system records ingestion/export  
Phase 5: policy optimization and governance analytics

## Failure Modes

Risks include premature deletion, hold violations, and incomplete disposition evidence. See [failure-modes.md](failure-modes.md).
