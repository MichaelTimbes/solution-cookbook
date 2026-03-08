# Search Index

## What this capability is
- Builds and maintains searchable indexes so large datasets can be retrieved with acceptable latency and relevance.

## When to use it
- Use when datasets are too large for direct scans and need indexed retrieval.
- Use when full-text search, facet counts, and relevance ordering are required.

## When not to use it
- Do not use for user preference persistence; that belongs in [Saved Views](saved-views.md).
- Do not use as business-policy filtering logic; apply policy via [Query Filtering](query-filtering.md).

## Core behaviors
- Ingest source changes and transform them into indexable documents.
- Build and refresh indexes for full-text, faceting, and fast lookup paths.
- Execute relevance-ranked retrieval with optional facet aggregation.
- Track index freshness lag and recover from failed indexing batches.
- Reconcile deletes and updates to avoid stale or ghost search results.

## Typical components
- Index ingestion pipeline (change feed, batch loader, or event consumer).
- Index storage engine (inverted index/vector index as needed).
- Reindex scheduler and backfill tooling.
- Search API for ranked retrieval and facet responses.
- Relevance tuning controls (field boosts, analyzers, synonym sets).
- Index health monitoring and repair tooling.

## Key data concepts
- Index document schema mapped from source domain records.
- Index version and mapping configuration.
- Change cursor/checkpoint for incremental indexing.
- Relevance profile settings and analyzer configuration.
- Freshness and coverage metadata for operational SLO tracking.

## Common workflows
- Initial backfill creates baseline index from source-of-truth records.
- Incremental updates process create/update/delete events into index mutations.
- Scheduled or rolling reindex runs after mapping and relevance changes.
- Incident workflow replays failed indexing batches to restore coverage.

## Integration touchpoints
- Source systems emitting change events or export snapshots.
- Query APIs and UI search surfaces that consume ranked results.
- Authorization and tenant-boundary services for secure retrieval filtering.
- Observability pipelines tracking latency, error rates, and index lag.

## Risks / failure modes
- Stale index causing missing results -> monitor index lag and freshness SLA.
- Mapping drift between source schema and index schema -> enforce compatibility checks before rollout.
- Reindex backlog during traffic spikes -> shard scaling and backpressure controls.
- Relevance regressions after analyzer changes -> canary relevance tests and rollback profiles.

## Related archetypes
- CRM: pipeline and territory views.
- Case/Ticket: queue triage and SLA watch lists.
- Inventory/Catalog: stock and exception lists.
- Analytics portals: dataset and dashboard governance lists.

## Related capabilities
- [query-filtering](query-filtering.md)
- [saved-views](saved-views.md)
- [custom-fields-extensible-attributes](custom-fields-extensible-attributes.md)
- [import-export-pipelines](import-export-pipelines.md)


