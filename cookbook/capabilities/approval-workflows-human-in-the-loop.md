# Approval Workflows / Human-In-The-Loop

## What this capability is
- deterministic progression with auditable accountability and timeout and escalation handling.

## When to use it
- Use when business outcomes require explicit human decisions combined with durable system orchestration.
- Typical in access requests, invoice approvals, publishing gates, and policy exceptions.

## When not to use it
- Do not treat this capability as a broad catch-all; keep adjacent concerns in separate capabilities.

## Core behaviors
- Request is submitted and workflow instance starts.
- Routing policy assigns first approver task.
- Approver decides (approve, reject, request changes).
- System executes side effects and records immutable audit trail.
- Timeouts trigger reminders and escalations via scheduler.
- Completion event notifies requestor and downstream systems.

## Typical components
- Start workflow endpoint.
- Task query and claim endpoints.
- Approve, reject, request-changes actions.
- Escalate and reassign endpoints with authorization checks.
- Callback and signal endpoint for external events.
- Request submission form.
- Approver inbox and task detail view.
- Decision panel with policy context.
- Escalation and reassignment controls.
- Timeline and audit view for workflow history.
- Workflow engine worker or orchestrator.
- Timer and escalation scheduler.
- Notification worker.
- Policy evaluation worker.

## Key data concepts
- Workflow instance (state, initiator, priority, timestamps)
- Task record (assignee, due date, decision, comments)
- Routing policy and rule set
- Escalation policy
- Decision audit trail

## Common workflows
- BPMN-modeled workflow engines.
- Durable code-first orchestration engines.
- App-native state machine for simpler flows.
- DMN and decision table driven routing.

## Integration touchpoints
- Start workflow endpoint.
- Task query and claim endpoints.
- Approve, reject, request-changes actions.
- Escalate and reassign endpoints with authorization checks.
- Callback and signal endpoint for external events.

## Risks / failure modes
- Duplicate approvals from repeated actions -> idempotent decision endpoint.
- Stuck tasks from identity changes -> fallback assignee and periodic reconciliation.
- Escalation loops due to circular routing rules -> static validation and loop guard.
- Missing signals for long-running workflows -> heartbeat and timeout detectors.
- Unauthorized reassignment -> strict policy checks and audit enforcement.
- State divergence between workflow and business entity -> transactional outbox and events.
- Enforce least privilege for decision and reassignment actions.
- Require step-up auth for high-risk approvals.

## Related archetypes
- CRM: discount and exception approvals.
- Case/Ticket: high-severity escalation approvals.
- Payments/Billing: refund and write-off approvals.
- DMS and CMS: publish and legal review gates.

## Related capabilities
- [rules-engine-decisioning](rules-engine-decisioning.md)
- [notification-preferences-routing](notification-preferences-routing.md)
- [audit-log-provenance](audit-log-provenance.md)
- [human-communication](human-communication.md)


