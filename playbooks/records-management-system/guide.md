---
playbook: Records Management System
archetype: document-management-system
required-capabilities:
  - audit-log-provenance
  - search-filters-saved-views
  - approval-workflows-human-in-the-loop
  - rules-engine-decisioning
  - import-export-pipelines
optional-capabilities:
  - notification-messaging-system
  - idempotency-outbox-retries-dlq
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
- [Document Management System](../../cookbook-v1/archetypes/document-management-system.md)

Related archetypes:
- [Workflow / BPM System](../../cookbook-v1/archetypes/workflow-bpm-system.md)
- [Case / Ticket System](../../cookbook-v1/archetypes/case-ticket-system.md)

## Foundational Patterns

- [Auditability / Traceability](../../cookbook-v1/foundational-patterns/auditability-traceability.md)
- [Data Movement (Import / Export)](../../cookbook-v1/foundational-patterns/data-movement.md)
- [Policy-Driven Behavior (Rules / Decisioning)](../../cookbook-v1/foundational-patterns/policy-driven-behavior.md)
- [Workflow / Stateful Progression](../../cookbook-v1/foundational-patterns/workflow-stateful-progression.md)

## Required Capabilities

- [Audit Log + Provenance](../../cookbook-v1/capabilities/audit-log-provenance.md)
- [Search / Filters / Saved Views](../../cookbook-v1/capabilities/search-filters-saved-views.md)
- [Approval Workflows / Human-In-The-Loop](../../cookbook-v1/capabilities/approval-workflows-human-in-the-loop.md)
- [Rules Engine / Decisioning](../../cookbook-v1/capabilities/rules-engine-decisioning.md)
- [Import / Export Pipelines](../../cookbook-v1/capabilities/import-export-pipelines.md)

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
