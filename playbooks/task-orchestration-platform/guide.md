---
playbook: Task Orchestration Platform
archetype: workflow-bpm-system
required-capabilities:
  - rules-engine-decisioning
- query-filtering
- saved-views
- search-index
  - human-communication
  - notification-messaging-system
  - audit-log-provenance
  - idempotency-outbox-retries-dlq
optional-capabilities:
  - template-merge-fields-document-generation
patterns:
  - workflow-stateful-progression
  - reliability-under-retry
  - operational-visibility-observability
  - discoverability-search-queryability
---

# Task Orchestration Platform Playbook

## Problem Context

Task orchestration platforms coordinate distributed task execution across teams and systems with explicit dependencies, retries, and operational visibility.

## Archetype

Primary archetype:
- [Workflow / BPM System](../../cookbook/archetypes/workflow-bpm-system.md)

## Foundational Patterns

- [Workflow / Stateful Progression](../../cookbook/foundational-patterns/workflow-stateful-progression.md)
- [Reliability Under Retry (Idempotency / Outbox)](../../cookbook/foundational-patterns/reliability-under-retry.md)
- [Operational Visibility (Observability)](../../cookbook/foundational-patterns/operational-visibility-observability.md)
- [Discoverability (Search & Queryability)](../../cookbook/foundational-patterns/discoverability-search-queryability.md)
- [Human Communication & Coordination](../../cookbook/foundational-patterns/human-communication-coordination.md)

## Required Capabilities

- [Rules Engine / Decisioning](../../cookbook/capabilities/rules-engine-decisioning.md)
- [Query Filtering](../../cookbook/capabilities/query-filtering.md)
- [Saved Views](../../cookbook/capabilities/saved-views.md)
- [Search Index](../../cookbook/capabilities/search-index.md)
- [Human Communication](../../cookbook/capabilities/human-communication.md)
- [Notification / Messaging System](../../cookbook/capabilities/notification-messaging-system.md)
- [Audit Log + Provenance](../../cookbook/capabilities/audit-log-provenance.md)
- [Idempotency + Outbox + Retries + DLQ](../../cookbook/capabilities/idempotency-outbox-retries-dlq.md)
