# Business Process Automation Workflows

## Core Workflow Set

## Typical Workflow Units

Workflows in this playbook usually represent bounded process units inside larger operational lifecycles rather than the entire business lifecycle itself.

- Process start workflow: intake validation, initial branching, and task creation.
- Integration workflow: external side-effect execution and callback handling.
- Recovery workflow: retry, compensation, and dead-letter resolution.

## 1) Model and Deploy Process Definition

1. Process definition is authored, reviewed, and versioned.
2. Deployment controls publish an immutable executable version.
3. Policy and branching rules are captured with the process definition.
4. New process instances reference the active deployment version.

Capabilities involved:
- [Rules Engine / Decisioning](../../cookbook/capabilities/rules-engine-decisioning.md)
- [Audit Log + Provenance](../../cookbook/capabilities/audit-log-provenance.md)

## 2) Start Process and Route Tasks

1. Start request enters the automation boundary with required context.
2. Execution engine initializes instance and task state.
3. Branching rules select path and owner or handler context.
4. Notifications and collaboration context are issued where relevant.

Capabilities involved:
- [Rules Engine / Decisioning](../../cookbook/capabilities/rules-engine-decisioning.md)
- [Human Communication](../../cookbook/capabilities/human-communication.md)
- [Notification / Messaging System](../../cookbook/capabilities/notification-messaging-system.md)
- [Audit Log + Provenance](../../cookbook/capabilities/audit-log-provenance.md)

## 3) Execute System Integrations

1. Process tasks trigger external side effects or export-oriented actions.
2. Integration task records capture request, delivery, and outcome context.
3. Idempotent handling prevents duplicate side effects under retries.
4. Canonical process state reflects integration success or exception paths.

Capabilities involved:
- [Import / Export Pipelines](../../cookbook/capabilities/import-export-pipelines.md)
- [Idempotency + Outbox + Retries + DLQ](../../cookbook/capabilities/idempotency-outbox-retries-dlq.md)
- [Audit Log + Provenance](../../cookbook/capabilities/audit-log-provenance.md)

## 4) Retry and Compensate Failures

1. Failed side effects enter retry-safe recovery handling.
2. Exhausted attempts move into dead-letter or compensation paths.
3. Operators or automation resolve exception states through bounded recovery units.
4. Recovery outcomes update process and operational visibility views.

Capabilities involved:
- [Idempotency + Outbox + Retries + DLQ](../../cookbook/capabilities/idempotency-outbox-retries-dlq.md)
- [Rules Engine / Decisioning](../../cookbook/capabilities/rules-engine-decisioning.md)
- [Notification / Messaging System](../../cookbook/capabilities/notification-messaging-system.md)
- [Audit Log + Provenance](../../cookbook/capabilities/audit-log-provenance.md)

## 5) Complete and Report Outcomes

1. Terminal process outcome is recorded in canonical execution state.
2. Reporting and export consumers receive outcome summaries where relevant.
3. Operational dashboards update throughput, backlog, and exception visibility.
4. Audit and observability views preserve full process lineage.

Capabilities involved:
- [Import / Export Pipelines](../../cookbook/capabilities/import-export-pipelines.md)
- [Notification / Messaging System](../../cookbook/capabilities/notification-messaging-system.md)
- [Audit Log + Provenance](../../cookbook/capabilities/audit-log-provenance.md)