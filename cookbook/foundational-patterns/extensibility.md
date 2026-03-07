# Extensibility

## Description of the pattern
Extensibility allows system behavior and data shape to evolve without destabilizing core workflows.

## Why it appears across enterprise systems
Enterprise domains change by tenant, region, and policy. Systems that cannot adapt become brittle and expensive to maintain.

## Typical implementation capabilities
- [Custom Fields / Extensible Attributes](../capabilities/custom-fields-extensible-attributes.md)
- [Rules Engine / Decisioning](../capabilities/rules-engine-decisioning.md)
- [Dynamic Evaluation / Survey Engine](../capabilities/dynamic-evaluation-survey-engine.md)

## Example archetypes that rely on it
- [CRM](../archetypes/crm.md)
- [Inventory / Catalog](../archetypes/inventory-catalog.md)
- [CMS / Wiki / Knowledge Base](../archetypes/cms-wiki-kb.md)

## Common failure modes when ignored
- Frequent schema rewrites for minor changes
- Hard-coded policy branches spread across services
- High regression risk for routine domain evolution
