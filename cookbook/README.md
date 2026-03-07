# Solution Cookbook

This folder contains the cookbook scaffold in four layers:

- Level 1: archetype blueprints in `archetypes/`
- Level 2: capability recipes in `capabilities/`
- Level 3: foundational design patterns in `foundational-patterns/`
- Level 4: reference system playbooks in `../playbooks/`
- Cross-link map: `cross-link-matrix.md`
- Navigation matrix: `archetype-capability-matrix.md`
- Tri-map (pattern → capability → archetype): `pattern-capability-archetype-tri-map.md`

## Scope

- 10 archetype pages
- 12 capability pages
- 13 foundational pattern pages

## How to use

### Core Layers

The Solution Cookbook is organized into four layers that move from conceptual guidance to concrete system design:

#### Patterns

Fundamental design forces that shape systems. Patterns explain why certain architecture concerns repeatedly appear across domains, such as identity and access control, auditability, discoverability, workflow progression, and operational visibility.

#### Capabilities

Reusable functional building blocks used across systems. Capabilities describe implementation-level concerns that can be assembled in different combinations, such as search/filtering, audit logging, approval workflows, notifications, and data movement.

#### Archetypes

Categories of systems with shared structural characteristics. Archetypes describe common system shapes (for example, document management, workflow, CRM, or case management) and the capabilities they typically require.

#### Playbooks

Reference architectures showing how archetypes and capabilities combine into real systems. Playbooks provide practical guidance with architecture composition, workflows, data model outlines, failure modes, and diagrams.

### Typical Workflow

Use the cookbook in this order when designing a new system:

1. Identify the type of system you need to build.
2. Review the relevant archetype.
3. Examine the required capabilities.
4. Study the reference playbook.
5. Adapt the architecture to your domain.

### Example

If you are building a document platform, start with the Document Management archetype to understand the system shape and boundaries. Then review capabilities such as search/filters/saved views, audit log and provenance, import/export pipelines, approval workflows, and notification/messaging. After that, study the Document Management System playbook to see how these pieces are composed into a reference architecture with workflows and lifecycle diagrams. Finally, adapt the playbook for your domain-specific rules, data model, and policy requirements.

## Navigation

- Archetype-capability matrix: [cross-link-matrix.md](cross-link-matrix.md)
- Capability-row navigation matrix: [archetype-capability-matrix.md](archetype-capability-matrix.md)
- Foundational patterns index: [foundational-patterns/README.md](foundational-patterns/README.md)
- Executive tri-map: [pattern-capability-archetype-tri-map.md](pattern-capability-archetype-tri-map.md)
- Playbooks index: [../playbooks/index.md](../playbooks/index.md)

## Coverage notes

- Requested high-value capabilities already present:
	- [Rules Engine / Decisioning](capabilities/rules-engine-decisioning.md)
	- [Template / Merge Fields Document Generation](capabilities/template-merge-fields-document-generation.md)
	- [Import / Export Pipelines](capabilities/import-export-pipelines.md)
	- [Search / Filters / Saved Views](capabilities/search-filters-saved-views.md)
- Newly scaffolded as missing foundational capability:
	- [Notification / Messaging System](capabilities/notification-messaging-system.md)
	- [Human Communication / Collaboration Layer](capabilities/human-communication-coordination.md)

- Newly scaffolded as recurring foundational pattern:
	- [Human Communication & Coordination](foundational-patterns/human-communication-coordination.md)

## Three-way navigation model

- By archetype: start in [archetypes](archetypes)
- By capability: start in [capabilities](capabilities)
- By foundational pattern: start in [foundational-patterns](foundational-patterns)
- By concept-to-implementation chain: [pattern-capability-archetype-tri-map.md](pattern-capability-archetype-tri-map.md)



