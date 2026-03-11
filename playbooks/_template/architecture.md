# Playbook Architecture Template

Use this file to elaborate on the logical architecture for a playbook.

Authoring references:
- Capabilities index: [../../cookbook/capabilities](../../cookbook/capabilities)
- Patterns index: [../../cookbook/foundational-patterns/README.md](../../cookbook/foundational-patterns/README.md)

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
- <Component A> -> [<capability-1>](../../cookbook/capabilities/<capability-1>.md)
- <Component B> -> [<capability-2>](../../cookbook/capabilities/<capability-2>.md)

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



## Event / Projection Notes

Use this section, where relevant, to describe how common canonical state changes often propagate to derived views or side effects.

Suggested optional format:

| Canonical change | Likely downstream consumers | Typical derived outputs |
|---|---|---|
| <State change A> | <search index, read models, notifications> | <projected search docs, delivery intents> |
| <State change B> | <audit/provenance, integrations, reporting> | <timeline entries, sync messages, aggregates> |

Guidance:
- Keep this lightweight and planning-oriented.
- Use wording such as likely, common, typical, or often.
- Do not assume a specific integration style or transport mechanism.
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

## Communication Boundary Notes

Clarify ownership and intent boundaries for communication-related capabilities:
- `human-communication`: durable participant discussion and coordination context.
- `notification-preferences-routing`: recipient intent, channel policy, and routing decisions.
- `notification-messaging-system`: delivery execution and channel transport behavior.
- workflow comments / approval rationale: decision context attached to lifecycle or approval transitions.

Keep this section short and boundary-focused.
## Diagram Links

- [System context](diagrams/system-context.mmd)
- [Container view](diagrams/container-view.mmd)
- [Lifecycle flow](diagrams/lifecycle-flow.mmd)


