# Policy-Driven Behavior (Rules / Decisioning)

## Description of the pattern
Policy-Driven Behavior externalizes decision logic from application code into governed, testable policy assets.

## Why it appears across enterprise systems
Eligibility, routing, risk, and compliance rules change faster than deploy cycles. Systems need controlled policy evolution without code churn.

## Typical implementation capabilities
- [Rules Engine / Decisioning](../capabilities/rules-engine-decisioning.md)
- [Dynamic Evaluation / Survey Engine](../capabilities/dynamic-evaluation-survey-engine.md)
- [Approval Workflows / Human-In-The-Loop](../capabilities/approval-workflows-human-in-the-loop.md)

## Example archetypes that rely on it
- [Workflow / BPM System](../archetypes/workflow-bpm-system.md)
- [Identity / Access (CIAM)](../archetypes/identity-access-ciam.md)
- [Inventory / Catalog](../archetypes/inventory-catalog.md)

## Common failure modes when ignored
- Business logic scattered across services
- Unintended behavior drift between environments
- Slow adaptation to regulatory or market changes
