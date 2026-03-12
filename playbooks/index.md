# System Playbooks

Playbooks provide reference architectures and workflows for building specific types of systems by combining archetypes, capabilities, and foundational patterns into complete architecture blueprints.

Each playbook includes:

- architecture overview
- workflows
- data model
- common failure modes
- diagrams

## Reference vs Variant

- **Reference playbooks** define the baseline architecture for each core archetype.
- **Variant playbooks** reuse the same archetype structure and adapt domain language, workflows, policies, lifecycle management, and integration boundaries.

Reference playbooks:

- [Document Management System](document-management-system/guide.md)
- [Customer Relationship Management](crm/guide.md)
- [Case / Ticket System](case-ticket-system/guide.md)
- [Workflow / BPM System](workflow-bpm-system/guide.md)

## Playbook Catalog

| Playbook | Archetype | Description |
|---|---|---|
| [Document Management System](document-management-system/guide.md) | Document Management Archetype | A governed platform for storing, classifying, and retrieving documents. |
| [Customer Relationship Management](crm/guide.md) | CRM Archetype | A customer lifecycle platform for managing accounts, contacts, leads, opportunities, and service-linked interactions. |
| [Case / Ticket System](case-ticket-system/guide.md) | Case / Ticket Archetype | An SLA-governed operations platform for intake, triage, assignment, resolution, and closure of requests and incidents. |
| [Workflow / BPM System](workflow-bpm-system/guide.md) | Workflow / BPM Archetype | A durable orchestration platform for long-running processes with explicit state transitions, approvals, timers, and escalations. |
| [Support Ticket System](support-ticket-system/guide.md) | Case / Ticket Archetype Variant | A support-focused ticket lifecycle for intake, triage, assignment, escalation, and closure. |
| [Incident Management System](incident-management-system/guide.md) | Case / Ticket Archetype Variant | An operations incident workflow for alert-driven triage, escalation, mitigation, and review. |
| [Sales CRM](sales-crm/guide.md) | CRM Archetype Variant | A revenue-focused CRM for lead, opportunity, quote, and pipeline management. |
| [Donor Management System](donor-management-system/guide.md) | CRM Archetype Variant | A fundraising relationship system for donor lifecycle, campaigns, pledges, and stewardship. |
| [Enterprise Document Management](enterprise-document-management/guide.md) | Document Management Archetype Variant | A multi-domain governed repository for enterprise document lifecycle and retention control. |
| [Contract Management System](contract-management-system/guide.md) | Document Management Archetype Variant | A contract lifecycle platform for drafting, review, execution, obligations, and renewals. |
| [Approval Workflow System](approval-workflow-system/guide.md) | Workflow / BPM Archetype Variant | A policy-governed approval engine with routing, escalation, and auditable decisions. |
| [Business Process Automation](business-process-automation/guide.md) | Workflow / BPM Archetype Variant | A deterministic orchestration platform for automated multi-step business processes. |

This page is the main entry point for readers looking for example architectures in the Solution Cookbook.
