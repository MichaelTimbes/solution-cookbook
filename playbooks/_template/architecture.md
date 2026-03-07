# Playbook Architecture Template

Use this file to elaborate on the logical architecture for a playbook.

Authoring references:
- Capabilities index: [../../cookbook-v1/capabilities](../../cookbook-v1/capabilities)
- Patterns index: [../../cookbook-v1/foundational-patterns/README.md](../../cookbook-v1/foundational-patterns/README.md)

## Architecture Intent

Describe the composition intent for the target system:
- What system shape is being composed?
- Which archetype is primary?
- Which related archetypes influence the boundaries?

## Principal Components

List principal services/components and responsibilities.

Template:
- <Component A>: <responsibility>
- <Component B>: <responsibility>
- <Component C>: <responsibility>

## Capability Mapping

Map components to capabilities.

Template:
- <Component A> -> [<capability-1>](../../cookbook-v1/capabilities/<capability-1>.md)
- <Component B> -> [<capability-2>](../../cookbook-v1/capabilities/<capability-2>.md)

## Boundary Principles

Document architectural boundary principles.

Include guidance such as:
- Separate storage concerns from metadata and query concerns.
- Keep workflow orchestration separate from the core repository.
- Keep audit/provenance evidence immutable and independently queryable.
- Keep import/export pathways explicit and policy-governed.
- Ensure consistent authorization evaluation at all access points.

## Interaction Overview

Describe how components interact at a high level:
- Request flow
- Event flow
- State transition flow
- Control points for policy and approval

## Diagram Links

- [System context](diagrams/system-context.mmd)
- [Container view](diagrams/container-view.mmd)
- [Lifecycle flow](diagrams/lifecycle-flow.mmd)
