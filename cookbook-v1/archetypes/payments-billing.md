# Payments / Billing Archetype

## What this archetype is / is not
- A system that manages subscriptions, invoices, collections, retries, and account financial state.
- Supports recurring and event-driven billing with payment-provider integrations.
- Not a full general ledger and accounting suite, though it exports accounting events.

## Typical modules
- Customer account and billing profile
- Product plans, prices, and usage dimensions
- Subscription lifecycle management
- Invoicing and adjustments
- Payment method vault and token references
- Collections, retries, and dunning
- Entitlements and status propagation
- Reconciliation and reporting

## Core workflows (top 3–5)
- Subscription activation, change, and cancel
- Bill run generation and invoice issuance
- Payment attempt, retry schedule, and dunning escalation
- Refund and credit memo handling
- End-of-period reconciliation

## Canonical data model skeleton
### Core entities
- Billing account
- Subscription
- Plan and price
- Invoice
- Invoice line item
- Payment attempt
- Payment method token reference
- Dunning policy
- Credit and refund record

### Key relations
- Billing account 1..N Subscriptions
- Subscription 1..N Invoices
- Invoice 1..N Line items
- Invoice 0..N Payment attempts
- Billing account 0..N Payment methods
- Billing account N..1 Dunning policy version

### Invariants/constraints
- Invoice totals equal line-item aggregate plus taxes and adjustments.
- Payment attempt idempotency scope must be explicit.
- Subscription status and entitlement status must not diverge beyond SLA.
- Refunds and credits must reference original financial events.
- Currency and tax region constraints must be enforced per account.

## Permission model patterns
- Segregation between support operations and financial operations.
- Least-privilege access to payment method references.
- Dual-control for high-risk actions (write-off and refund above threshold).
- Read-only compliance roles for financial audit views.

## Integration touchpoints
- Payment service providers
- Tax calculation providers
- ERP and accounting systems
- CRM and entitlement systems
- Notification channels (email, SMS, push)
- Fraud and risk systems

## Embedded capabilities
- Idempotency, outbox, retries, and DLQ
- Approval workflows and human-in-the-loop
- Template and merge fields document generation
- Notification preferences and routing
- Search, filters, and saved views
- Audit log and provenance
- Rules engine and decisioning
- Import and export pipelines
- Custom fields and extensible attributes

## Failure modes catalog (starter set: 8–12)
- Duplicate charges due to missing or incorrect idempotency keys.
- Webhook ordering gaps causing stale invoice status.
- Retry storms from overly aggressive retry policy.
- Dunning logic misfire on already-settled invoices.
- Currency rounding inconsistencies between systems.
- Entitlement not revoked after terminal delinquency.
- Partial refund without corresponding ledger adjustment.
- Provider timeout with ambiguous payment outcome.
- DLQ growth masking systemic downstream failures.
- Backfill and replay generating duplicate financial events.

## Observability baseline
### Key traces
- Invoice generation to payment attempt journey.
- Payment webhook ingestion and invoice state update.
- Dunning escalation and notification fan-out.

### Key metrics
- Authorization success rate.
- Collection rate and involuntary churn.
- Retry success by attempt number.
- Dunning stage population.
- Invoice aging buckets.

### Audit events
- Subscription lifecycle changes.
- Invoice creation, adjustment, and void actions.
- Payment attempt outcomes and retries.
- Refund and credit issuance.
- Dunning policy changes and manual overrides.

## Minimal architecture diagram (C4-ish, 1 page)
- Context: customer, finance operator, payment provider, ERP.
- Containers: billing API, pricing engine, invoice engine, collections worker, webhook ingestor, DB, event bus.
- Relationships: write model emits events; async workers handle retries, dunning, and downstream sync.

## Implementation notes and stack variants
- Keep provider-agnostic payment abstraction at the domain boundary.
- Isolate financial state transitions behind a deterministic state machine.
- Use outbox pattern for all external financial side effects.
- Preserve immutable event history for reconciliation and dispute handling.

## Licensing & source attribution notes
- Content is synthesized from OSS billing and public API guidance.
- Reuse patterns, not verbatim vendor documentation.
- Attach source-level attribution and license mode on final publish.