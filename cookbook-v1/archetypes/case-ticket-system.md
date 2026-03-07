# Case / Ticket System Archetype

## What this archetype is / is not
- A workflow system for intake, triage, assignment, resolution, and closure of cases and tickets under SLA constraints.
- Designed for support, ITSM, and case-management operations with automation and auditability.
- Not a generic project management tool or full CRM replacement.

## Typical modules
- Intake channels (portal, email, API)
- Classification and prioritization
- Queues, assignment, and ownership
- SLA policy and timers
- Automation (triggers, schedulers, escalations)
- Notifications and customer communications
- Knowledge linkage and canned responses
- Reporting and workforce dashboards

## Core workflows (top 3–5)
- Ticket creation → classification → queue assignment
- Agent assignment → work log updates → status transitions
- SLA monitoring → warning and escalation actions
- Resolution → customer confirmation → closure
- Reopen and recurrence handling

## Canonical data model skeleton
### Core entities
- Ticket and Case
- Requester
- Agent
- Queue and Team
- SLA policy
- Status transition record
- Comment and communication
- Automation rule

### Key relations
- Requester 1..N Tickets
- Ticket N..1 Queue
- Ticket N..1 Assigned Agent (nullable)
- Ticket 1..N Comments and communications
- Ticket 1..N Status transitions
- Ticket N..1 SLA policy (effective version)

### Invariants/constraints
- Status must follow a configured transition graph.
- SLA timer state must align with current status.
- Assignment changes require actor attribution.
- External communications must preserve delivery state.
- Reopen actions must retain prior closure context.

## Permission model patterns
- Requester versus agent separation.
- Queue-scoped access for operational teams.
- Supervisor override for escalations and reassignment.
- Restricted visibility for sensitive ticket categories.
- Immutable audit visibility for compliance roles.

## Integration touchpoints
- Email, SMS, and push delivery providers
- Identity provider and SSO
- CRM and account context providers
- Incident and on-call systems
- Knowledge base and CMS
- Analytics and data warehouse

## Embedded capabilities
- Search, filters, and saved views
- Approval workflows and human-in-the-loop
- Dynamic evaluation and survey engine
- Template and merge fields document generation
- Notification preferences and routing
- Rules engine and decisioning
- Import and export pipelines
- Audit log and provenance
- Custom fields and extensible attributes
- Idempotency, outbox, retries, and DLQ

## Failure modes catalog (starter set: 8–12)
- Misconfigured automation loops causing status thrashing.
- Scheduler jobs firing duplicate escalations.
- SLA breaches due to timezone and calendar misconfiguration.
- Queue overload without backpressure policies.
- Notifications sent after closure due to stale events.
- Permission leakage via shared views.
- Duplicate ticket creation from webhook retries.
- Orphan tickets after user deprovisioning.
- Reopen path bypassing required validation checks.
- Partial import creating malformed historical tickets.

## Observability baseline
### Key traces
- Intake event to persisted ticket path.
- Ticket escalation path across timer and notification services.
- Resolution and closure workflow including outbound communications.

### Key metrics
- Time to first response.
- Time to resolution.
- SLA breach rate by queue.
- Reopen rate.
- Automation success and error rate.

### Audit events
- Ticket status transitions.
- Assignment and queue changes.
- SLA policy evaluations and breaches.
- Outbound communication attempts and outcomes.
- Rule and scheduler configuration changes.

## Minimal architecture diagram (C4-ish, 1 page)
- Context: requesters, agents, supervisors, external communication systems.
- Containers: portal UI, agent UI, API, rules engine, scheduler, DB, event bus, search index.
- Relationships: API publishes domain events, workers evaluate policies and notify channels.

## Implementation notes and stack variants
- Keep SLA calculation logic centralized and versioned.
- Separate user-authored comments from system events.
- Use idempotency keys for inbound channel ingestion.
- Ensure scheduler and trigger engines have deterministic ordering.

## Licensing & source attribution notes
- Page content is original synthesis aligned to public OSS and standards references.
- Include per-source attribution in finalized version.
- Do not copy restricted vendor text or diagrams directly.
