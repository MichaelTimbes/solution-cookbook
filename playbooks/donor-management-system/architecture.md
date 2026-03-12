# Donor Management Architecture

## Logical Components

- Donor profile service: manages donor identity, household linkage, and stewardship preferences.
- Campaign and segmentation service: manages campaign targeting, segmentation, and outreach context.
- Pledge and contribution lifecycle service: manages pledges, contributions, and fulfillment state.
- Stewardship workflow service: coordinates approvals, follow-up, and donor-care tasks.
- Communication and acknowledgment service: manages outreach, receipts, and acknowledgment generation.
- Search and reporting query service: supports donor lookup, campaign worklists, and fundraising reporting.
- Audit and compliance service: records immutable fundraising and stewardship evidence.
- Integration boundary: synchronizes finance, grant, and adjacent donor systems.

## Workflow / Lifecycle Handshake

- Workflow commonly manages stewardship tasks, approvals, and exception-handling steps around fundraising work.
- Donor, pledge, contribution, and campaign lifecycle services typically own canonical mutation of donor-management state.
- Workflow completion may trigger lifecycle commands such as acknowledge, approve, or advance pledge status, but workflow state does not itself represent authoritative donor-lifecycle truth.

## Read Model Strategy

- Canonical reads usually come from the primary donor, household, campaign, pledge, contribution, and interaction records.
- Operational fundraising lists, stewardship inboxes, and campaign work queues often read from projection or read-model tables tuned for day-to-day fundraising work.
- Search index reads are typically used for donor discovery, relationship lookup, and segmentation retrieval.
- Reporting and fundraising summaries are often served from reporting projections rather than mutable donor tables.

## Typical Modular-Monolith Module Boundaries

These are typical in-process module boundaries for this playbook:
- Donor Profile
- Campaign and Segmentation
- Pledge and Contribution Lifecycle
- Stewardship Workflow
- Communication and Acknowledgment
- Search and Reporting Query
- Audit and Compliance
- Integration Boundary

## Typical V1 Integration Boundaries

- Finance and gift-accounting systems commonly receive contribution and receipt data.
- Messaging and communication providers often deliver outreach, acknowledgments, and reminders.
- Grant, event, or adjacent fundraising systems may exchange donor and campaign context.
- External adapters typically use controlled contracts, idempotent handling, and reconciliation-aware synchronization.