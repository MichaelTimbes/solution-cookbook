# CRM Archetype

## What this archetype is / is not
- A system for managing account, contact, lead, opportunity, and customer interaction lifecycles.
- Optimized for sales and service pipeline visibility, handoffs, and customer history continuity.
- Not a full ERP, billing engine, or content management suite, though it integrates with all three.

## Typical modules
- Accounts and contacts
- Leads and qualification
- Opportunities and pipeline stages
- Activities (tasks, calls, meetings, emails)
- Quotes and handoff to order and billing
- Service cases and knowledge links
- Reports and dashboards
- Administration (fields, workflows, permissions)

## Core workflows (top 3–5)
- Lead capture → qualification → conversion
- Opportunity progression → quote generation → close won or lost
- Account and contact enrichment over lifecycle
- Activity logging and follow-up management
- Case handoff from support to account teams and back

## Canonical data model skeleton
### Core entities
- Account
- Contact
- Lead
- Opportunity
- Activity
- Quote
- Case
- User
- Team

### Key relations
- Account 1..N Contacts
- Account 1..N Opportunities
- Lead 0..1 Opportunity (post-conversion)
- Opportunity 1..N Activities
- Opportunity 0..N Quotes
- Account 0..N Cases
- User and Team ownership across Lead, Opportunity, Case

### Invariants/constraints
- Converted leads are immutable except for audit-safe corrections.
- Opportunity stage transitions follow an allowed state graph.
- Exactly one active owner at a time per lead, opportunity, and case.
- PII fields require masking and export controls.
- Merge operations preserve source record lineage.

## Permission model patterns
- Role-based baseline (sales rep, manager, support, admin).
- Ownership-based access for record-level visibility.
- Team and territory overlays for shared pipelines.
- Field-level restrictions for sensitive PII.
- Audit-only roles for compliance and forensics.

## Integration touchpoints
- Email and calendar providers
- Telephony and contact center systems
- Billing and order management
- Marketing automation
- Identity provider and SSO
- Data warehouse and analytics stack

## Embedded capabilities
- Custom fields and extensible attributes
- Dynamic evaluation and survey engine
- Template and merge fields document generation
- Search, filters, and saved views
- Approval workflows and human-in-the-loop
- Notification preferences and routing
- Notification / messaging system
- Import and export pipelines
- Audit log and provenance
- Rules engine and decisioning
- Idempotency, outbox, retries, and DLQ

## Failure modes catalog (starter set: 8–12)
- Duplicate account and contact creation due to weak matching rules.
- Lead conversion race conditions producing duplicate opportunities.
- Stage drift from ad-hoc updates outside approved transitions.
- Ownership reassignment loops during territory changes.
- Saved views exposing rows beyond intended scope.
- Custom field type changes breaking historical data reads.
- Integration lag causing stale billing and order status in CRM.
- Notification storms from misordered automation rules.
- Import jobs partially applying with poor retry semantics.
- Audit gaps during bulk updates performed by background jobs.

## Observability baseline
### Key traces
- Lead-to-opportunity conversion journey.
- Opportunity update plus downstream quote sync.
- Case escalation with notification fan-out.

### Key metrics
- Lead conversion rate and median conversion time.
- Opportunity stage aging by stage.
- Assignment latency after record creation.
- Automation error rate per rule.
- Integration sync lag (source timestamp to CRM timestamp).

### Audit events
- Record created, updated, deleted for all core entities.
- Ownership and permission changes.
- Stage transition with actor and prior and new state.
- Bulk import and export operations.
- Schema and custom-field definition changes.

## Minimal architecture diagram (C4-ish, 1 page)
- Context: CRM users, external systems (email, billing, identity, analytics).
- Containers: Web UI, API service, workflow and rules worker, integration worker, primary DB, search index, event bus.
- Key relationships: UI→API, API→DB, API→event bus, workers→external systems.

## Implementation notes and stack variants
- Monolith-first is acceptable if eventing boundaries are explicit.
- Prefer append-only audit trail plus change-data-capture for integrations.
- Keep search index eventually consistent with clear freshness SLAs.
- Separate synchronous validation from asynchronous enrichment.

## Licensing & source attribution notes
- Content is synthesized from public references and standards-oriented material.
- Do not reproduce vendor documentation text verbatim.
- Add source links and reuse mode labels when this page is finalized.
