# Search / Filters / Saved Views

> Legacy capability page
>
> This capability has been split into more focused capabilities.
> See the following instead:
>
> - query-filtering
> - saved-views
> - search-index

## Problem / when to use
- Use when users must repeatedly locate and act on subsets of large record sets.
- Required for CRM pipelines, ticket queues, inventory operations, and analytics worklists.
- Goal: fast retrieval, persistent personalization, and safe sharing.

## Ingredients
### Data model components
- Filter definition model (field, operator, value, grouping)
- Saved view model (name, owner, visibility, query spec, column layout, sort)
- Access-control model for shared views
- Optional materialized or query cache metadata

### API contracts
- List endpoint accepting validated filter DSL.
- Saved view CRUD endpoints.
- Share and unshare endpoints with permission checks.
- Versioned query schema for backwards compatibility.

### UI surfaces
- Search bar with scoped fields.
- Filter builder with typed operators.
- Saved views panel (personal/shared/default).
- Column chooser and sort controls.
- Bulk action toolbar tied to current result set.

### Jobs/workers/async components
- Background index refresh and rebuild jobs.
- Query performance telemetry worker.
- Optional cache invalidation worker.

## Reference flow (happy path + async path)
1. User applies search, filter, and sort to retrieve paginated results.
2. User saves configuration as personal or shared view.
3. System validates permissions and stores normalized query spec.
4. Background workers maintain index freshness and performance telemetry.
5. User reopens view; system re-evaluates with current access constraints.

## Variants
- URL-encoded state for sharable links.
- Server-side persisted preferences for multi-device continuity.
- Hybrid approach with URL as source of truth and server profile fallback.
- Faceted search variant for high-cardinality domains.

## Failure modes & mitigations
- Unbounded filters producing expensive queries → enforce guardrails and limits.
- Saved views breaking after schema changes → introduce query schema migration.
- Shared views exposing unauthorized rows → enforce row-level ACL at execution time.
- Stale index causing missing results → monitor index lag and freshness SLA.
- Ambiguous filter semantics across locales/timezones → normalize and store canonical values.
- Deleted fields referenced by legacy views → soft-fail with repair guidance.

## Security/privacy considerations
- Never trust client-side filters for authorization.
- Validate field-level entitlements before query execution.
- Redact sensitive columns in shared views by policy.
- Audit all shared-view permission changes.

## Observability requirements
### Trace spans
- List query request and planner path.
- Saved view create and update actions.
- Index refresh and reindex operations.

### Metrics
- Query latency percentiles by view.
- Slow-query count by filter pattern.
- Saved-view load and adoption rates.
- Index freshness lag.
- Error rate for invalid and legacy views.

### Structured logs/audit events
- Saved view create, update, delete, share, and unshare events.
- Query execution metadata (sanitized).
- ACL enforcement outcomes for shared views.
- Schema migration applied to stored views.

## Testing checklist
### Unit
- Filter DSL parser and validator.
- Query spec normalization.
- ACL evaluation for shared views.

### Integration
- End-to-end search with saved-view persistence.
- Schema evolution compatibility for stored views.
- Row-level security validation under shared links.

### Failure injection/chaos-lite checks
- Index lag simulation.
- Burst of expensive queries.
- Mid-migration query schema mismatch.

## Operational runbook checklist
- Identify slow-view patterns via telemetry.
- Apply temporary query limits and communicate impact.
- Rebuild index if freshness SLA is breached.
- Migrate and repair broken saved views.
- Verify security constraints after remediation.

## Adoption notes by archetype
- CRM: pipeline and territory views.
- Case/Ticket: queue triage and SLA watch lists.
- Inventory/Catalog: stock and exception lists.
- Analytics portals: dataset and dashboard governance lists.

## Licensing & source attribution notes
- Keep UX guidance as synthesized patterns.
- Attribute OSS and UI framework inspirations without copying restricted text.
- Mark reusable components by license class in final docs.
