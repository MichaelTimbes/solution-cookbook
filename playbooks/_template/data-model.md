# Playbook Data Model Template

Use this file to define the canonical data model skeleton for the playbook.

## Core Entity Groups

Describe aggregate roots or entity groups.

Template:
- <Aggregate Group A>
  - <Entity A1>: <one-sentence description>
  - <Entity A2>: <one-sentence description>
- <Aggregate Group B>
  - <Entity B1>: <one-sentence description>
  - <Entity B2>: <one-sentence description>

Guidance:
- Clarify which entities are authoritative sources of truth.
- Clarify which entities are projections or read models.
- Keep naming and scope consistent with capabilities and archetypes.

## Canonical Entities (Fill In)

- <Entity 1>: <definition>
- <Entity 2>: <definition>
- <Entity 3>: <definition>

## Relationships

Add relationship rules:
- <Entity X> has many <Entity Y>
- <Entity Z> references <Entity X> by stable identifier
- <Event/Activity entity> correlates state transitions across services

## Invariants

Add non-negotiable data and state rules:
- <Invariant 1>
- <Invariant 2>
- <Invariant 3>

## Governance and Lifecycle Notes

Document governance constraints and lifecycle implications:
- <retention/legal hold implications>
- <audit/provenance expectations>
- <import/export boundaries>
