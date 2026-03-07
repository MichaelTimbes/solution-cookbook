# Workflow / BPM System Archetype

## What this archetype is / is not
- A system for defining, executing, monitoring, and evolving long-running business processes with human and system tasks.
- Built for reliable orchestration, explicit state transitions, and auditability.
- Not just a queue processor or a simple cron scheduler.

## Typical modules
- Process definition and versioning
- Task management and assignment
- Decisioning and routing rules
- Timers, reminders, and escalations
- Execution engine and persistence
- Integration connectors and callbacks
- Monitoring and operations console
- Audit and history explorer

## Core workflows (top 3–5)
- Model workflow → deploy version → start instances
- Route work item to human approver or system task
- Evaluate decision table and branch path
- Handle timeout, escalation, and retry
- Complete or compensate workflow on terminal outcome

## Canonical data model skeleton
### Core entities
- ProcessDefinition
- ProcessVersion
- WorkflowInstance
- TaskInstance
- DecisionPolicy
- TimerEvent
- Signal/EventMessage
- CompensationRecord
- WorkflowAuditEvent

### Key relations
- ProcessDefinition 1..N ProcessVersions
- ProcessVersion 1..N WorkflowInstances
- WorkflowInstance 1..N TaskInstances
- WorkflowInstance 0..N TimerEvents
- WorkflowInstance 0..N Signal/EventMessages
- WorkflowInstance 0..N CompensationRecords

### Invariants/constraints
- Each workflow instance references a fixed process version.
- State transitions follow the declared process graph.
- Task actions require valid assignee and authorization.
- Compensations are idempotent and replay-safe.
- Timer events are uniquely keyed per workflow state.

## Permission model patterns
- Separate model author, deployer, operator, and approver roles.
- Scope task access by queue, domain, and tenant.
- Require explicit permission for manual state overrides.
- Restrict process-definition mutation in production.
- Audit all administrative and override actions.

## Integration touchpoints
- Identity provider and SSO
- Line-of-business APIs
- Messaging/event bus
- Notification channels
- Rules and decision engines
- Document and e-signature systems

## Embedded capabilities
- Approval workflows and human-in-the-loop
- Dynamic evaluation and survey engine
- Rules engine and decisioning
- Notification preferences and routing
- Notification / messaging system
- Audit log and provenance
- Idempotency, outbox, retries, and DLQ
- Import and export pipelines
- Search, filters, and saved views
- Custom fields and extensible attributes

## Failure modes catalog (starter set: 8–12)
- Workflow instances stuck on missing external signals.
- Duplicate signal handling causing repeated side effects.
- Timer drift leading to late escalations.
- Decision policy updates breaking in-flight assumptions.
- Manual overrides bypassing process constraints.
- Dead-lettered integration tasks without operator visibility.
- Compensation logic failing and leaving inconsistent business state.
- Version rollout causing split behavior across instances.
- Queue starvation for lower-priority tasks.
- Task reassignment loops after organizational changes.

## Observability baseline
### Key traces
- Workflow start to completion journey.
- Task claim, decision, and state-transition sequence.
- Escalation timer to notification and reassignment path.

### Key metrics
- Active instance count by process and state.
- Time-in-state and cycle time percentiles.
- Task backlog size and age.
- Escalation rate and completion rate.
- Failure and compensation rates.

### Audit events
- Process definition publish and rollback.
- Instance state transitions.
- Task assignments and decisions.
- Manual overrides and re-drives.
- External signal receipt and processing outcomes.

## Minimal architecture diagram (C4-ish, 1 page)
- Context: requesters, approvers, operators, external systems.
- Containers: workflow UI, orchestration API, execution engine, task queue, scheduler, state store, event bus, audit store.
- Relationships: engine manages state; scheduler fires timers; workers execute system tasks; UI manages human tasks.

## Implementation notes and stack variants
- Prefer durable execution semantics for long-running processes.
- Keep process definition versioning explicit and immutable.
- Separate orchestration concerns from domain side-effect handlers.
- Design compensations and retries from the first iteration.

## Licensing & source attribution notes
- Content is original synthesis informed by standards and OSS workflows.
- Avoid direct text reuse from proprietary guides.
- Add source and license notes per finalized page.
