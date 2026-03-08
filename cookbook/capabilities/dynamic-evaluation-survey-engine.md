# Dynamic Evaluation / Survey Engine

## What this capability is
- change form behavior quickly without code deploys while preserving historical consistency.

## When to use it
- Use when teams need configurable, versioned questionnaires with branching, scoring, and downstream automation.
- Useful for intake, compliance assessments, onboarding, and inspections.

## When not to use it
- Do not treat this capability as a broad catch-all; keep adjacent concerns in separate capabilities.

## Core behaviors
- Admin authors form and publishes a version.
- User starts response session and submits answers.
- Engine evaluates branching and validation rules.
- Scoring/outcome is computed and persisted.
- Workflow or notification triggers run based on result.
- Reports aggregate outcomes by version/cohort.

## Typical components
- Form-definition CRUD and publish endpoints.
- Render endpoint returning resolved schema for a version.
- Response submit/save-progress endpoints.
- Evaluation endpoint for scoring and derived outcomes.
- Form builder for non-developer authors.
- Runtime form renderer for end users.
- Validation/error guidance views.
- Results and scoring dashboard.
- Rule evaluation worker.
- Scoring and aggregation worker.
- Notification/trigger worker for outcomes.
- Migration worker for schema/version maintenance.

## Key data concepts
- FormDefinition (schema/DSL)
- FormVersion
- Question/Field definitions
- Rule and branching conditions
- ResponseSession
- ResponseItem
- Score/Outcome record
- FormAuditEvent

## Common workflows
- JSON schema-driven runtime.
- Spreadsheet-authored form definition transformed to runtime schema.
- Low-code builder with plugin question types.
- Stateless render + stateful response processing.

## Integration touchpoints
- Form-definition CRUD and publish endpoints.
- Render endpoint returning resolved schema for a version.
- Response submit/save-progress endpoints.
- Evaluation endpoint for scoring and derived outcomes.

## Risks / failure modes
- Version mismatch between rendered form and submit payload -> strict version token checks.
- Rule changes invalidating historical scores -> immutable versioned scoring logic.
- Partial saves lost on session timeout -> autosave and resumable sessions.
- Complex branching causing unreachable questions -> static rule analysis pre-publish.
- Injection through rich text fields -> sanitize and whitelist input formats.
- Scoring worker backlog delaying outcomes -> queue monitoring and scaling policy.
- Encrypt sensitive responses at rest.
- Restrict authoring/publish permissions.

## Related archetypes
- Case/Ticket: dynamic intake and triage forms.
- CIAM: risk and assurance questionnaires.
- CRM: qualification and onboarding checklists.
- Workflow/BPM: decision inputs for routing.

## Related capabilities
- [rules-engine-decisioning](rules-engine-decisioning.md)
- [approval-workflows-human-in-the-loop](approval-workflows-human-in-the-loop.md)
- [template-merge-fields-document-generation](template-merge-fields-document-generation.md)
- [custom-fields-extensible-attributes](custom-fields-extensible-attributes.md)


