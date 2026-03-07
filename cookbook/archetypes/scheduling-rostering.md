# Scheduling / Rostering Archetype

## What this archetype is / is not
- A system for managing availability, slot generation, booking, assignment, and schedule changes.
- Supports both appointment booking and workforce rostering use cases.
- Not a full payroll or HRIS platform, though it often integrates with both.

## Typical modules
- Availability and constraints engine
- Slot generation and conflict detection
- Booking and rescheduling
- Assignment and roster management
- Notifications and reminders
- Calendar synchronization
- Policy and exception handling
- Reporting and utilization analytics

## Core workflows (top 3–5)
- Define availability and constraints
- Generate slots and expose booking options
- Confirm booking and send notifications
- Reschedule or cancel with policy checks
- Publish roster and handle exceptions

## Canonical data model skeleton
### Core entities
- SchedulePolicy
- AvailabilityWindow
- BookingSlot
- Appointment/Shift
- Participant/Resource
- Assignment
- ExceptionRule
- ReminderEvent
- ScheduleAuditEvent

### Key relations
- Resource 1..N AvailabilityWindows
- AvailabilityWindow 1..N BookingSlots
- BookingSlot 0..1 Appointment/Shift
- Appointment/Shift 1..N Participants
- Appointment/Shift 0..N ReminderEvents
- Policy 0..N ExceptionRules

### Invariants/constraints
- No double-booking for a resource unless overbook policy explicitly allows it.
- Timezone normalization is required at storage and API boundaries.
- Capacity limits enforced per slot.
- Reschedule/cancel windows enforced by policy.
- Assignment changes preserve audit trail.

## Permission model patterns
- Self-service user booking with scoped capabilities.
- Scheduler and supervisor roles for roster changes.
- Resource-level access boundaries for sensitive calendars.
- Override permissions for emergency reassignments.
- Audited break-glass operations.

## Integration touchpoints
- External calendar providers
- Identity provider and SSO
- Messaging channels for reminders
- Video/meeting systems
- Workforce and HR systems
- Billing or payment systems for appointment scenarios

## Embedded capabilities
- Notification preferences and routing
- Notification / messaging system
- Approval workflows and human-in-the-loop
- Dynamic evaluation and survey engine
- Search, filters, and saved views
- Rules engine and decisioning
- Audit log and provenance
- Import and export pipelines
- Idempotency, outbox, retries, and DLQ
- Custom fields and extensible attributes

## Failure modes catalog (starter set: 8–12)
- Race conditions booking the last available slot.
- Timezone conversion errors producing wrong local times.
- Reminder storms after duplicate schedule updates.
- Calendar sync drift across providers.
- Canceled slots not released to availability.
- Over-constrained roster producing no feasible schedule.
- Resource deactivation leaving orphaned assignments.
- Bulk import creating overlapping shifts.
- Policy misconfiguration allowing forbidden reschedules.
- Notification failures causing missed appointments.

## Observability baseline
### Key traces
- Slot search to booking confirmation.
- Reschedule workflow with policy evaluation.
- Calendar sync and conflict-resolution path.

### Key metrics
- Booking conversion rate.
- No-show rate.
- Reschedule/cancel rates.
- Sync lag and failure rates.
- Resource utilization and schedule coverage.

### Audit events
- Availability policy updates.
- Booking create, update, cancel.
- Assignment and roster changes.
- Override and exception actions.
- External sync reconciliation actions.

## Minimal architecture diagram (C4-ish, 1 page)
- Context: end users, schedulers, resources, external calendar systems.
- Containers: booking UI, scheduling API, constraint engine, sync workers, DB, event bus, notification service.
- Relationships: API writes canonical schedule state; engine validates constraints; workers synchronize and notify.

## Implementation notes and stack variants
- Keep canonical schedule state internal and treat external calendars as projections.
- Use optimistic locking or reservation tokens to prevent slot races.
- Separate appointment and workforce modes behind policy configurations.
- Design reminder pipeline with dedupe keys.

## Licensing & source attribution notes
- Content is original synthesis from open references and standards patterns.
- Avoid direct reuse of vendor-specific implementation text.
- Record per-source attribution during final review.
