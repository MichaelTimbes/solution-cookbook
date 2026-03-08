# Human Communication & Coordination

## Description of the pattern
Human Communication & Coordination is the recurring architectural force where systems must support people coordinating with people around shared work context. The system is not only a record store; it is also a collaboration surface where decisions, clarifications, handoffs, and escalation conversations happen.

This pattern appears when users need durable, contextual, role-aware communication attached to business objects such as tickets, accounts, documents, tasks, schedules, or workflow instances.

## Why it appears across enterprise systems
Enterprise work is distributed across teams, roles, and time zones. Even highly automated systems require human interpretation, exception handling, approvals, and handoffs. As a result, communication must be:
- contextual to the work item
- durable enough for later reconstruction
- visible to the right audience
- constrained by authorization and privacy boundaries
- structured enough to prevent coordination drift

Without this pattern, systems force coordination into external channels and lose authoritative operational context.

## Typical systems that rely on it
- [Case / Ticket System](../archetypes/case-ticket-system.md)
- [CRM](../archetypes/crm.md)
- [Workflow / BPM System](../archetypes/workflow-bpm-system.md)
- [Document Management System](../archetypes/document-management-system.md)
- [CMS / Wiki / Knowledge Base](../archetypes/cms-wiki-kb.md)
- [Scheduling / Rostering](../archetypes/scheduling-rostering.md)

## Common failure modes when ignored
- Decisions and rationale are scattered across unmanaged channels.
- Handoffs fail due to missing audience context.
- Escalations happen without durable timeline evidence.
- Mention or assignment intent is not visible to the intended participants.
- Sensitive discussion context leaks across visibility boundaries.
- Users cannot determine who has acknowledged critical updates.

## Typical implementation capabilities
- [Human Communication](../capabilities/human-communication.md)
- [Notification Preferences and Routing](../capabilities/notification-preferences-routing.md)
- [Notification / Messaging System](../capabilities/notification-messaging-system.md)
- [Audit Log + Provenance](../capabilities/audit-log-provenance.md)

## Common archetypes that depend on it
- [Case / Ticket System](../archetypes/case-ticket-system.md): triage, assignment, escalation, and closure coordination.
- [CRM](../archetypes/crm.md): account ownership changes, opportunity discussion, and follow-up alignment.
- [Workflow / BPM System](../archetypes/workflow-bpm-system.md): decision context and exception collaboration.
- [Document Management System](../archetypes/document-management-system.md): review commentary, signoff clarifications, and retention-related coordination.
- [CMS / Wiki / Knowledge Base](../archetypes/cms-wiki-kb.md): editorial collaboration and publication readiness discussion.
- [Scheduling / Rostering](../archetypes/scheduling-rostering.md): shift handoffs, coverage negotiation, and incident communication.

## Design intent summary
Systems that manage real work must treat human communication as a first-class architectural concern. Durable, context-linked, audience-aware collaboration improves decision quality, operational continuity, and accountability.
