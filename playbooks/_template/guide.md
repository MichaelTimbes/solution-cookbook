---
playbook: <name of system to build>
archetype: <primary archetype, e.g. document-management-system>
required-capabilities:
  - <capability-1>
  - <capability-2>
optional-capabilities:
  - <capability-3>
patterns:
  - <foundational-pattern-1>
  - <foundational-pattern-2>
---

# <Playbook Title>

Use this template to author a new playbook in a technology-agnostic way.

Authoring references:
- Archetypes index: [../../cookbook-v1/archetypes](../../cookbook-v1/archetypes)
- Capabilities index: [../../cookbook-v1/capabilities](../../cookbook-v1/capabilities)
- Foundational patterns index: [../../cookbook-v1/foundational-patterns/README.md](../../cookbook-v1/foundational-patterns/README.md)
- Tri-map: [../../cookbook-v1/pattern-capability-archetype-tri-map.md](../../cookbook-v1/pattern-capability-archetype-tri-map.md)

## Problem Context

Describe the real-world problem this system solves.

Guidance:
- Explain why this system type is needed.
- Describe the operational and governance pains it addresses.
- Keep language general so future authors can fill in domain specifics.

## Archetype

Identify the primary archetype and any related archetypes.

Fill in:
- Primary archetype: [<primary-archetype-page>](../../cookbook-v1/archetypes/<primary-archetype-page>.md)
- Related archetypes:
  - [<related-archetype-1>](../../cookbook-v1/archetypes/<related-archetype-1>.md)
  - [<related-archetype-2>](../../cookbook-v1/archetypes/<related-archetype-2>.md)

Explain briefly how these archetypes interact in this system.

## Foundational Patterns

List the high-level patterns that influence this system shape.

Fill in:
- [<pattern-1>](../../cookbook-v1/foundational-patterns/<pattern-1>.md)
- [<pattern-2>](../../cookbook-v1/foundational-patterns/<pattern-2>.md)
- [<pattern-3>](../../cookbook-v1/foundational-patterns/<pattern-3>.md)

Explain why each pattern is relevant to this system and how it influences design decisions.

## Required Capabilities

Reference the capabilities that must be assembled for this playbook.

Fill in:
- [<required-capability-1>](../../cookbook-v1/capabilities/<required-capability-1>.md)
- [<required-capability-2>](../../cookbook-v1/capabilities/<required-capability-2>.md)
- [<required-capability-3>](../../cookbook-v1/capabilities/<required-capability-3>.md)

Optional:
- [<optional-capability-1>](../../cookbook-v1/capabilities/<optional-capability-1>.md)

For each capability, add a short note describing how it participates in the system.

## Reference Architecture

Provide guidance on a typical architecture using capability-aligned components.

Suggested component placeholders:
- Ingestion gateway or intake boundary
- Metadata/classification service
- Core repository service
- Search/query service
- Workflow/orchestration service
- Notification/messaging service
- Audit/provenance service
- Data movement/import-export service

Explain how these components interact and where the boundaries are.

Diagrams:
- [System context](diagrams/system-context.mmd)
- [Container view](diagrams/container-view.mmd)
- [Lifecycle flow](diagrams/lifecycle-flow.mmd)

## System Evolution

Describe maturity phases for this system type.

Template:
- Phase 1: <initial minimal capability set>
- Phase 2: <metadata/search and core governance>
- Phase 3: <workflow and collaboration>
- Phase 4: <automation and policy-driven behavior>
- Phase 5: <advanced compliance, retention, and operational visibility>

Explain how capabilities and patterns emerge across phases.

## Failure Modes

List common architectural risks and summarize causes, impacts, and mitigations.

Examples to consider:
- Weak metadata strategy
- Missing audit trails
- Poor search performance
- Uncontrolled duplication
- Insufficient access control
- Lifecycle policy drift
- Notification storms

See also: [failure-modes.md](failure-modes.md)
