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
- Archetypes index: [../../cookbook/archetypes](../../cookbook/archetypes)
- Capabilities index: [../../cookbook/capabilities](../../cookbook/capabilities)
- Foundational patterns index: [../../cookbook/foundational-patterns/README.md](../../cookbook/foundational-patterns/README.md)
- Tri-map: [../../cookbook/pattern-capability-archetype-tri-map.md](../../cookbook/pattern-capability-archetype-tri-map.md)

## Problem Context

Describe the real-world problem this system solves.

Guidance:
- Explain why this system type is needed.
- Describe the operational and governance pains it addresses.
- Keep language general so future authors can fill in domain specifics.

## System Forces

Describe the forces that influence the architecture of this system.

Examples:
- scale pressure
- data consistency requirements
- human workflow complexity
- compliance and audit requirements
- integration surface area
- operational reliability needs

Guidelines:
- keep this section concise
- explain *why the architecture exists*, not just how it works
- focus on recurring forces seen across implementations

## Archetype

Identify the primary archetype and any related archetypes.

Fill in:
- Primary archetype: [<primary-archetype-page>](../../cookbook/archetypes/<primary-archetype-page>.md)
- Related archetypes:
  - [<related-archetype-1>](../../cookbook/archetypes/<related-archetype-1>.md)
  - [<related-archetype-2>](../../cookbook/archetypes/<related-archetype-2>.md)

Explain briefly how these archetypes interact in this system.

## Foundational Patterns

List the high-level patterns that influence this system shape.

Fill in:
- [<pattern-1>](../../cookbook/foundational-patterns/<pattern-1>.md)
- [<pattern-2>](../../cookbook/foundational-patterns/<pattern-2>.md)
- [<pattern-3>](../../cookbook/foundational-patterns/<pattern-3>.md)

Explain why each pattern is relevant to this system and how it influences design decisions.

## Required Capabilities

Reference the capabilities that must be assembled for this playbook.

Fill in:
- [<required-capability-1>](../../cookbook/capabilities/<required-capability-1>.md)
- [<required-capability-2>](../../cookbook/capabilities/<required-capability-2>.md)
- [<required-capability-3>](../../cookbook/capabilities/<required-capability-3>.md)

Optional:
- [<optional-capability-1>](../../cookbook/capabilities/<optional-capability-1>.md)

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
