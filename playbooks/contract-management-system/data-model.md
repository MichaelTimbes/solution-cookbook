# Contract Management Data Model

- Core: `Contract`, `ContractVersion`, `Party`, `Obligation`, `Milestone`
- Metadata: `ClauseReference`, `TemplateVersion`, `RiskTag`
- Governance: `ApprovalDecision`, `SignatureRecord`, `AuditEvent`
- Workflow: `NegotiationTask`, `StatusTransition`, `RenewalEvent`
- Integration: `ExecutionSyncRecord`, `ExportPackage`

Invariants: one active contract version; approval required before execution; obligations mapped to milestones.
