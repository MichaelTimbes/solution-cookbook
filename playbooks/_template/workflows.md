# Playbook Workflows Template

Use this file to document the key workflows/use cases supported by the system.

Authoring references:
- Capabilities index: [../../cookbook/capabilities](../../cookbook/capabilities)

## Workflow Authoring Notes

For each workflow:
- Name the workflow clearly.
- List stages in order.
- Note which capabilities are involved.
- Identify decision points and policy checks.

## Typical Workflow Units

Use this section to describe the bounded workflow units that commonly exist inside the broader system lifecycle.

Guidance:
- Keep this lightweight and domain-shaped.
- Treat workflows as process units, not the entire lifecycle.
- Name the common units readers would likely implement or orchestrate first.


## Workflow 1: <workflow-name>

Stages:
1. <stage-1>
2. <stage-2>
3. <stage-3>

Capabilities involved:
- [<capability-1>](../../cookbook/capabilities/<capability-1>.md)
- [<capability-2>](../../cookbook/capabilities/<capability-2>.md)

Notes:
- <policy checks, approvals, notifications, retries, etc.>

## Workflow 2: <workflow-name>

Stages:
1. <stage-1>
2. <stage-2>
3. <stage-3>

Capabilities involved:
- [<capability-1>](../../cookbook/capabilities/<capability-1>.md)
- [<capability-2>](../../cookbook/capabilities/<capability-2>.md)

Notes:
- <operational constraints, audit expectations, failure handling>

## Workflow 3: <workflow-name>

Stages:
1. <stage-1>
2. <stage-2>
3. <stage-3>

Capabilities involved:
- [<capability-1>](../../cookbook/capabilities/<capability-1>.md)
- [<capability-2>](../../cookbook/capabilities/<capability-2>.md)

Notes:
- <state transitions, SLAs/SLOs, exception paths>

