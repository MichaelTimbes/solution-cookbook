# Archetype → Capability Matrix

This page is the primary navigation map for understanding how system archetypes are composed from reusable capabilities.

Use it to:
- start from an archetype and discover required capability building blocks,
- start from a capability and find all archetypes that depend on it,
- prioritize shared platform investments before archetype-specific implementation.

Legend: `✓` = currently mapped in archetype docs.

| Capability | CRM | Ticketing | Workflow | CMS | DMS | Billing | Scheduling | Inventory | CIAM | Analytics |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| [Custom Fields / Extensible Attributes](capabilities/custom-fields-extensible-attributes.md) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| [Audit Log and Provenance](capabilities/audit-log-provenance.md) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| [Approval Workflows / Human-In-The-Loop](capabilities/approval-workflows-human-in-the-loop.md) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| [Dynamic Evaluation / Survey Engine](capabilities/dynamic-evaluation-survey-engine.md) | ✓ | ✓ | ✓ |  |  |  | ✓ |  | ✓ | ✓ |
| [Idempotency, Outbox, Retries, and DLQ](capabilities/idempotency-outbox-retries-dlq.md) | ✓ | ✓ | ✓ |  | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| [Search / Filters / Saved Views](capabilities/search-filters-saved-views.md) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| [Rules Engine / Decisioning](capabilities/rules-engine-decisioning.md) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| [Notification / Messaging System](capabilities/notification-messaging-system.md) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| [Notification Preferences and Routing](capabilities/notification-preferences-routing.md) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| [Template / Merge Fields Document Generation](capabilities/template-merge-fields-document-generation.md) | ✓ | ✓ |  | ✓ | ✓ | ✓ |  | ✓ |  |  |
| [Import / Export Pipelines](capabilities/import-export-pipelines.md) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |

## Archetype file mapping

- CRM → [crm.md](archetypes/crm.md)
- Ticketing → [case-ticket-system.md](archetypes/case-ticket-system.md)
- Workflow → [workflow-bpm-system.md](archetypes/workflow-bpm-system.md)
- CMS → [cms-wiki-kb.md](archetypes/cms-wiki-kb.md)
- DMS → [document-management-system.md](archetypes/document-management-system.md)
- Billing → [payments-billing.md](archetypes/payments-billing.md)
- Scheduling → [scheduling-rostering.md](archetypes/scheduling-rostering.md)
- Inventory → [inventory-catalog.md](archetypes/inventory-catalog.md)
- CIAM → [identity-access-ciam.md](archetypes/identity-access-ciam.md)
- Analytics → [analytics-portal.md](archetypes/analytics-portal.md)

## High-value capability coverage check

Requested capabilities status:

1. Rules / Decision Engine → [present](capabilities/rules-engine-decisioning.md)
2. Notification / Messaging System → [new scaffold](capabilities/notification-messaging-system.md)
3. Template + Document Generation → [present](capabilities/template-merge-fields-document-generation.md)
4. Import / Export Pipelines → [present](capabilities/import-export-pipelines.md)
5. Search / Filters / Saved Views → [present](capabilities/search-filters-saved-views.md)

## Composition guidance

- Treat capabilities as shared platform modules and archetypes as curated assemblies.
- Prefer capability-level runbooks and observability baselines reused across archetypes.
- Keep archetype pages focused on domain shape and workflow intent; keep implementation depth in capability pages.
