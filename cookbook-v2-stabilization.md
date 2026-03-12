# Solution Cookbook V2 Stabilization

## Purpose

This document captures the current V2 stabilization direction for the `solution-cookbook` repository.

The goal is to bring the cookbook to a **stable, usable V2** that can be exercised repeatedly for architecture planning before any major framework revisions are considered.

This is **not** a redesign brief.  
This is a stabilization brief.

---

## Current Repository Model

The cookbook is organized around three primary knowledge layers:

### Archetypes
High-level system shapes.

Examples:
- case-ticket-system
- crm
- document-management-system
- workflow-bpm-system

### Capabilities
Reusable architectural behaviors that recur across multiple system types.

Examples:
- query-filtering
- saved-views
- search-index
- human-communication
- notification-preferences-routing
- notification-messaging-system
- audit-log-provenance
- artifact-repository

### Playbooks
Domain-specific realizations that combine archetypes and capabilities into concrete reference system designs.

Examples:
- contract-management-system
- support-ticket-system
- donor-management-system
- approval-workflow-system

---

## V2 Philosophy

V2 should preserve the current cookbook model and improve it through **small, targeted refinements**.

The cookbook should remain:

- technology-neutral
- vendor-neutral
- deployment-neutral
- useful to both humans and AI-assisted architecture planning

The cookbook should **describe recurring structures and boundaries**, not enforce architecture dogma.

It should help answer:

- what kind of system is this?
- what capabilities typically appear inside it?
- where does truth likely live?
- what is likely derived?
- what boundaries commonly matter?

It should **not** try to prescribe:

- microservices vs monolith
- event bus vs direct invocation
- database product choices
- infrastructure stack choices

---

## What Is Already Working Well

The following parts of the cookbook should remain stable in V2:

### 1. Archetype / Capability / Playbook structure
This three-layer model is working and should not be rethought in V2.

### 2. Reference playbook -> variant playbook model
The reference-vs-variant distinction is clear and useful.

### 3. Recent capability splits
These should remain in place:

- query-filtering
- saved-views
- search-index
- human-communication
- notification-preferences-routing
- notification-messaging-system

These splits materially improved reasoning during architecture synthesis.

### 4. Lightweight role metadata
Capability metadata such as:

- `primary-role`
- `secondary-role`

should remain lightweight and helpful, not expanded into a heavy taxonomy.

### 5. Negative boundary language
Capability pages have been especially useful where they clearly state what the capability is **not** responsible for.

Examples:
- query-filtering is not an index
- saved-views is not a query engine
- search-index is not business-policy filtering logic
- notification routing is distinct from notification delivery

This pattern should be preserved.

### 6. Architecture synthesis as the primary validation loop
The cookbook is validated by using it in architecture-planning exercises.

That remains the main test of usefulness.

---

## Recent Changes Already Completed

The following changes have already been made and should be treated as part of V2:

### Capability improvements
- split search / filter / saved-view concerns into separate capabilities
- split communication / notification concerns into separate capabilities
- normalized capability pages to a consistent structure
- introduced lightweight role metadata on selected capability pages
- preserved legacy combined capability pages with notices pointing to replacement pages

### Artifact capability
- added `artifact-repository` as a reusable capability
- clarified that artifact management is a system behavior, not just low-level storage
- artifact metadata and lineage are distinct from business lifecycle state

### Template / playbook improvements
The playbook template and `contract-management-system` playbook have been improved with sections such as:

- Capability Ownership Map
- State Authority
- Workflow / Lifecycle Handshake
- Read Model Strategy
- Communication Boundary Notes
- Artifact Handling Model

These additions materially improved architecture synthesis quality.

---

## What Architecture Synthesis Testing Showed

The cookbook has been tested through repeated architecture-planning exercises, especially against `contract-management-system`.

The main findings:

### What improved significantly
- authoritative vs derived state became much clearer
- workflow no longer drifted into becoming the system of record
- artifact handling became more coherent
- module boundaries became more deterministic
- search, notification, and integration concerns were handled as derived/projection/boundary concerns rather than canonical domain state

### What still caused ambiguity
- clause definition vs clause instance modeling
- obligation derivation rules
- workflow granularity in v1
- minimal v1 read models
- exact modular-monolith interpretation
- minimal v1 integration boundary set

The remaining gaps are now mostly **domain modeling and playbook precision issues**, not high-level framework issues.

---

## V2 Stabilization Goal

V2 should make the cookbook stable enough to:

- drive repeated architecture synthesis exercises
- reduce architectural guessing
- preserve clean boundaries between canonical state, derived state, process control, artifacts, and integrations
- avoid major structural framework changes

V2 is complete when the cookbook can be used repeatedly to produce credible system architectures across multiple archetypes without major ambiguity.

---

## Remaining V2 Work

The remaining work should focus on **playbook precision**, not new framework invention.

### 1. Tighten the canonical domain model in contract-management-system
Clarify the core authoritative model, especially:

- Contract
- ContractVersion
- ClauseDefinition
- ClauseInstance
- Obligation

