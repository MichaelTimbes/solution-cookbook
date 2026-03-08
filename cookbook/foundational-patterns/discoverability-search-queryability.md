# Discoverability (Search & Queryability)

## Description of the pattern
Discoverability ensures users and systems can efficiently locate relevant records, views, and insights.

## Why it appears across enterprise systems
As data volume grows, value depends on retrieval speed and precision. Operational work degrades when information is technically present but practically inaccessible.

## Typical implementation capabilities
- [Query Filtering](../capabilities/query-filtering.md)
- [Saved Views](../capabilities/saved-views.md)
- [Search Index](../capabilities/search-index.md)
- [Import / Export Pipelines](../capabilities/import-export-pipelines.md)
- [Custom Fields / Extensible Attributes](../capabilities/custom-fields-extensible-attributes.md)

## Example archetypes that rely on it
- [Analytics Platform](../archetypes/analytics-platform.md)
- [Case / Ticket System](../archetypes/case-ticket-system.md)
- [Document Management System](../archetypes/document-management-system.md)

## Common failure modes when ignored
- Slow operations from unbounded queries
- Users creating shadow data exports to compensate
- Inconsistent decisions from missing or stale search results
