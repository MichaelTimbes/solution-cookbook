# Approval Workflows / Human-In-The-Loop

## Problem / when to use
- Use when business outcomes require explicit human decisions combined with durable system orchestration.
- Typical in access requests, invoice approvals, publishing gates, and policy exceptions.
- Goal: deterministic progression with auditable accountability and timeout and escalation handling.

## Ingredients
### Data model components
- Workflow instance (state, initiator, priority, timestamps)
- Task record (assignee, due date, decision, comments)
- Routing policy and rule set
- Escalation policy
- Decision audit trail

### API contracts
- Start workflow endpoint.
- Task query and claim endpoints.
- Approve, reject, request-changes actions.
- Escalate and reassign endpoints with authorization checks.
- Callback and signal endpoint for external events.

### UI surfaces
- Request submission form.
- Approver inbox and task detail view.
- Decision panel with policy context.
- Escalation and reassignment controls.
- Timeline and audit view for workflow history.

### Jobs/workers/async components
- Workflow engine worker or orchestrator.
- Timer and escalation scheduler.
- Notification worker.
- Policy evaluation worker.

## Reference flow (happy path + async path)
1. Request is submitted and workflow instance starts.
2. Routing policy assigns first approver task.
3. Approver decides (approve, reject, request changes).
4. System executes side effects and records immutable audit trail.
5. Timeouts trigger reminders and escalations via scheduler.
6. Completion event notifies requestor and downstream systems.

## Variants
- BPMN-modeled workflow engines.
- Durable code-first orchestration engines.
- App-native state machine for simpler flows.
- DMN and decision table driven routing.

## Failure modes & mitigations
- Duplicate approvals from repeated actions → idempotent decision endpoint.
- Stuck tasks from identity changes → fallback assignee and periodic reconciliation.
- Escalation loops due to circular routing rules → static validation and loop guard.
- Missing signals for long-running workflows → heartbeat and timeout detectors.
- Unauthorized reassignment → strict policy checks and audit enforcement.
- State divergence between workflow and business entity → transactional outbox and events.

## Security/privacy considerations
- Enforce least privilege for decision and reassignment actions.
- Require step-up auth for high-risk approvals.
- Protect comments and attachments containing sensitive data.
- Capture non-repudiation metadata for decisions.

## Observability requirements
### Trace spans
- Workflow start and routing decision.
- Task claim and decision submission.
- Escalation timer fire and reassignment.
- Side-effect execution and completion event.

### Metrics
- Time in state by workflow step.
- Approval cycle time.
- Escalation rate.
- Orphaned or stalled workflow count.
- Reassignment frequency.

### Structured logs/audit events
- Workflow instance lifecycle events.
- Task assignment and decision events.
- Policy evaluation snapshots.
- Escalation and override actions.

## Testing checklist
### Unit
- State transition guard logic.
- Routing policy evaluation.
- Escalation timing calculations.

### Integration
- End-to-end request to completion.
- Multi-approver and parallel branch scenarios.
- External callback and signal handling.

### Failure injection/chaos-lite checks
- Lost callback and signal simulation.
- Approver account deprovision mid-flow.
- Scheduler delay and outage recovery.

## Operational runbook checklist
- Identify stalled workflows and affected cohorts.
- Validate scheduler health and queue backlog.
- Reconcile orphan tasks with fallback assignment.
- Perform controlled re-drive of pending transitions.
- Confirm audit continuity before closure.

## Adoption notes by archetype
- CRM: discount and exception approvals.
- Case/Ticket: high-severity escalation approvals.
- Payments/Billing: refund and write-off approvals.
- DMS and CMS: publish and legal review gates.

## Licensing & source attribution notes
- Describe patterns in original language.
- Attribute standards and OSS concepts appropriately.
- Avoid copying proprietary framework text verbatim.
