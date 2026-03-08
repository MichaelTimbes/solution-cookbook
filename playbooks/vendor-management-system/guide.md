---
playbook: Vendor Management System
archetype: crm
required-capabilities:
  - human-communication
- query-filtering
- saved-views
- search-index
  - rules-engine-decisioning
  - approval-workflows-human-in-the-loop
  - audit-log-provenance
  - import-export-pipelines
optional-capabilities:
  - template-merge-fields-document-generation
patterns:
  - policy-driven-behavior
  - identity-access-control
  - auditability-traceability
  - data-movement
---

# Vendor Management System Playbook

## Problem Context

Vendor management systems manage vendor onboarding, qualification, performance review, and risk/compliance checks. They support procurement governance and supplier lifecycle visibility.

## Archetype

Primary archetype:
- [CRM](../../cookbook/archetypes/crm.md)

Related archetypes:
- [Workflow / BPM System](../../cookbook/archetypes/workflow-bpm-system.md)
- [Identity / Access (CIAM)](../../cookbook/archetypes/identity-access-ciam.md)

## Foundational Patterns

- [Policy-Driven Behavior (Rules / Decisioning)](../../cookbook/foundational-patterns/policy-driven-behavior.md)
- [Identity & Access Control](../../cookbook/foundational-patterns/identity-access-control.md)
- [Human Communication & Coordination](../../cookbook/foundational-patterns/human-communication-coordination.md)
- [Auditability / Traceability](../../cookbook/foundational-patterns/auditability-traceability.md)
- [Data Movement (Import / Export)](../../cookbook/foundational-patterns/data-movement.md)

## Required Capabilities
- [Query Filtering](../../cookbook/capabilities/query-filtering.md)
- [Saved Views](../../cookbook/capabilities/saved-views.md)
- [Search Index](../../cookbook/capabilities/search-index.md)
- [Human Communication](../../cookbook/capabilities/human-communication.md)
- [Rules Engine / Decisioning](../../cookbook/capabilities/rules-engine-decisioning.md)
- [Approval Workflows / Human-In-The-Loop](../../cookbook/capabilities/approval-workflows-human-in-the-loop.md)
- [Audit Log + Provenance](../../cookbook/capabilities/audit-log-provenance.md)
- [Import / Export Pipelines](../../cookbook/capabilities/import-export-pipelines.md)

## Reference Architecture

Architecture centers on vendor profile service, risk/compliance scoring, onboarding workflow, and procurement integration boundaries.

## System Evolution

Phase 1: vendor registry and onboarding  
Phase 2: qualification and scoring rules  
Phase 3: approval workflow and policy controls  
Phase 4: ERP/procurement integration  
Phase 5: supplier performance intelligence

## Failure Modes

Risks include incomplete onboarding evidence, policy bypasses, and stale vendor risk data. See [failure-modes.md](failure-modes.md).
