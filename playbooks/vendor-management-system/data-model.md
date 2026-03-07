# Vendor Management Data Model

- Core: `Vendor`, `VendorContact`, `Qualification`, `ContractReference`, `PerformanceReview`
- Metadata: `RiskScore`, `Category`, `RegionTag`
- Governance: `PolicyDecision`, `ApprovalDecision`, `AuditEvent`
- Workflow: `OnboardingTask`, `RenewalTask`, `StatusTransition`
- Integration: `ProcurementSyncRecord`, `ExportPackage`

Invariants: vendor status transitions require policy validation; risk changes are auditable; closure requires evidence completeness.
