# Sales CRM Architecture

- Lead intake boundary and enrichment service.
- Account/contact domain service.
- Opportunity pipeline service.
- Quote and approval orchestration service.
- Search and forecast query service.
- Notification and task routing service.
- Audit and activity timeline service.
- Integration boundary for marketing, order, and billing systems.

Boundary principles: separate canonical pipeline state from analytics projections; keep stage rules explicit and versioned; keep integration updates idempotent.
