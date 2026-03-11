# Artifact Repository

primary-role: execution-transport
secondary-role: governance-trust

## What this capability is
- Provides the authoritative management layer for file-like artifacts and their structured metadata when artifacts must be attached to business records.
- Coordinates artifact registration, versioning, linkage, retrieval, integrity controls, and retention behavior.
- Separates artifact management behavior from storage product selection so implementations can use different persistence technologies without changing system contracts.

## When to use it
- Use when systems must durably store and retrieve uploaded or generated artifacts (for example, signed PDFs, redlines, evidence files, screenshots, and attachments) tied to domain records.
- Use when artifacts require version history, integrity validation, and policy-aligned retention handling.
- Use when downstream systems need artifact lifecycle events for indexing, preview generation, or audit enrichment.

## When not to use it
- Do not use as the domain lifecycle engine for parent records; business state remains owned by the domain model.
- Do not use as the workflow engine; orchestration and approvals belong in workflow-oriented capabilities.
- Do not use as the search index; retrieval metadata may be emitted to indexing capabilities, but this capability does not replace search.
- Do not treat this as authorization policy itself; access decisions come from identity and policy layers.
- Do not frame this page as generic storage infrastructure documentation; this is system-level artifact management behavior.

## Core behaviors
- Upload and register an artifact with canonical metadata.
- Version artifacts while preserving lineage and immutable historical references.
- Attach and detach artifacts to parent records through explicit linkage rules.
- Retrieve and download artifacts by stable identifiers and parent context.
- Validate integrity through content hash and consistency checks.
- Archive, retain, or dispose artifacts according to policy and retention class.
- Emit artifact events for indexing, preview/rendition generation, and audit pipelines.

## Typical components
- Artifact metadata registry for authoritative artifact records and linkage state.
- Blob/object storage adapter for binary payload persistence.
- Version manager for controlled replacement and historical retrieval.
- Attachment/link service for parent-child association rules.
- Integrity service for hash computation and verification.
- Retention and archival worker for policy-driven lifecycle execution.
- Preview/rendition hook for asynchronous derived-file generation.
- Retrieval/download API for secure artifact access.

## Key data concepts
- Artifact record (id, parent reference, status, created metadata).
- Artifact version (version id, sequence, supersedes relation).
- Parent record linkage (entity type, entity id, relation semantics).
- Content hash and integrity state.
- MIME/content type and file characteristics.
- Retention class and disposal policy reference.
- Storage location reference for binary content.
- Preview/rendition reference for derived outputs.

## Common workflows
- User uploads a file, system validates it, stores content, registers metadata, and links the artifact to a parent record.
- User replaces an artifact with a new version while preserving previous versions for traceability.
- System-generated document is stored as a derived artifact and linked to the originating record.
- Consumer retrieves artifacts by parent record with pagination and version-aware selection.
- Retention job archives or disposes eligible artifacts and records lifecycle outcomes.

## Integration touchpoints
- Domain lifecycle modules that own parent record state and trigger artifact actions.
- Document/template generation services producing derived artifacts.
- Search indexing services consuming artifact metadata events.
- Audit logging services capturing artifact creation, linkage, access, and retention actions.
- External signature providers for signed artifact ingestion and verification metadata.
- Import/export pipelines for bulk artifact migration and reconciliation.

## Risks / failure modes
- Orphaned blobs when binary content exists without a valid metadata record or parent link.
- Metadata/blob mismatch when registry state diverges from stored binary payloads.
- Missing retention enforcement leading to compliance and cost exposure.
- Duplicate or conflicting versions causing ambiguous authoritative artifacts.
- Broken parent-child linkage that hides critical supporting evidence.
- Unauthorized access to artifacts when access checks are bypassed or inconsistently applied.
- Checksum/integrity drift caused by corruption, incorrect migration, or invalid rewrite behavior.

## Related archetypes
- Document Management System.
- Case / Ticket System.
- Workflow / BPM System.
- CRM.

## Related capabilities
- [template-merge-fields-document-generation](template-merge-fields-document-generation.md)
- [audit-log-provenance](audit-log-provenance.md)
- [import-export-pipelines](import-export-pipelines.md)
- [search-index](search-index.md)
- [custom-fields-extensible-attributes](custom-fields-extensible-attributes.md)
