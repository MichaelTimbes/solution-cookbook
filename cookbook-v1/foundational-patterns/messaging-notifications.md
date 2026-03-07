# Messaging & Notifications

## Description of the pattern
Messaging & Notifications coordinates communication between systems and humans with delivery guarantees, routing policies, and status feedback.

## Why it appears across enterprise systems
Enterprise workflows depend on timely events, reminders, and alerts. Reliable messaging is a backbone for asynchronous coordination.

## Typical implementation capabilities
- [Notification / Messaging System](../capabilities/notification-messaging-system.md)
- [Notification Preferences and Routing](../capabilities/notification-preferences-routing.md)
- [Idempotency + Outbox + Retries + DLQ](../capabilities/idempotency-outbox-retries-dlq.md)

## Example archetypes that rely on it
- [Scheduling / Rostering](../archetypes/scheduling-rostering.md)
- [Case / Ticket System](../archetypes/case-ticket-system.md)
- [Payments / Billing](../archetypes/payments-billing.md)

## Common failure modes when ignored
- Lost or duplicate notifications
- Unbounded retry storms under outage
- User trust erosion from noisy or late delivery
