# CMS / Wiki / Knowledge Base Archetype

## What this archetype is / is not
- A system for creating, structuring, reviewing, publishing, and discovering knowledge content.
- Supports editorial governance, version history, and reusable templates.
- Not a pure document repository or transactional workflow engine, though it integrates with both.

## Typical modules
- Content types and schema builder
- Editor and draft management
- Review and approval pipeline
- Versioning and change history
- Taxonomy, tags, and navigation
- Search and relevance ranking
- Permissions and audience segmentation
- API delivery (headless and/or rendered pages)

## Core workflows (top 3–5)
- Author content → review → publish
- Update published page → version increment → republish
- Apply taxonomy changes and recategorize content
- Template-driven content creation
- Archive or retire stale content

## Canonical data model skeleton
### Core entities
- ContentItem
- ContentVersion
- ContentType
- Template
- TaxonomyTerm
- MediaAsset
- Publication
- EditorialTask
- ContentAuditEvent

### Key relations
- ContentType 1..N ContentItems
- ContentItem 1..N ContentVersions
- ContentItem 0..N TaxonomyTerms
- ContentItem 0..N MediaAssets
- ContentItem 0..N EditorialTasks
- ContentVersion 0..1 Publication snapshot

### Invariants/constraints
- One published version per content item per channel.
- Published versions are immutable snapshots.
- Template references must resolve before publish.
- Taxonomy terms use controlled vocabularies where configured.
- Visibility rules enforced at render and API layers.

## Permission model patterns
- Author, editor, reviewer, publisher, admin role separation.
- Space, collection, or site-scoped permissions.
- Draft-only access for pre-publication content.
- Restricted publishing rights for regulated sections.
- Audit visibility for compliance and content operations.

## Integration touchpoints
- Identity provider and SSO
- Translation/localization services
- Asset storage/CDN
- Search and analytics platforms
- Workflow and notification systems
- External app APIs for headless delivery

## Embedded capabilities
- Template and merge fields document generation
- Approval workflows and human-in-the-loop
- Search, filters, and saved views
- Rules engine and decisioning
- Audit log and provenance
- Notification preferences and routing
- Notification / messaging system
- Import and export pipelines
- Custom fields and extensible attributes

## Failure modes catalog (starter set: 8–12)
- Broken template references preventing render.
- Stale caches serving retired content.
- Publish race creating inconsistent navigation links.
- Permissions leakage via shared links or API tokens.
- Taxonomy changes orphaning content discovery paths.
- Concurrent edits causing lost updates.
- Search index lag hiding newly published content.
- Localization fallback showing wrong language variants.
- Asset deletion breaking embedded media references.
- Workflow misconfiguration bypassing mandatory review.

## Observability baseline
### Key traces
- Draft-to-publish workflow.
- Page render and dependency resolution path.
- Content update to search-index propagation.

### Key metrics
- Publish lead time.
- Content freshness and staleness rate.
- Search click-through and zero-result rate.
- Template render failure rate.
- Permission-denied access attempts.

### Audit events
- Content create, update, publish, unpublish.
- Template changes and dependency updates.
- Taxonomy edits.
- Permission and visibility changes.
- External API token usage and revocation.

## Minimal architecture diagram (C4-ish, 1 page)
- Context: authors, reviewers, readers, downstream apps.
- Containers: editorial UI, content API, publish pipeline, search index, media store/CDN, primary DB, audit store.
- Relationships: editorial actions update content state; pipeline publishes immutable snapshots; APIs and web front ends consume published content.

## Implementation notes and stack variants
- Headless-first architecture supports multiple front-end consumers.
- Separate editorial state from published snapshot state.
- Treat template execution as sandboxed and deterministic.
- Rebuild search indexes asynchronously with freshness SLOs.

## Licensing & source attribution notes
- Content is synthesized from public architecture and OSS patterns.
- Do not copy design-system or vendor docs verbatim.
- Add explicit source/reuse notes during final editorial pass.
