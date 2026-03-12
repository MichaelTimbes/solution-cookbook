Use the updated `contract-management-system` playbook and linked capability catalog as the source of truth.

Design a **v1 implementation architecture** for this system.

Assumptions:
- greenfield implementation
- technology-neutral
- vendor-neutral
- modular monolith
- one relational database
- background workers allowed
- search index allowed


- no microservices required
- no distributed transactions
- minimize operational complexity

Goals:
- preserve the logical boundaries implied by the updated playbook
- preserve the workflows and lifecycle expectations
- respect authoritative vs derived state
- use the referenced capabilities as implementation building blocks
- do not invent a fundamentally different architecture

Produce:

## 1. System scope
## 2. Application modules
## 3. Core data model
## 4. Capability embedding
## 5. Key workflows
## 6. Async processing
## 7. Integration boundaries
## 8. Extraction seams
## 9. Architectural risks

Constraint:
Prefer clear module boundaries over distributed deployment boundaries.

Post your plan as a response.