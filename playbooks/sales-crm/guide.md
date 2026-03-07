---
playbook: Sales CRM System
archetype: crm
required-capabilities:
  - search-filters-saved-views
  - rules-engine-decisioning
  - notification-messaging-system
  - audit-log-provenance
  - approval-workflows-human-in-the-loop
optional-capabilities:
  - template-merge-fields-document-generation
  - import-export-pipelines
  - custom-fields-extensible-attributes
patterns:
  - discoverability-search-queryability
  - workflow-stateful-progression
  - policy-driven-behavior
  - auditability-traceability
---

# Sales CRM Playbook

## Problem Context

Sales CRM systems coordinate lead management, opportunity progression, and account lifecycle management to improve conversion, forecast quality, and collaboration across revenue teams.

## Archetype

Primary archetype:
- [CRM](../../cookbook-v1/archetypes/crm.md)

Related archetypes:
- [Workflow / BPM System](../../cookbook-v1/archetypes/workflow-bpm-system.md)
- [Case / Ticket System](../../cookbook-v1/archetypes/case-ticket-system.md)

## Foundational Patterns

- [Discoverability (Search & Queryability)](../../cookbook-v1/foundational-patterns/discoverability-search-queryability.md)
- [Workflow / Stateful Progression](../../cookbook-v1/foundational-patterns/workflow-stateful-progression.md)
- [Policy-Driven Behavior (Rules / Decisioning)](../../cookbook-v1/foundational-patterns/policy-driven-behavior.md)
- [Auditability / Traceability](../../cookbook-v1/foundational-patterns/auditability-traceability.md)

## Required Capabilities

- [Search / Filters / Saved Views](../../cookbook-v1/capabilities/search-filters-saved-views.md)
- [Rules Engine / Decisioning](../../cookbook-v1/capabilities/rules-engine-decisioning.md)
- [Notification / Messaging System](../../cookbook-v1/capabilities/notification-messaging-system.md)
- [Audit Log + Provenance](../../cookbook-v1/capabilities/audit-log-provenance.md)
- [Approval Workflows / Human-In-The-Loop](../../cookbook-v1/capabilities/approval-workflows-human-in-the-loop.md)

## Reference Architecture

Use [system-context](diagrams/system-context.mmd), [container-view](diagrams/container-view.mmd), and [lifecycle-flow](diagrams/lifecycle-flow.mmd).

## System Evolution

Phase 1: account/contact baseline  
Phase 2: lead-to-opportunity workflow  
Phase 3: quote and approval controls  
Phase 4: billing and marketing integrations  
Phase 5: advanced revenue analytics

## Failure Modes

Risks include stage drift, duplicate leads, stale integration data, and weak ownership controls. See [failure-modes.md](failure-modes.md).
