# Workflow / Stateful Progression

## Description of the pattern
Workflow / Stateful Progression models how entities move through explicit states with controlled transitions.

## Why it appears across enterprise systems
Most enterprise outcomes are not one-step operations. They require durable progression across human and system actions over time.

## Typical implementation capabilities
- [Approval Workflows / Human-In-The-Loop](../capabilities/approval-workflows-human-in-the-loop.md)
- [Rules Engine / Decisioning](../capabilities/rules-engine-decisioning.md)
- [Audit Log + Provenance](../capabilities/audit-log-provenance.md)

## Example archetypes that rely on it
- [Workflow / BPM System](../archetypes/workflow-bpm-system.md)
- [Case / Ticket System](../archetypes/case-ticket-system.md)
- [Payments / Billing](../archetypes/payments-billing.md)

## Common failure modes when ignored
- Hidden state transitions and inconsistent outcomes
- Stuck work with no escalation path
- Manual reconciliation replacing deterministic flow
