# Query Filtering

primary-role: interaction
secondary-role: execution-transport

## What this capability is
- Provides consistent filtering semantics so users and services can narrow result sets safely and predictably.

## When to use it
- Use when users need structured filters (status, owner, priority, date ranges, facets) on large result sets.
- Use when policies require server-side enforcement of filter rules and pagination boundaries.

## When not to use it
- Do not use as a replacement for indexing; filtering narrows results but does not solve retrieval performance on its own.
- Do not use to store user-specific reusable presets; that belongs in [Saved Views](saved-views.md).

## Core behaviors
- Parse and validate filter expressions against an allowed field/operator set.
- Enforce authorization-aware filtering before query execution.
- Normalize sort and pagination parameters into a deterministic query plan.
- Return stable result ordering for repeatable paging.
- Reject unsafe or overly expensive query shapes with explicit validation errors.

## Typical components
- Filter parser and validator (DSL or structured JSON model).
- Query planner translating validated filters to datastore-native predicates.
- Policy guard layer for field-level and row-level constraints.
- API endpoint for list/search with typed filter contracts.
- Optional UI filter builder with operator controls.
- Query observability hooks for latency and cardinality guardrails.

## Key data concepts
- Filter expression (field, operator, value, logical grouping).
- Query contract version (to evolve filter semantics safely).
- Sort and pagination policy (cursor or offset with constraints).
- Authorization context attached to query execution.

## Common workflows
- User composes filters in UI; API validates and executes constrained query.
- API consumers submit structured filters for operational list endpoints.
- Policy update changes allowed filters; invalid filters are rejected with repair hints.
- Teams standardize canonical filter presets that can later be persisted as saved views.

## Integration touchpoints
- Primary read/list APIs for CRM, ticketing, workflow, and inventory domains.
- Optional search backends for full-text plus structured filtering.
- Rules/policy engines when filter permissions depend on runtime context.
- Audit and observability pipelines for query usage and abuse detection.

## Risks / failure modes
- Unbounded filters producing expensive queries -> enforce guardrails and limits.
- Stale index causing missing results -> monitor index lag and freshness SLA.
- Ambiguous filter semantics across locales/timezones -> normalize and store canonical values.
- Never trust client-side filters for authorization.
- Validate field-level entitlements before query execution.
- Schema drift invalidating filter fields -> add compatibility checks and deprecation windows.

## Related archetypes
- CRM: pipeline and territory views.
- Case/Ticket: queue triage and SLA watch lists.
- Inventory/Catalog: stock and exception lists.
- Analytics portals: dataset and dashboard governance lists.

## Related capabilities
- [saved-views](saved-views.md)
- [search-index](search-index.md)
- [custom-fields-extensible-attributes](custom-fields-extensible-attributes.md)
- [rules-engine-decisioning](rules-engine-decisioning.md)


