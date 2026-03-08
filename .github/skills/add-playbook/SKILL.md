---
name: add-playbook
description: Use this skill when the user asks to add, scaffold, or create a new playbook in the solution-cookbook repository. This skill creates a playbook from the template, keeps it aligned to an existing archetype and reference playbook, updates the playbook index, and validates links, metadata, and file structure.
---

# Add a New Playbook

Use this skill to create a new playbook in the `solution-cookbook` repository with the correct file structure, metadata, links, diagrams, and index entry.

## Repository Constraint

- Apply this skill only when the active repository is `solution-cookbook`.
- Do not generalize this skill to other repositories.
- Keep changes inside `playbooks/**` unless explicitly asked to update repository-level docs.
- Treat the cookbook as the source of truth:
  - `cookbook/archetypes/`
  - `cookbook/capabilities/`
  - `cookbook/foundational-patterns/`
  - `playbooks/_template/`

## Purpose

A playbook is a concrete implementation form of an existing archetype.

Use this skill to create either:

- a **reference** playbook, which acts as the canonical baseline for an archetype
- a **variant** playbook, which adapts an existing reference playbook to a specific domain or operational context

## Classification Rules

### Reference playbook
A `reference` playbook is the baseline implementation for an archetype.

- Only create a `reference` playbook if no canonical reference playbook already exists for that archetype.
- A reference playbook should stay close to the generic archetype shape.
- A reference playbook should not be overly domain-specific.

### Variant playbook
A `variant` playbook is a domain-specific form of an archetype.

- A variant must be based on an existing reference playbook.
- A variant should preserve the core architectural shape of its reference playbook.
- A variant should mainly change:
  - domain language
  - workflows
  - lifecycle states
  - compliance/governance requirements
  - integration boundaries
- A variant should not invent a fundamentally different architecture unless clearly justified.

## Inputs Required

Collect these inputs before creating files.

### Required for all playbooks
1. `playbook_slug`
   - kebab-case folder name
   - example: `vendor-risk-management-system`

2. `playbook_title`
   - human-readable title
   - example: `Vendor Risk Management System`

3. `archetype_slug`
   - must correspond to an existing archetype file in `cookbook/archetypes/`
   - example: `crm`, `case-ticket-system`

4. `classification`
   - `reference` or `variant`

5. `short_description`
   - one sentence for the playbook catalog

6. `required_capabilities`
   - ordered list of capability slugs
   - each slug must resolve to an existing page in `cookbook/capabilities/`

7. `optional_capabilities`
   - ordered list of capability slugs
   - may be empty: `[]`

8. `patterns`
   - ordered list of foundational pattern slugs
   - each slug must resolve to an existing page in `cookbook/foundational-patterns/`

### Required for variant playbooks
9. `based_on_reference_playbook`
   - required when `classification = variant`
   - must point to an existing reference playbook under `playbooks/`

### Optional
10. `related_archetypes`
   - optional ordered list of archetype slugs

If any required input is missing, ask concise follow-up questions before editing.

## Files to Create

Create a new folder:

- `playbooks/<playbook_slug>/`

Create these files by copying and adapting templates from `playbooks/_template/`:

- `guide.md`
- `architecture.md`
- `workflows.md`
- `data-model.md`
- `failure-modes.md`

Create the diagrams folder and files:

- `diagrams/system-context.mmd`
- `diagrams/container-view.mmd`
- `diagrams/lifecycle-flow.mmd`

## Authoring Rules

### General rules
- Keep content technology-neutral.
- Keep content vendor-neutral.
- Use terminology consistent with the cookbook.
- Do not invent new archetypes.
- Do not invent new capabilities or foundational patterns unless explicitly asked.
- If a requested capability or pattern does not exist, call it out explicitly and keep placeholder text minimal.
- Variants must preserve the core architecture of the reference playbook.

### Link rules
- Use links under `../../cookbook/...`
- Do not use `cookbook-v1`
- All capability, archetype, and foundational pattern links must resolve to real files.
- All local playbook links must resolve to real files.

## File-Specific Rules

### 1) `guide.md`
Use frontmatter keys in this exact order:

1. `playbook`
2. `archetype`
3. `required-capabilities`
4. `optional-capabilities`
5. `patterns`

