# Donor Management Data Model

- Core: `Donor`, `Household`, `Campaign`, `Pledge`, `Contribution`, `Interaction`
- Metadata: `Segment`, `AffinityScore`, `Preference`
- Governance: `ConsentRecord`, `AuditEvent`, `ApprovalDecision`
- Workflow: `StewardshipTask`, `StatusTransition`
- Integration: `FinanceSyncRecord`, `ReceiptExport`

Invariants: donor merges preserve lineage; pledge transitions are policy-governed; receipts map to contribution events.