Need:
- clearer relationship between library clauses and version-bound clause instances
- clearer relationship between clause instances and obligations

### 2. Clarify typical workflow units
Document likely v1 workflow scopes such as:

- review workflow per contract version
- approval workflow per lifecycle gate
- amendment workflow per lifecycle branch
- renewal workflow per lifecycle trigger

Need:
- clearer guidance on workflow granularity
- preserve lifecycle ownership of canonical state

### 3. Clarify minimal v1 read models
Document the common v1 projections for contract systems, such as:

- contract list projection
- obligation queue projection
- approval inbox projection
- audit timeline projection
- search index documents

Need:
- clearer guidance on what is typically projected in v1
- avoid over-building read models

### 4. Clarify modular-monolith interpretation
Document likely in-process module boundaries for v1 contract systems, such as:

- Contract Lifecycle
- Authoring / Intake
- Artifact Repository
- Review Collaboration
- Approval Orchestration
- Policy Decisioning
- Obligations & Renewals
- Query Workspace
- Search Projection
- Notification Policy & Delivery
- Integration Hub
- Audit & Provenance

Need:
- more deterministic module interpretation
- no microservice implication

### 5. Clarify minimal v1 integration contracts
Document the expected minimum external boundaries in contract systems, such as:

- e-sign callback boundary
- downstream export / sync boundary
- integration checkpoints / reconciliation

Need:
- a small, practical v1 integration envelope
- avoid speculative integration sprawl

---

## What Should NOT Be Done In V2

The following should be deferred.

### Do not add new archetypes
No major archetype expansion in V2.

### Do not redesign the capability model
The capability model is working well enough for V2.

### Do not introduce a heavy taxonomy framework
Role metadata should remain lightweight.

### Do not introduce architecture dogma
Avoid introducing:
- required service decomposition rules
- required event-driven rules
- prescribed technology choices

### Do not mass-edit every playbook immediately
Changes should be validated on the template and a small number of representative playbooks before propagating.

### Do not treat CLM-specific improvements as universal truth
The `contract-management-system` playbook is being used as a stress test, not as the universal model for all playbooks.

---

## Why Contract Management Is Being Used As A Stress Test

`contract-management-system` has been the primary V2 test case because it exercises many of the cookbook’s most important concerns at once:

- lifecycle state
- document/artifact handling
- workflow and approvals
- search and projections
- notifications
- integrations
- policy/rules
- audit/provenance

This makes it a strong test instrument for the cookbook itself.

However, V2 is not considered complete until the same architecture-planning quality holds for other reference archetypes as well.

---

## V2 Completion Criteria

The cookbook can be considered **stable V2** when:

### Framework stability
- archetype / capability / playbook structure remains unchanged
- capability splits remain in place
- lightweight role metadata remains useful but not overbuilt

### Capability stability
- capability boundaries are clear
- negative boundary statements remain strong
- artifact-repository is integrated where appropriate

### Playbook stability
- template supports architecture synthesis cleanly
- contract-management-system ambiguity is materially reduced
- at least one additional reference archetype or major playbook can be tested successfully using the same planning loop

### Documentation stability
- repo-level docs match the current structure
- legacy capability pages are clearly marked
- template guidance reflects current V2 model

### Architecture synthesis quality
Repeated planning exercises should produce:
- clearer canonical vs derived state
- cleaner workflow vs lifecycle boundaries
- cleaner artifact handling
- fewer architectural guesses
- more deterministic module interpretation

---

## Suggested Execution Plan

### Phase 1
Finish the remaining stabilization work for `contract-management-system`:

- Canonical Contract Domain Model
- Typical Workflow Units
- Common V1 Operational Read Models
- Typical Modular-Monolith Module Boundaries
- minimal v1 integration boundary clarification

### Phase 2
Re-run the same architecture synthesis and evaluation prompts against `contract-management-system`.

Success signal:
- fewer modeling guesses
- fewer authority/boundary ambiguities
- more deterministic module design

### Phase 3
Run the same architecture synthesis test against another major playbook, preferably:

- `case-ticket-system`

Then optionally:
- `document-management-system`
- `crm`

Success signal:
- cookbook works as a domain-neutral architecture constraint framework, not just as a CLM-specific document set

---

## Codex Tasking Guidance

When using Codex against this repository:

### Good tasks
- make small, targeted edits
- update template sections
- tighten one playbook at a time
- rerun architecture synthesis exercises
- summarize where ambiguity remains

### Bad tasks
- redesign the whole framework
- expand archetypes
- add many new capabilities at once
- mass-update every playbook without testing
- infer V2 direction from scattered chat history

Codex should use this document as the source of truth for V2 stabilization work.

---

## Immediate Next Task

The next task is:

**finish the remaining V2 stabilization edits for `playbooks/contract-management-system` and then rerun the prior architecture synthesis test using the same prompts as before.**

Specifically:
- tighten canonical domain model
- clarify workflow units
- define minimal v1 read models
- clarify modular-monolith module blueprint
- clarify minimal v1 integration boundary set

After that, evaluate whether the architecture synthesis result shows fewer guesses and cleaner boundaries.