# Data Movement (Import / Export)

## Description of the pattern
Data Movement governs how data crosses system boundaries through ingestion, migration, export, and interchange workflows.

## Why it appears across enterprise systems
Enterprise systems rarely operate in isolation. They must exchange data with partners, legacy systems, and analytics platforms.

## Typical implementation capabilities
- [Import / Export Pipelines](../capabilities/import-export-pipelines.md)
- [Idempotency + Outbox + Retries + DLQ](../capabilities/idempotency-outbox-retries-dlq.md)
- [Audit Log + Provenance](../capabilities/audit-log-provenance.md)

## Example archetypes that rely on it
- [CRM](../archetypes/crm.md)
- [Document Management System](../archetypes/document-management-system.md)
- [Inventory / Catalog](../archetypes/inventory-catalog.md)

## Common failure modes when ignored
- Partial loads and silent data corruption
- Unreliable reconciliation between systems
- Compliance risk from unmanaged export surfaces
