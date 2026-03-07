# Legal Case Management Architecture

## Logical Components

- Intake and matter registration boundary.
- Case domain service for legal matter lifecycle.
- Evidence linkage service for attachments and references.
- Review and approval orchestration service.
- Access policy enforcement service.
- Search/query service for legal operations.
- Notification and deadline service.
- Audit and chain-of-custody service.

## Boundary Principles

- Separate case state from evidence content stores.
- Enforce policy checks before retrieval and mutation.
- Keep chain-of-custody logs immutable.
- Keep review decisions versioned and attributable.
