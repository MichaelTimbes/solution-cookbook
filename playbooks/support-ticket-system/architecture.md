# Support Ticket System Architecture

## Logical Components

- Intake boundary for portal, email, and API requests.
- Ticket domain service for state, ownership, and resolution context.
- Assignment and routing service for queue balancing.
- SLA policy service for deadlines and escalations.
- Search/query service for agent triage views.
- Notification service for requester and agent updates.
- Audit service for immutable ticket history.
- Integration boundary for CRM and knowledge base context.

## Responsibilities and Interactions

- Intake normalizes channel payloads and enforces required metadata.
- Routing applies priority and team assignment rules.
- Ticket lifecycle publishes events consumed by SLA and notification services.
- Search projections update asynchronously for operational dashboards.
- Audit events capture transitions, reassignments, and communication outcomes.

## Boundary Principles

- Separate canonical ticket state from search projections.
- Keep policy decisions explicit and versioned.
- Keep notification generation separate from delivery routing.
- Keep retries idempotent at integration boundaries.