The guide must:
- identify the problem space
- identify the archetype
- identify foundational patterns
- identify required capabilities
- identify optional capabilities if any
- explain the role of the playbook
- link to:
  - `architecture.md`
  - `workflows.md`
  - `data-model.md`
  - `failure-modes.md`
  - all 3 diagrams

If `classification = variant`, the guide must explicitly state that the playbook is based on `based_on_reference_playbook`.

### 2) `architecture.md`
Use this exact section order:

1. `## Composition Intent`
2. `## Logical Components`
3. `## Capability Mapping`
4. `## Boundary Principles`
5. `## Interaction Flow`
6. `## Evolution Anchors`
7. `## Diagram References`

Rules:
- Keep sections architecture-centric
- Make component-to-capability mapping explicit
- Keep boundaries explicit:
  - repository/core state
  - workflow and orchestration
  - notification and messaging
  - audit and provenance
  - integration boundaries
- Include links to the 3 canonical diagram files

### 3) `workflows.md`
- Include at least 3 concrete workflows
- For each workflow include:
  - ordered stages
  - linked capabilities
  - operational or policy notes
- Keep workflows domain-specific
- Avoid product or tool implementation details

### 4) `data-model.md`
- Define canonical entity groups
- Define key relationships
- Define invariants
- Define governance or lifecycle notes where relevant
- Keep entities aligned to workflows and capabilities

### 5) `failure-modes.md`
- Use either:
  - a structured table, or
  - structured bullets matching existing repo style
- Each failure mode should include:
  - cause
  - impact
  - mitigation
- Tie mitigations to capabilities or patterns where possible

### 6) Diagrams
- Ensure all 3 diagram files exist
- Keep names exactly as:
  - `system-context.mmd`
  - `container-view.mmd`
  - `lifecycle-flow.mmd`
- Do not invent alternate diagram filenames
- Initial content may be minimal, but must be relevant to the playbook

## Index Update

Update `playbooks/index.md`.

### Playbook Catalog
Add one row under the existing playbook catalog using repository style:

- Title/link column:
  - `[<playbook_title>](<playbook_slug>/guide.md)`
- Archetype column:
  - use existing index wording and style
- Description column:
  - use `short_description`

### Reference playbooks
If `classification = reference`, add the playbook to the existing reference playbooks section using current repository style.

### Important
- Preserve the current index structure and headings.
- Do not rewrite the whole file unnecessarily.
- Insert new content in the correct section only.

## Validation Checklist

Before finalizing, verify:

- New folder exists at `playbooks/<playbook_slug>/`
- All 5 markdown files exist and are populated
- All 3 diagram files exist with canonical names
- `guide.md` frontmatter keys are present and ordered correctly
- `guide.md` metadata matches the actual playbook content
- No `cookbook-v1` links remain in newly created files
- Capability, pattern, and archetype links resolve under `../../cookbook/...`
- `playbooks/index.md` contains the new catalog row
- If `classification = reference`, the reference playbook section is updated
- Links in `guide.md` to local files are valid
- If `classification = variant`, the playbook clearly references `based_on_reference_playbook`
- If `classification = variant`, the playbook preserves the core architecture of the reference playbook

## Execution Sequence

1. Collect and confirm required inputs.
2. Validate that `archetype_slug` exists in `cookbook/archetypes/`.
3. If `classification = variant`, validate that `based_on_reference_playbook` exists.
4. Create `playbooks/<playbook_slug>/` and `diagrams/`.
5. Scaffold all required files from `_template`.
6. Fill in playbook-specific content and links.
7. Update `playbooks/index.md`.
8. Run the validation checklist.
9. Report results.

## Output Format

Return results in this format:

- **Overview**: one short paragraph
- **Files Created/Updated**: grouped by folder
- **Validation Results**: pass/fail bullets for each checklist item
- **Follow-ups**: optional next steps

## Strictness

- If required inputs are incomplete, pause and ask only for the missing fields.
- If any required link target does not exist, call it out explicitly.
- Do not create extra pages, extra diagrams, or extra categories unless the user asks.
- Do not silently widen scope.
- Prefer consistency with the cookbook over novelty.