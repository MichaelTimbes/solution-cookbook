# Donor Management Data Model

## Core Aggregate Groups

### Core Domain Objects
- `Donor`
- `Household`
- `Campaign`
- `Pledge`
- `Contribution`
- `Interaction`

### Metadata and Classification
- `Segment`
- `AffinityScore`
- `Preference`

### Access and Governance
- `ConsentRecord`
- `AuditEvent`
- `ApprovalDecision`

### Process and Workflow
- `StewardshipTask`
- `StatusTransition`

### Interchange and Integrations
- `FinanceSyncRecord`
- `ReceiptExport`

## State Authority

- Authoritative domain state typically lives in `Donor`, `Household`, `Campaign`, `Pledge`, `Contribution`, `Interaction`, and `StatusTransition`.
- Supporting authoritative records commonly include `ConsentRecord`, `ApprovalDecision`, `StewardshipTask`, and finance synchronization checkpoints within their own concerns.
- Derived or rebuildable forms often include donor search documents, campaign worklists, stewardship dashboards, notification delivery views, and fundraising reporting summaries.
- Generated acknowledgments or receipts may be authoritative within their artifact boundary, but they typically do not own donor or pledge lifecycle state.
- Search indexes, dashboards, and notifications are projections and should remain conceptually rebuildable from canonical donor-management records.

## Invariants

- Donor merges preserve lineage and historical reference integrity.
- Pledge transitions remain policy-governed and attributable.
- Receipt and acknowledgment outputs map to canonical contribution events.
- Audit and consent history remain immutable and traceable.