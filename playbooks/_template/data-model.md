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


## Authority Model

Use this section to make source-of-truth boundaries explicit in this playbook.

### Canonical / authoritative state

Describe records that are likely the primary source of truth.

Template:
- <Canonical record A>
- <Canonical record B>

### Supporting authoritative records

Describe records that are authoritative within their own concern, but are not the primary lifecycle owner.

Template examples:
- <Artifact metadata/linkage>
- <Approval decisions>
- <Obligation records>
- <Configuration records>

### Derived / projected state

Describe records that are likely derived from canonical state.

Template:
- <Search index documents>
- <Read-model projections>
- <Notification delivery state>
- <Reporting aggregates>
- <Cache entries>

### Notes

Implementation details can vary by system and constraints. In this playbook, this distinction is mainly a planning aid to reduce confusion between canonical records and derived views.

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


