# Human Communication

primary-role: interaction
secondary-role: governance-trust

## What this capability is
- contextual, durable, audience-aware human collaboration with clear visibility, acknowledgement, and accountability boundaries.

## When to use it
- Use when people must communicate with other people in the context of shared work objects.
- Apply when discussion history, mentions, handoffs, and escalation communication must remain attached to records, not externalized into disconnected tools.

## When not to use it
- Do not treat this capability as a broad catch-all; keep adjacent concerns in separate capabilities.

## Core behaviors
- User opens a work object and starts or joins a thread.
- User posts a comment or reply with optional mentions and directed recipients.
- System validates participation and visibility rules before persistence.
- Thread and timeline records are stored as durable context for the parent object.
- Mention and acknowledgement states update asynchronously for recipients.
- Escalation communication, if configured, is appended to the same discussion lineage.

## Typical components
- Thread create/read/list APIs scoped to parent object permissions.
- Comment/reply create and edit APIs with immutable history policy options.
- Mention and directed communication APIs.
- Read-state and acknowledgement update APIs.
- Audience and visibility management APIs.
- Assignment handoff and escalation note APIs.
- Contextual conversation panel embedded with the work object.
- Threaded comment and reply view.
- Mention composer with participant resolution.
- Audience visibility indicator and participation controls.
- Read/acknowledgement indicators for targeted communication.
- Activity timeline integrating communication and state-change events.
- Mention resolution and recipient expansion worker.
- Read-state projection worker for large audiences.
- Timeline projection and indexing worker.
- Escalation reminder worker tied to human communication states.

## Key data concepts
- Conversation thread linked to parent object (ticket, record, document, workflow step, schedule item).
- Message/comment entity (author, timestamp, content, edit lineage, reply linkage).
- Participant model (roles, membership, watch/follow state).
- Mention and directed-recipient model.
- Visibility scope model (private, team, tenant, cross-team, restricted audience).
- Read/acknowledgement state model.
- Handoff and escalation communication markers.
- Discussion timeline projection for fast retrieval.

## Common workflows
- Object-anchored threads only (one parent object, many threads).
- Single canonical discussion timeline per object.
- Role-constrained communication channels (for example, internal-only vs external-facing).
- Strict acknowledgement-required mode for critical updates.
- Lightweight comment mode for low-governance domains.

## Integration touchpoints
- Thread create/read/list APIs scoped to parent object permissions.
- Comment/reply create and edit APIs with immutable history policy options.
- Mention and directed communication APIs.
- Read-state and acknowledgement update APIs.
- Audience and visibility management APIs.
- Assignment handoff and escalation note APIs.

## Risks / failure modes
- Context drift from off-platform communication -> enforce object-anchored thread entry points and reference links.
- Mention noise and alert fatigue -> support directed communication, audience scoping, and mention policy controls.
- Hidden critical updates -> add acknowledgement-required paths for high-severity communication.
- Unauthorized audience exposure -> apply row/object-level authorization and scope validation on every read/write.
- Ambiguous handoff ownership -> require explicit handoff note templates with actor attribution.
- Fragmented discussion history across duplicate threads -> provide thread merge guidance and canonical timeline views.
- Enforce least-privilege participation and visibility by role and tenant boundaries.
- Apply content access checks on both thread metadata and message payload retrieval.

## Related archetypes
- Case/Ticket: assignment handoffs, escalation commentary, and closure rationale.
- CRM: opportunity/account coordination, ownership changes, and follow-up alignment.
- Workflow/BPM: decision context exchange, exception handling communication, and approver collaboration.
- DMS/CMS: review conversations, editorial/legal clarifications, and publication readiness coordination.
- Scheduling/Rostering: shift handoff notes, coverage requests, and escalation communication.

## Related capabilities
- [notification-preferences-routing](notification-preferences-routing.md)
- [notification-messaging-system](notification-messaging-system.md)
- [approval-workflows-human-in-the-loop](approval-workflows-human-in-the-loop.md)
- [audit-log-provenance](audit-log-provenance.md)

