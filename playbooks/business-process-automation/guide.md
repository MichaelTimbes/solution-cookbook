---
playbook: Business Process Automation System
archetype: workflow-bpm-system
required-capabilities:
  - rules-engine-decisioning
  - human-communication-coordination
  - idempotency-outbox-retries-dlq
  - notification-messaging-system
  - audit-log-provenance
  - import-export-pipelines
optional-capabilities:
  - template-merge-fields-document-generation
patterns:
  - workflow-stateful-progression
  - policy-driven-behavior
  - reliability-under-retry
  - operational-visibility-observability
---

# Business Process Automation Playbook

## Problem Context

Business process automation systems orchestrate repeatable multi-step processes with deterministic state, policy-based branching, and integration side effects.

## Archetype

Primary archetype:
- [Workflow / BPM System](../../cookbook/archetypes/workflow-bpm-system.md)

## Foundational Patterns

- [Workflow / Stateful Progression](../../cookbook/foundational-patterns/workflow-stateful-progression.md)
- [Policy-Driven Behavior (Rules / Decisioning)](../../cookbook/foundational-patterns/policy-driven-behavior.md)
- [Human Communication & Coordination](../../cookbook/foundational-patterns/human-communication-coordination.md)
- [Reliability Under Retry (Idempotency / Outbox)](../../cookbook/foundational-patterns/reliability-under-retry.md)
- [Operational Visibility (Observability)](../../cookbook/foundational-patterns/operational-visibility-observability.md)

## Required Capabilities

- [Rules Engine / Decisioning](../../cookbook/capabilities/rules-engine-decisioning.md)
- [Human Communication / Collaboration Layer](../../cookbook/capabilities/human-communication-coordination.md)
- [Idempotency + Outbox + Retries + DLQ](../../cookbook/capabilities/idempotency-outbox-retries-dlq.md)
- [Notification / Messaging System](../../cookbook/capabilities/notification-messaging-system.md)
- [Audit Log + Provenance](../../cookbook/capabilities/audit-log-provenance.md)
- [Import / Export Pipelines](../../cookbook/capabilities/import-export-pipelines.md)

## System Evolution

Phase 1: modeled process automation  
Phase 2: branching and policy controls  
Phase 3: retry-safe integrations  
Phase 4: scaling and operational controls  
Phase 5: optimization analytics
