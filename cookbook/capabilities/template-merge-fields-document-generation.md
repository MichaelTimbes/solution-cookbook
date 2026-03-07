# Template / Merge Fields Document Generation

## Problem / when to use
- Use when systems must generate repeatable documents or messages from business data.
- Common for invoices, contracts, letters, notices, and compliance packets.
- Goal: deterministic rendering with versioned templates and secure field substitution.

## Ingredients
### Data model components
- TemplateDefinition
- TemplateVersion
- MergeFieldCatalog
- RenderRequest
- RenderArtifact metadata
- DeliveryRecord
- RenderAuditEvent

### API contracts
- Template CRUD and publish endpoints.
- Merge-field discovery endpoint.
- Render endpoint (sync/async modes).
- Artifact retrieval and delivery status endpoints.

### UI surfaces
- Template editor with preview.
- Merge-field browser and validation hints.
- Render history dashboard.
- Delivery and failure management panel.

### Jobs/workers/async components
- Render worker pool.
- Asset fetch and normalization worker.
- Delivery adapter workers (email/storage/e-sign).
- Retry and dead-letter worker.

## Reference flow (happy path + async path)
1. Author creates template and publishes version.
2. System validates merge fields against catalog.
3. Request references template version and data payload.
4. Render worker produces document artifact.
5. Artifact is stored, delivered, and audited.
6. Failures retry or move to dead-letter with diagnostics.

## Variants
- HTML/PDF templating pipeline.
- DOCX merge-field pipeline.
- Guided-interview to template-render flow.
- Inline transactional message rendering.

## Failure modes & mitigations
- Missing merge fields at runtime → compile-time validation and strict render contracts.
- Template injection risk → sandboxed template language and escaping policies.
- Asset link failures during render → preflight asset checks and fallback assets.
- Rendering timeouts for large payloads → async mode with progress and retries.
- Version drift between template and payload schema → version negotiation checks.
- Duplicate document generation on retries → idempotent render request keys.

## Security/privacy considerations
- Sanitize all user-supplied template inputs.
- Restrict template publish and edit roles.
- Encrypt artifacts at rest and during delivery.
- Apply retention and redaction rules to generated artifacts.

## Observability requirements
### Trace spans
- Template resolution and validation.
- Render execution path.
- Artifact storage and delivery dispatch.
- Retry and dead-letter handling.

### Metrics
- Render success/failure rates.
- Render latency by template.
- Missing-field validation failures.
- Delivery completion rate.
- Dead-letter backlog.

### Structured logs/audit events
- Template lifecycle events.
- Merge-field validation outcomes.
- Render request and artifact metadata.
- Delivery and retry outcomes.

## Testing checklist
### Unit
- Template parser and validator.
- Merge-field resolver.
- Output format normalizers.

### Integration
- End-to-end template publish and render.
- Delivery adapters and status tracking.
- Versioned payload compatibility.

### Failure injection/chaos-lite checks
- Asset service outage.
- Renderer timeout under large payload.
- Duplicate render request replay.

## Operational runbook checklist
- Identify impacted templates and cohorts.
- Validate field catalog and template version mapping.
- Drain and triage dead-letter queue.
- Redrive safe render requests.
- Confirm artifact integrity and delivery outcomes.

## Adoption notes by archetype
- Payments/Billing: invoice and statement generation.
- CMS/Wiki/KB: templated content publishing.
- Case/Ticket: case summaries and notices.
- DMS: policy-driven document production.

## Licensing & source attribution notes
- Keep guidance as original synthesis.
- Attribute open template ecosystem concepts where relevant.
- Avoid verbatim reuse from proprietary docs.
