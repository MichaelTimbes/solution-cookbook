# Business Process Automation Architecture

## Logical Components

- Process definition service: manages process models and versioned automation logic.
- Execution engine: runs process instances and coordinates state progression.
- Policy decision service: evaluates branching and exception rules.
- Integration task service: handles side effects, external calls, and export-oriented work.
- Retry and dead-letter handling service: manages replay-safe failure recovery.
- Event and notification service: coordinates process signals and participant notifications.
- Audit and observability service: records immutable process evidence and operational visibility signals.

## Workflow / Lifecycle Handshake

- Workflow commonly manages the bounded process progression itself, while lifecycle state remains anchored in canonical process-instance and task records.
- Execution services typically own canonical mutation of process instance, task, transition, and recovery state.
- Workflow completion may trigger downstream commands or integrations, but workflow step completion does not bypass authoritative persisted process state.

## Read Model Strategy

- Canonical reads usually come from the primary process definition, process instance, task, transition, and recovery records.
- Operational worklists, backlog views, and exception dashboards often read from projection or read-model tables tuned for process operations.
- Search index reads are typically used for process discovery and operational retrieval where supported.
- Reporting and optimization summaries are often served from reporting projections rather than mutable execution tables.

## Typical Modular-Monolith Module Boundaries

These are typical in-process module boundaries for this playbook:
- Process Definition
- Execution Engine
- Policy Decisioning
- Integration Task Handling
- Retry and Dead-Letter Handling
- Event and Notification
- Audit and Observability

## Typical V1 Integration Boundaries

- External systems of record commonly receive process outcomes or side-effect callbacks.
- Messaging providers often deliver participant notifications or process signals.
- Third-party APIs may execute task side effects through adapter boundaries.
- Integration handling typically relies on controlled contracts, idempotent processing, and reconciliation-aware recovery.