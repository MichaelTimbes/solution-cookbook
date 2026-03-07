# Compliance Case Management Architecture

## Logical Components

- Compliance intake boundary.
- Policy classification and scoring service.
- Case investigation domain service.
- Remediation workflow service.
- Evidence and control linkage service.
- Search and reporting service.
- Notification and escalation service.
- Audit and compliance evidence service.

## Boundary Principles

- Keep policy logic externalized and versioned.
- Keep evidence references immutable.
- Keep remediation workflow separated from ingestion.
- Keep reporting projections separated from canonical case state.
