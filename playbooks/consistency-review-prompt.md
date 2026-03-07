# Playbook Consistency Review Prompt (Reusable)

Use this prompt whenever you want a repeatable, high-consistency review and normalization pass across reference playbooks and variants.

## Prompt

```text
You are reviewing and normalizing the Solution Cookbook playbooks for architectural consistency.

## Scope
- Repository root: <repo-root>
- Reference playbooks (canonical):
  - playbooks/case-ticket-system
  - playbooks/crm
  - playbooks/document-management-system
  - playbooks/workflow-bpm-system
- Variant playbooks to review:
  - <list-variant-folders>

## Goals
1) Preserve canonical architecture shape from the 4 reference playbooks.
2) Keep variant-specific domain language and workflows.
3) Normalize metadata/frontmatter, section structure, subsystem terminology, and diagram naming/linking.
4) Produce deterministic output: same rules, same order, same checks every run.

## Non-Goals
- Do not add new archetypes/capabilities.
- Do not introduce vendor/product-specific implementation detail.
- Do not rewrite unrelated content outside declared scope.

## Canonical Normalization Rules

### A) Guide frontmatter
- Required keys in this order:
  1. playbook
  2. archetype
  3. required-capabilities
  4. optional-capabilities
  5. patterns
- Keep existing domain-appropriate required-capabilities unless explicitly instructed to harmonize by archetype.
- For variant optional-capabilities, use canonical single entry:
  - template-merge-fields-document-generation

### B) Architecture structure
- Enforce these sections in order:
  1. # <Name> Architecture Composition
  2. ## Composition Intent
  3. ## Logical Components
  4. ## Capability Mapping
  5. ## Boundary Principles
  6. ## Interaction Flow
  7. ## Evolution Anchors
  8. ## Diagram References

### C) Terminology normalization
- Prefer these subsystem names consistently:
  - Repository / Core State Store
  - Workflow and Orchestration
  - Notification and Messaging
  - Audit and Provenance
  - Search and Query
  - Integration and data movement

### D) Diagram set and links
- Each playbook must contain and reference exactly:
  - diagrams/system-context.mmd
  - diagrams/container-view.mmd
  - diagrams/lifecycle-flow.mmd
- Replace legacy diagram names in links if present.

### E) Content constraints
- Keep docs concise and architecture-centric.
- Keep lifecycle/workflow states domain-relevant.
- Keep references relative and valid.

## Execution Order
1. Read canonical references first.
2. Review each target variant in place.
3. Apply only required edits (minimal diffs).
4. Validate with a consistency sweep:
   - frontmatter keys exist in correct order
   - optional-capabilities strategy is consistent
   - architecture section order is correct
   - diagram links/names are consistent
5. Return a change summary grouped by playbook.

## Required Output Format
- **Overview**: one short paragraph.
- **What Changed**: bullets grouped by playbook path.
- **Validation Results**: pass/fail bullets for each rule family (A-E).
- **Follow-ups**: optional next-step suggestions.

## Strictness
- If any rule cannot be enforced, explicitly state why and list the exact file paths impacted.
```

## Recommended Invocation Notes

- Keep the variant folder list explicit per run.
- Re-run the same prompt after adding new variants to preserve drift-free metadata and structure.
- If you only want analysis (no edits), add: `Review only; do not modify files.`
