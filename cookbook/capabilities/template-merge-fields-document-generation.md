# Template / Merge Fields Document Generation

## What this capability is
- deterministic rendering with versioned templates and secure field substitution.

## When to use it
- Use when systems must generate repeatable documents or messages from business data.
- Common for invoices, contracts, letters, notices, and compliance packets.

## When not to use it
- Do not treat this capability as a broad catch-all; keep adjacent concerns in separate capabilities.

## Core behaviors
- Author creates template and publishes version.
- System validates merge fields against catalog.
- Request references template version and data payload.
- Render worker produces document artifact.
- Artifact is stored, delivered, and audited.
- Failures retry or move to dead-letter with diagnostics.

## Typical components
- Template CRUD and publish endpoints.
- Merge-field discovery endpoint.
- Render endpoint (sync/async modes).
- Artifact retrieval and delivery status endpoints.
- Template editor with preview.
- Merge-field browser and validation hints.
- Render history dashboard.
- Delivery and failure management panel.
- Render worker pool.
- Asset fetch and normalization worker.
- Delivery adapter workers (email/storage/e-sign).
- Retry and dead-letter worker.

## Key data concepts
- TemplateDefinition
- TemplateVersion
- MergeFieldCatalog
- RenderRequest
- RenderArtifact metadata
- DeliveryRecord
- RenderAuditEvent

## Common workflows
- HTML/PDF templating pipeline.
- DOCX merge-field pipeline.
- Guided-interview to template-render flow.
- Inline transactional message rendering.

## Integration touchpoints
- Template CRUD and publish endpoints.
- Merge-field discovery endpoint.
- Render endpoint (sync/async modes).
- Artifact retrieval and delivery status endpoints.

## Risks / failure modes
- Missing merge fields at runtime -> compile-time validation and strict render contracts.
- Template injection risk -> sandboxed template language and escaping policies.
- Asset link failures during render -> preflight asset checks and fallback assets.
- Rendering timeouts for large payloads -> async mode with progress and retries.
- Version drift between template and payload schema -> version negotiation checks.
- Duplicate document generation on retries -> idempotent render request keys.
- Sanitize all user-supplied template inputs.
- Restrict template publish and edit roles.

## Related archetypes
- Payments/Billing: invoice and statement generation.
- CMS/Wiki/KB: templated content publishing.
- Case/Ticket: case summaries and notices.
- DMS: policy-driven document production.

## Related capabilities
- [dynamic-evaluation-survey-engine](dynamic-evaluation-survey-engine.md)
- [custom-fields-extensible-attributes](custom-fields-extensible-attributes.md)
- [approval-workflows-human-in-the-loop](approval-workflows-human-in-the-loop.md)
- [audit-log-provenance](audit-log-provenance.md)


