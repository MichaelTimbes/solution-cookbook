# Compliance Case Management Data Model

## Core Aggregate Groups

- `ComplianceCase`, `Control`, `Policy`, `Finding`
- `InvestigationTask`, `RemediationTask`, `ApprovalDecision`
- `EvidenceReference`, `AssessmentRecord`, `AuditEvent`
- `StatusTransition`, `EscalationEvent`, `NotificationEvent`
- `RegulatoryExport`

## Key Relationships

- One compliance case can have many findings and remediation tasks.
- One finding maps to one or more controls and policy clauses.
- Approval decisions gate remediation closure.

## Invariants

- Policy and control references are versioned.
- Audit records remain immutable.
- Case closure requires remediation verification.
