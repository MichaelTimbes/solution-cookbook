# Analytics Platform Archetype

## What this archetype is / is not
- A system for governed data exploration, chart authoring, dashboard sharing, and metric consumption.
- Provides semantic and permission layers between raw data sources and business users.
- Not a full ETL/data engineering platform, though it depends on one.

## Typical modules
- Data source and dataset registry
- Semantic models and metric definitions
- Query and visualization builder
- Dashboard and collection management
- Permissions and governance controls
- Caching and performance acceleration
- Scheduled reports and subscriptions
- Usage analytics and monitoring

## Core workflows (top 3–5)
- Connect data source → register dataset
- Define semantic fields and reusable metrics
- Build chart → assemble dashboard → publish/share
- Manage permissions and access scopes
- Monitor query performance and optimize

## Canonical data model skeleton
### Core entities
- DataSource
- Dataset
- MetricDefinition
- Chart
- Dashboard
- Collection/Folder
- AccessPolicy
- QueryExecution
- AnalyticsAuditEvent

### Key relations
- DataSource 1..N Datasets
- Dataset 0..N MetricDefinitions
- Dataset 0..N Charts
- Dashboard 1..N Charts
- Collection 1..N Dashboards
- Dashboard/Dataset N..1 AccessPolicy set

### Invariants/constraints
- Published dashboards reference valid datasets and metrics.
- Access is evaluated at both dataset and dashboard scopes.
- Query limits and timeout policies enforced.
- Metric definitions are versioned where backward compatibility matters.
- Cached results carry freshness metadata.

## Permission model patterns
- Role-based baseline (viewer, analyst, editor, admin).
- Dataset-level and collection-level permission layering.
- Row-level and column-level security integration.
- Service accounts for scheduled report execution.
- Audit-only roles for compliance and investigations.

## Integration touchpoints
- Data warehouse/lakehouse systems
- Identity provider and SSO
- Notification channels (subscriptions)
- Governance/catalog systems
- Embedding APIs for downstream apps
- Alerting/incidents platforms for performance issues

## Embedded capabilities
- Search, filters, and saved views
- Dynamic evaluation and survey engine
- Notification preferences and routing
- Notification / messaging system
- Rules engine and decisioning
- Audit log and provenance
- Import and export pipelines
- Approval workflows and human-in-the-loop
- Custom fields and extensible attributes
- Idempotency, outbox, retries, and DLQ

## Failure modes catalog (starter set: 8–12)
- Permission leakage through embedded dashboards.
- Dataset schema drift breaking saved charts.
- Expensive queries causing portal degradation.
- Stale caches showing outdated metrics.
- Inconsistent metric definitions across teams.
- Scheduled report failures without alerting.
- Token misconfiguration exposing data source credentials.
- Row-level security bypass via unsupported query path.
- Dashboard dependency cycles during content moves.
- Cross-tenant data bleed in shared environments.

## Observability baseline
### Key traces
- Dashboard load and query fan-out path.
- Chart build and save workflow.
- Scheduled report generation and dispatch.

### Key metrics
- Dashboard load latency.
- Query success/failure rate.
- Slow query rate by dataset.
- Cache hit ratio and freshness lag.
- Permission-denied events by scope.

### Audit events
- Dataset and metric definition changes.
- Dashboard publish/share actions.
- Permission policy updates.
- Scheduled report and subscription changes.
- Embedding token issuance and revocation.

## Minimal architecture diagram (C4-ish, 1 page)
- Context: analysts, business viewers, data platform, embedded consumers.
- Containers: portal UI, query API, semantic layer, cache, metadata DB, audit store, notification worker.
- Relationships: UI calls semantic/query services; services enforce policy and query data sources; outputs cached and visualized.

## Implementation notes and stack variants
- Keep semantic definitions version-controlled and reviewable.
- Enforce policy checks as close to query execution as possible.
- Separate authoring and runtime workloads for performance isolation.
- Treat dashboards as deployable artifacts with dependency validation.

## Licensing & source attribution notes
- Content is synthesized from OSS analytics patterns.
- Do not copy restricted vendor documentation text.
- Add source attribution in final publish pass.
