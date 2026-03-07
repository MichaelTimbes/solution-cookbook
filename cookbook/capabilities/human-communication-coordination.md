# Human Communication / Collaboration Layer

## Problem / when to use
- Use when people must communicate with other people in the context of shared work objects.
- Apply when discussion history, mentions, handoffs, and escalation communication must remain attached to records, not externalized into disconnected tools.
- Goal: contextual, durable, audience-aware human collaboration with clear visibility, acknowledgement, and accountability boundaries.

## Ingredients
### Data model components
- Conversation thread linked to parent object (ticket, record, document, workflow step, schedule item).
- Message/comment entity (author, timestamp, content, edit lineage, reply linkage).
- Participant model (roles, membership, watch/follow state).
- Mention and directed-recipient model.
- Visibility scope model (private, team, tenant, cross-team, restricted audience).
- Read/acknowledgement state model.
- Handoff and escalation communication markers.
- Discussion timeline projection for fast retrieval.

### API contracts
- Thread create/read/list APIs scoped to parent object permissions.
- Comment/reply create and edit APIs with immutable history policy options.
- Mention and directed communication APIs.
- Read-state and acknowledgement update APIs.
- Audience and visibility management APIs.
- Assignment handoff and escalation note APIs.

### UI surfaces
- Contextual conversation panel embedded with the work object.
- Threaded comment and reply view.
- Mention composer with participant resolution.
- Audience visibility indicator and participation controls.
- Read/acknowledgement indicators for targeted communication.
- Activity timeline integrating communication and state-change events.

### Jobs/workers/async components
- Mention resolution and recipient expansion worker.
- Read-state projection worker for large audiences.
- Timeline projection and indexing worker.
- Escalation reminder worker tied to human communication states.

## Reference flow (happy path + async path)
1. User opens a work object and starts or joins a thread.
2. User posts a comment or reply with optional mentions and directed recipients.
3. System validates participation and visibility rules before persistence.
4. Thread and timeline records are stored as durable context for the parent object.
5. Mention and acknowledgement states update asynchronously for recipients.
6. Escalation communication, if configured, is appended to the same discussion lineage.

## Variants
- Object-anchored threads only (one parent object, many threads).
- Single canonical discussion timeline per object.
- Role-constrained communication channels (for example, internal-only vs external-facing).
- Strict acknowledgement-required mode for critical updates.
- Lightweight comment mode for low-governance domains.

## Failure modes & mitigations
- Context drift from off-platform communication -> enforce object-anchored thread entry points and reference links.
- Mention noise and alert fatigue -> support directed communication, audience scoping, and mention policy controls.
- Hidden critical updates -> add acknowledgement-required paths for high-severity communication.
- Unauthorized audience exposure -> apply row/object-level authorization and scope validation on every read/write.
- Ambiguous handoff ownership -> require explicit handoff note templates with actor attribution.
- Fragmented discussion history across duplicate threads -> provide thread merge guidance and canonical timeline views.

## Security/privacy considerations
- Enforce least-privilege participation and visibility by role and tenant boundaries.
- Apply content access checks on both thread metadata and message payload retrieval.
- Protect sensitive discussion content in transit and at rest.
- Preserve immutable author/time attribution for governance-relevant communication.
- Support retention and redaction policies aligned to domain requirements.

## Observability requirements
### Trace spans
- Thread creation and parent-object authorization check.
- Comment/reply write path and mention expansion.
- Read/acknowledgement updates.
- Visibility-scope mutations.
- Escalation communication append events.

### Metrics
- Thread creation and participation rates by object type.
- Mention-to-response latency.
- Acknowledgement completion rates for required notices.
- Handoff communication completion rate.
- Visibility-scope change volume.

### Structured logs/audit events
- Thread and message lifecycle events.
- Mention targeting and resolution outcomes.
- Read/acknowledgement transitions.
- Visibility scope changes with actor attribution.
- Handoff and escalation communication events.

## Testing checklist
### Unit
- Visibility and participation policy evaluators.
- Mention parsing and recipient resolution.
- Read/acknowledgement state transitions.

### Integration
- End-to-end thread/comment/reply flows on protected parent objects.
- Mention and directed communication behavior by role.
- Handoff and escalation note propagation within timeline context.

### Failure injection/chaos-lite checks
- Delayed mention processing and eventual timeline consistency.
- Concurrent edits/replies in high-traffic threads.
- Access policy changes while users are active in discussions.

## Operational runbook checklist
- Identify communication-impacting incidents by object scope and audience size.
- Verify thread/write permissions and visibility policy health.
- Reconcile delayed mention or acknowledgement state projections.
- Triage escalation communication lag for high-severity workflows.
- Confirm audit continuity and timeline integrity after remediation.

## Adoption notes by archetype
- Case/Ticket: assignment handoffs, escalation commentary, and closure rationale.
- CRM: opportunity/account coordination, ownership changes, and follow-up alignment.
- Workflow/BPM: decision context exchange, exception handling communication, and approver collaboration.
- DMS/CMS: review conversations, editorial/legal clarifications, and publication readiness coordination.
- Scheduling/Rostering: shift handoff notes, coverage requests, and escalation communication.

## Boundary clarification
- This capability addresses human-to-human coordination in system context.
- It is distinct from infrastructure messaging concerns such as brokers, queues, pub/sub topology, or event transport internals.

## Licensing & source attribution notes
- Keep content architecture-focused, implementation-neutral, and vendor-neutral.
- Reference standards and platform concepts through synthesis.
- Avoid copying proprietary product documentation text.
