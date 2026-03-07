# Archetype ↔ Capability Cross-Link Matrix

This matrix maps each Level 1 archetype page to the Level 2 capabilities currently listed in its **Embedded capabilities** section.

## Capability key

- **AWH**: [Approval Workflows / Human-In-The-Loop](capabilities/approval-workflows-human-in-the-loop.md)
- **ALP**: [Audit Log and Provenance](capabilities/audit-log-provenance.md)
- **CFEA**: [Custom Fields / Extensible Attributes](capabilities/custom-fields-extensible-attributes.md)
- **DESE**: [Dynamic Evaluation / Survey Engine](capabilities/dynamic-evaluation-survey-engine.md)
- **IORD**: [Idempotency, Outbox, Retries, and DLQ](capabilities/idempotency-outbox-retries-dlq.md)
- **IEP**: [Import / Export Pipelines](capabilities/import-export-pipelines.md)
- **NPR**: [Notification Preferences and Routing](capabilities/notification-preferences-routing.md)
- **RED**: [Rules Engine / Decisioning](capabilities/rules-engine-decisioning.md)
- **SFV**: [Search / Filters / Saved Views](capabilities/search-filters-saved-views.md)
- **TMG**: [Template / Merge Fields Document Generation](capabilities/template-merge-fields-document-generation.md)

## Matrix

Legend: `✓` = listed in the archetype page’s Embedded capabilities.

| Archetype | AWH | ALP | CFEA | DESE | IORD | IEP | NPR | RED | SFV | TMG |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| [CRM](archetypes/crm.md) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| [Case / Ticket System](archetypes/case-ticket-system.md) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| [Payments / Billing](archetypes/payments-billing.md) | ✓ | ✓ | ✓ |  | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| [Document Management System](archetypes/document-management-system.md) | ✓ | ✓ | ✓ |  | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| [Workflow / BPM System](archetypes/workflow-bpm-system.md) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| [Inventory / Catalog](archetypes/inventory-catalog.md) | ✓ | ✓ | ✓ |  | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| [CMS / Wiki / Knowledge Base](archetypes/cms-wiki-kb.md) | ✓ | ✓ | ✓ |  |  | ✓ | ✓ | ✓ | ✓ | ✓ |
| [Scheduling / Rostering](archetypes/scheduling-rostering.md) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| [Analytics Portal](archetypes/analytics-portal.md) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| [Identity / Access (CIAM)](archetypes/identity-access-ciam.md) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |  |

## Reverse coverage view

| Capability | Coverage | Archetypes |
|---|---:|---|
| AWH | 10/10 | All archetypes |
| ALP | 10/10 | All archetypes |
| CFEA | 10/10 | All archetypes |
| DESE | 6/10 | CRM, Case / Ticket System, Workflow / BPM System, Scheduling / Rostering, Analytics Portal, Identity / Access (CIAM) |
| IORD | 9/10 | All except CMS / Wiki / Knowledge Base |
| IEP | 10/10 | All archetypes |
| NPR | 10/10 | All archetypes |
| RED | 10/10 | All archetypes |
| SFV | 10/10 | All archetypes |
| TMG | 6/10 | CRM, Case / Ticket System, Payments / Billing, Document Management System, Inventory / Catalog, CMS / Wiki / Knowledge Base |

## Suggested next normalization pass

- Consider adding [Dynamic Evaluation / Survey Engine](capabilities/dynamic-evaluation-survey-engine.md) to archetypes where dynamic intake is still optional (e.g., Document Management System, Inventory / Catalog).
- Consider adding [Template / Merge Fields Document Generation](capabilities/template-merge-fields-document-generation.md) to archetypes where generated outputs may become common later (e.g., Workflow / BPM System, Scheduling / Rostering).