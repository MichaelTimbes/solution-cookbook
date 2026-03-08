# Saved Views

## What this capability is
- Persists reusable query and layout configurations so teams can return to high-value operational views quickly.

## When to use it
- Use when teams repeatedly apply the same query criteria, sorting, and column sets.
- Use when operational handoffs rely on named shared views and role-specific defaults.

## When not to use it
- Do not use as a query execution engine; pair with [Query Filtering](query-filtering.md).
- Do not use as an index or retrieval layer; pair with [Search Index](search-index.md) for scale.

## Core behaviors
- Persist named view definitions (filters, sort, columns, and optional grouping).
- Scope views as personal, team-shared, or organization-default.
- Resolve a saved view into an executable query at runtime.
- Track ownership and permission changes for shared operational views.
- Provide safe migration when underlying schema or fields evolve.

## Typical components
- Saved view registry service and persistence store.
- CRUD APIs for create/update/archive/restore view definitions.
- Sharing and ownership APIs with role-aware permission checks.
- UI surfaces for pinned, recent, and default views.
- Migration utility for view schema/version upgrades.
- Audit trail for shared-view mutations.

## Key data concepts
- Saved view record (id, name, owner, visibility, query payload, layout settings).
- View scope and access model (personal/team/org with role constraints).
- Default-view assignment per role, queue, or workspace.
- View schema version and migration status.

## Common workflows
- Analyst or operator saves a recurring queue/report view for repeated use.
- Team lead shares and pins a canonical operational view for handoffs.
- Platform migrates saved views when fields are renamed or retired.
- Org admin retires stale shared views and promotes new defaults.

## Integration touchpoints
- Query execution services that consume saved view payloads.
- Identity and authorization systems for ownership and share scope enforcement.
- Notification systems for shared-view updates where collaboration requires it.
- Analytics/audit pipelines for view usage and stale view detection.

## Risks / failure modes
- Saved views breaking after schema changes -> introduce query schema migration.
- Shared views exposing unauthorized rows -> enforce row-level ACL at execution time.
- Deleted fields referenced by legacy views -> soft-fail with repair guidance.
- View sprawl and low trust in defaults -> apply lifecycle ownership and archival policies.
- Hidden operational dependencies on one user's personal view -> require team-owned shared views for critical processes.

## Related archetypes
- CRM: pipeline and territory views.
- Case/Ticket: queue triage and SLA watch lists.
- Inventory/Catalog: stock and exception lists.
- Analytics portals: dataset and dashboard governance lists.

## Related capabilities
- [query-filtering](query-filtering.md)
- [search-index](search-index.md)
- [custom-fields-extensible-attributes](custom-fields-extensible-attributes.md)
- [notification-preferences-routing](notification-preferences-routing.md)


