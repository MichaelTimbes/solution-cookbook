# Playbook Architecture Template

Use this file to elaborate on the logical architecture for a playbook.

Authoring references:
- Capabilities index: [../../cookbook/capabilities](../../cookbook/capabilities)
- Patterns index: [../../cookbook/foundational-patterns/README.md](../../cookbook/foundational-patterns/README.md)

## Composition Intent

Describe the composition intent for the target system:
- What system shape is being composed?
- Which archetype is primary?
- Which related archetypes influence the boundaries?

## Logical Components

List the principal logical components and responsibilities.

Template:
- <Component A>: <responsibility>
- <Component B>: <responsibility>
- <Component C>: <responsibility>

## Capability Mapping

Map components to capabilities.

Template:
- <Component A> -> [<capability-1>](../../cookbook/capabilities/<capability-1>.md)
- <Component B> -> [<capability-2>](../../cookbook/capabilities/<capability-2>.md)

## Boundary Principles

Document architectural boundary principles.

Include guidance such as:
- Storage, metadata, and query concerns often benefit from being kept conceptually distinct.
- Workflow orchestration is typically kept separate from the core lifecycle or repository boundary.
- Audit/provenance evidence is commonly kept immutable and independently queryable.
- Import/export pathways are often made explicit and policy-governed.
- Authorization evaluation is typically kept consistent across access points.

## Interaction Flow

Describe how components interact at a high level:
- Request flow
- Event flow
- State transition flow
- Control points for policy and approval




## Workflow / Lifecycle Handshake

Clarify responsibility boundaries between orchestration and lifecycle state.

Describe:
- what lifecycle state can be changed directly
- what workflow can gate or trigger
- how workflow completion affects lifecycle transitions
- what should not mutate authoritative state directly

Guidance:
- Focus on responsibility boundaries.
- Do not prescribe implementation style.

## Read Model Strategy

Describe expected read paths and why they exist.

Typical sources:
- primary relational or domain records
- projection/read-model tables
- search index
- reporting/export paths

Guidance:
- Keep this conceptual and technology-neutral.
- Distinguish operational reads from indexed retrieval and reporting paths.

## Typical Modular-Monolith Module Boundaries

List the typical in-process logical modules for the playbook.

Template:
- <Module A>
- <Module B>
- <Module C>

Guidance:
- Treat these as logical boundaries inside one system shape.
- Do not imply a microservice split.
- Keep names responsibility-oriented.

## Typical V1 Integration Boundaries

Describe the external boundaries the playbook commonly interacts with.

Examples:
- identity provider
- messaging or notification providers
- external systems of record
- file or artifact storage
- third-party APIs

Guidance:
- Keep this boundary-oriented and technology-neutral.
- Emphasize adapters, controlled contracts, and idempotent handling where relevant.

## Communication Boundary Notes

Clarify ownership and intent boundaries for communication-related capabilities:
- `human-communication`: durable participant discussion and coordination context.
- `notification-preferences-routing`: recipient intent, channel policy, and routing decisions.
- `notification-messaging-system`: delivery execution and channel transport behavior.
- workflow comments / approval rationale: decision context attached to lifecycle or approval transitions.

Keep this section short and boundary-focused.

## Diagram References

- [System context](diagrams/system-context.mmd)
- [Container view](diagrams/container-view.mmd)
- [Lifecycle flow](diagrams/lifecycle-flow.mmd)


