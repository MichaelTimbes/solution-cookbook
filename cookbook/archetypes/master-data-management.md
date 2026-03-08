# Master Data Management Archetype

## What this archetype is / is not
- A system for reconciling, governing, and publishing authoritative records across multiple upstream and downstream systems.
- Manages golden records derived from multiple source records using matching, survivorship, and stewardship controls.
- Not just a data warehouse, not only a data quality tool, and not a single-system reference table manager.

## Typical modules
- Ingestion adapters for source systems
- Matching and deduplication engine
- Merge rules and survivorship logic engine
- Golden record store and version history
- Stewardship UI and task management
- Data quality and validation rules
- Publishing and downstream synchronization pipeline
- Audit, lineage, and governance reporting

## Core workflows (top 3-5)
- Source ingestion and normalization
- Match and merge resolution
- Stewardship review and exception handling
- Golden record publishing
- Downstream synchronization and acknowledgment

## Canonical data model skeleton
### Core entities
- MasterEntity
- SourceRecord
- MatchCandidate
- MergeDecision
- StewardshipTask
- SurvivorshipRule
- CanonicalAttributeValue
- PublishEvent
- MdmAuditEvent

### Key relations
- MasterEntity 1..N SourceRecords
- MasterEntity 0..N MatchCandidates
- MatchCandidate 0..1 MergeDecision
- MergeDecision N..1 StewardshipTask (when human review is required)
- MasterEntity 1..N CanonicalAttributeValues
- MasterEntity 0..N PublishEvents

### Invariants/constraints
- Each source record maps to at most one active master entity at a time.
- Golden record updates are deterministic given source inputs and active rules.
- Survivorship rules are versioned and traceable for every merge outcome.
- Stewardship overrides require identity, reason, and timestamp.
- Published canonical records are schema-validated before distribution.

## Permission model patterns
- Separate data steward, governance admin, integration operator, and read-only consumer roles.
- Restrict rule and survivorship changes to authorized governance roles.
- Require explicit approval for high-impact merge or unmerge actions.
- Scope stewardship queues by domain, region, and data sensitivity.
- Audit all manual corrections, rule updates, and publish retries.

## Integration touchpoints
- Source operational systems (ERP, CRM, billing, HR, etc.)
- Data warehouse or lakehouse platforms
- Identity provider and SSO
- Workflow/tasking systems for stewardship
- Event/messaging infrastructure for publish and sync
- Downstream consumers needing canonical master data

## Embedded capabilities
- Import and export pipelines
- Rules engine and decisioning
- Dynamic evaluation and survey engine
- Approval workflows and human-in-the-loop
- Custom fields and extensible attributes
- Search, filters, and saved views
- Audit log and provenance
- Notification preferences and routing
- Notification / messaging system
- Idempotency, outbox, retries, and DLQ

## Failure modes catalog (starter set: 8-12)
- Over-merge of distinct entities from weak matching thresholds.
- Under-merge causing duplicate golden records.
- Survivorship misconfiguration selecting stale or low-trust values.
- Stewardship backlog causing unresolved match candidates.
- Source schema drift breaking ingestion mappings.
- Publish failures creating stale downstream canonical views.
- Feedback loop conflicts when downstream updates re-enter ingestion.
- Unmerge operations not restoring prior lineage correctly.
- Cross-tenant/domain data leakage in shared queues.
- Rule changes producing non-deterministic merge outcomes.

## Observability baseline
### Key traces
- Source ingest to canonical publish flow.
- Match candidate generation to merge decision path.
- Stewardship task assignment to resolution lifecycle.

### Key metrics
- Match precision/recall proxy metrics by entity domain.
- Duplicate rate before and after merge pipeline.
- Stewardship queue depth and age.
- Publish success/failure rate and latency.
- Rule override frequency and unmerge rate.

### Audit events
- Source ingest and normalization outcomes.
- Match candidate creation, scoring, and suppression.
- Merge and unmerge decisions with actor and rationale.
- Survivorship rule changes and version activations.
- Publish, retry, and downstream synchronization outcomes.

## Minimal architecture diagram (C4-ish, 1 page)
- Context: source systems, data stewards, governance team, downstream consumers.
- Containers: ingestion adapters, matching engine, merge rules engine, golden record store, stewardship UI, publishing pipeline, audit store.
- Relationships: ingestion normalizes source records; matching proposes candidates; rules + stewardship resolve entities; golden records published to subscribers.

## Implementation notes and stack variants
- Keep matching strategy configurable per entity domain (deterministic, probabilistic, or hybrid).
- Treat survivorship logic as versioned policy with reproducible outcomes.
- Isolate stewardship operations from bulk ingestion throughput paths.
- Design publish pipeline for replay safety and idempotent downstream sync.
- Example systems: Informatica MDM, Reltio, Talend MDM, SAP Master Data Governance.

## Licensing & source attribution notes
- Content is synthesized from common enterprise MDM architecture patterns.
- Avoid copying proprietary vendor documentation text verbatim.
- Add source attribution in final publish pass.
