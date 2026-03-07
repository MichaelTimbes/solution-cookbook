# Dynamic Evaluation / Survey Engine

## Problem / when to use
- Use when teams need configurable, versioned questionnaires with branching, scoring, and downstream automation.
- Useful for intake, compliance assessments, onboarding, and inspections.
- Goal: change form behavior quickly without code deploys while preserving historical consistency.

## Ingredients
### Data model components
- FormDefinition (schema/DSL)
- FormVersion
- Question/Field definitions
- Rule and branching conditions
- ResponseSession
- ResponseItem
- Score/Outcome record
- FormAuditEvent

### API contracts
- Form-definition CRUD and publish endpoints.
- Render endpoint returning resolved schema for a version.
- Response submit/save-progress endpoints.
- Evaluation endpoint for scoring and derived outcomes.

### UI surfaces
- Form builder for non-developer authors.
- Runtime form renderer for end users.
- Validation/error guidance views.
- Results and scoring dashboard.

### Jobs/workers/async components
- Rule evaluation worker.
- Scoring and aggregation worker.
- Notification/trigger worker for outcomes.
- Migration worker for schema/version maintenance.

## Reference flow (happy path + async path)
1. Admin authors form and publishes a version.
2. User starts response session and submits answers.
3. Engine evaluates branching and validation rules.
4. Scoring/outcome is computed and persisted.
5. Workflow or notification triggers run based on result.
6. Reports aggregate outcomes by version/cohort.

## Variants
- JSON schema-driven runtime.
- Spreadsheet-authored form definition transformed to runtime schema.
- Low-code builder with plugin question types.
- Stateless render + stateful response processing.

## Failure modes & mitigations
- Version mismatch between rendered form and submit payload → strict version token checks.
- Rule changes invalidating historical scores → immutable versioned scoring logic.
- Partial saves lost on session timeout → autosave and resumable sessions.
- Complex branching causing unreachable questions → static rule analysis pre-publish.
- Injection through rich text fields → sanitize and whitelist input formats.
- Scoring worker backlog delaying outcomes → queue monitoring and scaling policy.

## Security/privacy considerations
- Encrypt sensitive responses at rest.
- Restrict authoring/publish permissions.
- Enforce data retention and deletion by policy.
- Redact sensitive fields in logs and exports.

## Observability requirements
### Trace spans
- Form render and schema resolution.
- Response submission and validation path.
- Rule evaluation and scoring path.
- Outcome trigger execution.

### Metrics
- Form completion rate.
- Abandonment rate by step.
- Validation error frequency by question.
- Scoring latency.
- Publish-to-first-response lead time.

### Structured logs/audit events
- Form schema and version lifecycle events.
- Rule evaluation outcomes.
- Response submission and correction events.
- Outcome-trigger and integration events.

## Testing checklist
### Unit
- Rule evaluator correctness.
- Scoring calculations.
- Version-compatibility validators.

### Integration
- End-to-end render/submit/score flow.
- Save-progress and resume behavior.
- Trigger integration for outcome workflows.

### Failure injection/chaos-lite checks
- Mid-session network interruption.
- Rule engine delay under load.
- Backward-incompatible schema change simulation.

## Operational runbook checklist
- Verify publish state and active version routing.
- Monitor validation errors and abandonment spikes.
- Triage scoring delays and queue backlogs.
- Roll back problematic form version if needed.
- Reprocess affected response sessions where safe.

## Adoption notes by archetype
- Case/Ticket: dynamic intake and triage forms.
- CIAM: risk and assurance questionnaires.
- CRM: qualification and onboarding checklists.
- Workflow/BPM: decision inputs for routing.

## Licensing & source attribution notes
- Keep this page as original synthesis.
- Attribute OSS form engines and standards where applicable.
- Do not copy proprietary builder documentation text.
