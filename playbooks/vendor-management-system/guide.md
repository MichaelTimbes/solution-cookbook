---
playbook: Vendor Management System
archetype: crm
required-capabilities:
  - search-filters-saved-views
  - rules-engine-decisioning
  - approval-workflows-human-in-the-loop
  - audit-log-provenance
  - import-export-pipelines
optional-capabilities:
  - notification-messaging-system
  - custom-fields-extensible-attributes
  - idempotency-outbox-retries-dlq
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
- [CRM](../../cookbook-v1/archetypes/crm.md)

Related archetypes:
- [Workflow / BPM System](../../cookbook-v1/archetypes/workflow-bpm-system.md)
- [Identity / Access (CIAM)](../../cookbook-v1/archetypes/identity-access-ciam.md)

## Foundational Patterns

- [Policy-Driven Behavior (Rules / Decisioning)](../../cookbook-v1/foundational-patterns/policy-driven-behavior.md)
- [Identity & Access Control](../../cookbook-v1/foundational-patterns/identity-access-control.md)
- [Auditability / Traceability](../../cookbook-v1/foundational-patterns/auditability-traceability.md)
- [Data Movement (Import / Export)](../../cookbook-v1/foundational-patterns/data-movement.md)

## Required Capabilities

- [Search / Filters / Saved Views](../../cookbook-v1/capabilities/search-filters-saved-views.md)
- [Rules Engine / Decisioning](../../cookbook-v1/capabilities/rules-engine-decisioning.md)
- [Approval Workflows / Human-In-The-Loop](../../cookbook-v1/capabilities/approval-workflows-human-in-the-loop.md)
- [Audit Log + Provenance](../../cookbook-v1/capabilities/audit-log-provenance.md)
- [Import / Export Pipelines](../../cookbook-v1/capabilities/import-export-pipelines.md)

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
