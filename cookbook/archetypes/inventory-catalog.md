# Inventory / Catalog Archetype

## What this archetype is / is not
- A system for defining products and variants, managing stock across locations, and exposing sellable catalog views.
- Supports inventory movement, allocation, reservation, and reconciliation workflows.
- Not a full order management or warehouse execution platform, though it integrates with both.

## Typical modules
- Product and variant modeling
- Attributes and taxonomy management
- Pricing and publishability flags
- Stock ledger and movement tracking
- Location and channel availability
- Reservation and allocation engine
- Replenishment and reconciliation
- Catalog search and merchandising views

## Core workflows (top 3–5)
- Create product → define variants → publish to channels
- Receive stock → update on-hand quantities
- Reserve and allocate stock for demand
- Fulfill and decrement stock with movement records
- Reconcile discrepancies and adjust inventory

## Canonical data model skeleton
### Core entities
- Product
- Variant
- AttributeDefinition
- AttributeValue
- InventoryItem
- InventoryLocation
- StockMovement
- Reservation
- Allocation

### Key relations
- Product 1..N Variants
- Variant 0..N AttributeValues
- Variant 1..N InventoryItems (by location)
- InventoryItem N..1 InventoryLocation
- InventoryItem 1..N StockMovements
- Variant 0..N Reservations
- Reservation 0..1 Allocation

### Invariants/constraints
- Variant SKU is unique per tenant or business unit.
- Stock movement ledger is append-only.
- Available stock = on-hand - reserved.
- Negative inventory requires explicit policy and audit.
- Reservation expiry and release are deterministic.

## Permission model patterns
- Separate catalog management from stock adjustment authority.
- Restrict high-risk inventory adjustments with approval threshold.
- Channel-specific publish permissions.
- Read-only external partner access through scoped APIs.
- Full audit for financial-impacting quantity changes.

## Integration touchpoints
- ERP and accounting systems
- Commerce storefront and checkout services
- Warehouse and fulfillment systems
- Supplier and procurement systems
- Pricing and promotion engines
- Analytics and forecasting platforms

## Embedded capabilities
- Custom fields and extensible attributes
- Template and merge fields document generation
- Search, filters, and saved views
- Import and export pipelines
- Rules engine and decisioning
- Notification preferences and routing
- Notification / messaging system
- Audit log and provenance
- Approval workflows and human-in-the-loop
- Idempotency, outbox, retries, and DLQ

## Failure modes catalog (starter set: 8–12)
- Oversell due to stale availability caches.
- Reservation leakage from failed checkout completion.
- Duplicate stock movement events from retry loops.
- Attribute schema changes breaking variant indexing.
- Batch import creating duplicate SKUs.
- Location sync drift between ERP and inventory service.
- Reconciliation adjustments without sufficient audit metadata.
- Publish state mismatch across sales channels.
- Allocation deadlocks under high-concurrency demand.
- Backorder logic applying to ineligible products.

## Observability baseline
### Key traces
- Product publish flow to channel sync.
- Reservation to allocation to fulfillment path.
- Stock adjustment with downstream ERP synchronization.

### Key metrics
- Stock accuracy rate.
- Oversell incident count.
- Reservation expiry and release rates.
- Inventory sync lag by integration.
- Variant query latency for catalog views.

### Audit events
- Product and variant lifecycle changes.
- Attribute schema and value changes.
- Stock adjustments and movement postings.
- Reservation and allocation overrides.
- Publish and unpublish actions by channel.

## Minimal architecture diagram (C4-ish, 1 page)
- Context: merchandising users, warehouse operators, external channels.
- Containers: catalog UI, inventory API, reservation service, movement ledger DB, search index, event bus, integration workers.
- Relationships: API persists catalog and inventory state; workers synchronize channels and ERP/fulfillment systems.

## Implementation notes and stack variants
- Keep inventory ledger separate from denormalized availability views.
- Use asynchronous channel sync with explicit freshness targets.
- Design reservation APIs for idempotent retries.
- Preserve immutable movement history for reconciliation.

## Licensing & source attribution notes
- Content is synthesized from open reference ecosystems and standards patterns.
- Do not reuse restricted vendor prose verbatim.
- Add attribution and license-mode notes on final publication.
