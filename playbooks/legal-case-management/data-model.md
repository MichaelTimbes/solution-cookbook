# Legal Case Management Data Model

## Core Aggregate Groups

- `LegalCase`, `Party`, `Counsel`, `CaseTask`
- `EvidenceReference`, `DocumentLink`, `CustodyEvent`
- `AccessPolicySnapshot`, `ApprovalDecision`, `AuditEvent`
- `Deadline`, `StatusTransition`, `NotificationEvent`
- `ExternalFilingRecord`, `ExportPackage`

## Key Relationships

- One legal case has many tasks, deadlines, and evidence references.
- One evidence reference has many custody events.
- Approval decisions reference specific case transitions.

## Invariants

- Custody events are append-only.
- Privileged access is policy-gated and audited.
- Case closure requires required review checkpoints.
