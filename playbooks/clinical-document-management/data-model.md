# Clinical Document Management Data Model

- Core: `ClinicalDocument`, `DocumentVersion`, `PatientReference`, `EncounterReference`
- Metadata: `ClinicalTag`, `DocumentType`, `SensitivityLevel`
- Governance: `AccessPolicySnapshot`, `SignoffRecord`, `AuditEvent`
- Workflow: `ReviewTask`, `StatusTransition`, `NotificationEvent`
- Integration: `ClinicalSyncRecord`, `ExportJob`

Invariants: access checks before retrieval; signoff required for publish states; audit trail immutable.
