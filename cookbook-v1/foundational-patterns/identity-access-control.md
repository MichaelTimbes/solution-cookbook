# Identity & Access Control

## Description of the pattern
Identity & Access Control defines who an actor is, what they can do, and where those permissions apply.

## Why it appears across enterprise systems
Enterprise systems span many roles, tenants, and trust zones. Without explicit identity and authorization boundaries, domain correctness and security both fail.

## Typical implementation capabilities
- [Audit Log + Provenance](../capabilities/audit-log-provenance.md)
- [Notification / Messaging System](../capabilities/notification-messaging-system.md)
- [Approval Workflows / Human-In-The-Loop](../capabilities/approval-workflows-human-in-the-loop.md)

## Example archetypes that rely on it
- [Identity / Access (CIAM)](../archetypes/identity-access-ciam.md)
- [CRM](../archetypes/crm.md)
- [Case / Ticket System](../archetypes/case-ticket-system.md)

## Common failure modes when ignored
- Permission leakage across tenant or role boundaries
- Untraceable privileged actions
- Inconsistent access behavior across APIs and UI
