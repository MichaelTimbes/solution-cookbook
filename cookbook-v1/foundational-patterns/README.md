# Foundational Patterns

Foundational patterns are the conceptual forces that explain why capabilities and archetypes recur across enterprise systems.

They are not implementation modules. They describe architectural pressure and design intent.

## How to use this layer

- Start from a pattern when you need to explain *why* a capability exists.
- Follow links from pattern → capability for implementation depth.
- Follow links from pattern → archetype to see where it applies in system shapes.
- Use the executive tri-map for fast scanning: [pattern-capability-archetype-tri-map.md](../pattern-capability-archetype-tri-map.md)

## Pattern index

| Pattern | Focus | Typical capabilities | Common archetypes |
|---|---|---|---|
| [Identity & Access Control](identity-access-control.md) | Trust boundaries and authorization | [Notification / Messaging System](../capabilities/notification-messaging-system.md), [Audit Log + Provenance](../capabilities/audit-log-provenance.md) | [CIAM](../archetypes/identity-access-ciam.md), [CRM](../archetypes/crm.md), [Case / Ticket](../archetypes/case-ticket-system.md) |
| [Auditability / Traceability](auditability-traceability.md) | Accountability and forensic reconstruction | [Audit Log + Provenance](../capabilities/audit-log-provenance.md), [Idempotency + Outbox + Retries + DLQ](../capabilities/idempotency-outbox-retries-dlq.md) | [DMS](../archetypes/document-management-system.md), [Billing](../archetypes/payments-billing.md), [CIAM](../archetypes/identity-access-ciam.md) |
| [Extensibility](extensibility.md) | Evolving domain shape safely | [Custom Fields / Extensible Attributes](../capabilities/custom-fields-extensible-attributes.md), [Rules Engine / Decisioning](../capabilities/rules-engine-decisioning.md) | [CRM](../archetypes/crm.md), [Inventory / Catalog](../archetypes/inventory-catalog.md), [CMS](../archetypes/cms-wiki-kb.md) |
| [Discoverability (Search & Queryability)](discoverability-search-queryability.md) | Fast, safe information retrieval | [Search / Filters / Saved Views](../capabilities/search-filters-saved-views.md), [Import / Export Pipelines](../capabilities/import-export-pipelines.md) | [Analytics](../archetypes/analytics-portal.md), [Case / Ticket](../archetypes/case-ticket-system.md), [DMS](../archetypes/document-management-system.md) |
| [Workflow / Stateful Progression](workflow-stateful-progression.md) | Durable business process evolution | [Approval Workflows / Human-In-The-Loop](../capabilities/approval-workflows-human-in-the-loop.md), [Rules Engine / Decisioning](../capabilities/rules-engine-decisioning.md) | [Workflow / BPM](../archetypes/workflow-bpm-system.md), [Ticketing](../archetypes/case-ticket-system.md), [Billing](../archetypes/payments-billing.md) |
| [Policy-Driven Behavior (Rules / Decisioning)](policy-driven-behavior.md) | Externalized business logic | [Rules Engine / Decisioning](../capabilities/rules-engine-decisioning.md), [Dynamic Evaluation / Survey Engine](../capabilities/dynamic-evaluation-survey-engine.md) | [Workflow / BPM](../archetypes/workflow-bpm-system.md), [CIAM](../archetypes/identity-access-ciam.md), [Inventory](../archetypes/inventory-catalog.md) |
| [Messaging & Notifications](messaging-notifications.md) | Event-to-human/system communication | [Notification / Messaging System](../capabilities/notification-messaging-system.md), [Notification Preferences and Routing](../capabilities/notification-preferences-routing.md) | [Scheduling](../archetypes/scheduling-rostering.md), [Ticketing](../archetypes/case-ticket-system.md), [Billing](../archetypes/payments-billing.md) |
| [Reliability Under Retry (Idempotency / Outbox)](reliability-under-retry.md) | Correctness under duplication and failure | [Idempotency + Outbox + Retries + DLQ](../capabilities/idempotency-outbox-retries-dlq.md), [Notification / Messaging System](../capabilities/notification-messaging-system.md) | [Billing](../archetypes/payments-billing.md), [Workflow](../archetypes/workflow-bpm-system.md), [Inventory](../archetypes/inventory-catalog.md) |
| [Data Movement (Import / Export)](data-movement.md) | Controlled boundary crossing of data | [Import / Export Pipelines](../capabilities/import-export-pipelines.md), [Audit Log + Provenance](../capabilities/audit-log-provenance.md) | [CRM](../archetypes/crm.md), [DMS](../archetypes/document-management-system.md), [Inventory](../archetypes/inventory-catalog.md) |
| [Human Approval / Human-In-The-Loop](human-approval-human-in-the-loop.md) | Explicit human control in critical paths | [Approval Workflows / Human-In-The-Loop](../capabilities/approval-workflows-human-in-the-loop.md), [Rules Engine / Decisioning](../capabilities/rules-engine-decisioning.md) | [Workflow](../archetypes/workflow-bpm-system.md), [Case / Ticket](../archetypes/case-ticket-system.md), [Billing](../archetypes/payments-billing.md) |
| [Generated Artifacts (Document / Template Generation)](generated-artifacts-document-template-generation.md) | Repeatable output generation from domain data | [Template / Merge Fields Document Generation](../capabilities/template-merge-fields-document-generation.md), [Import / Export Pipelines](../capabilities/import-export-pipelines.md) | [CMS](../archetypes/cms-wiki-kb.md), [DMS](../archetypes/document-management-system.md), [CRM](../archetypes/crm.md) |
| [Operational Visibility (Observability)](operational-visibility-observability.md) | Understanding behavior in production | [Audit Log + Provenance](../capabilities/audit-log-provenance.md), [Notification / Messaging System](../capabilities/notification-messaging-system.md), [Idempotency + Outbox + Retries + DLQ](../capabilities/idempotency-outbox-retries-dlq.md) | [Analytics](../archetypes/analytics-portal.md), [Workflow](../archetypes/workflow-bpm-system.md), [CIAM](../archetypes/identity-access-ciam.md) |

