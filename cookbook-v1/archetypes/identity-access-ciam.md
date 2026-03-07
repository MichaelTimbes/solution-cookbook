# Identity / Access (CIAM) Archetype

## What this archetype is / is not
- A system for customer identity lifecycle, authentication, authorization, federation, and provisioning.
- Enables secure sign-up, sign-in, token issuance, and policy-driven access controls.
- Not an application business domain itself; it is a foundational control plane.

## Typical modules
- Registration and profile management
- Authentication and MFA
- Authorization policies and scopes
- OAuth/OIDC token services
- Federation and social login
- SCIM provisioning and deprovisioning
- Session and device management
- Audit, risk, and anomaly detection

## Core workflows (top 3–5)
- User registration and verification
- Authentication with step-up MFA
- Authorization and token issuance
- Provisioning and deprovisioning to downstream apps
- Session refresh, revocation, and logout

## Canonical data model skeleton
### Core entities
- Identity
- CredentialFactor
- ClientApplication
- AuthorizationGrant
- AccessToken/RefreshToken metadata
- Group/Role
- Policy
- ProvisioningJob
- SecurityAuditEvent

### Key relations
- Identity 1..N CredentialFactors
- Identity N..M Groups/Roles
- ClientApplication 1..N AuthorizationGrants
- AuthorizationGrant 0..N Token metadata records
- Identity 0..N ProvisioningJobs
- Policy applies across Identity, ClientApplication, and Resource scopes

### Invariants/constraints
- Token validity and signature verification are mandatory at all resource boundaries.
- MFA requirements enforced for protected actions and risk states.
- Session revocation propagates within defined SLA.
- Provisioning actions are idempotent and auditable.
- PII handling follows minimization and purpose limits.

## Permission model patterns
- RBAC baseline with optional ABAC extensions.
- Scope-based API authorization with least privilege.
- Tenant isolation controls for multi-tenant CIAM.
- Admin action controls with step-up auth.
- Break-glass and emergency access flows fully audited.

## Integration touchpoints
- Application gateways and APIs
- Identity providers/federation partners
- HR/CRM/profile systems
- Notification channels for OTP and alerts
- SIEM and security operations tools
- Provisioning endpoints (SCIM)

## Embedded capabilities
- Approval workflows and human-in-the-loop
- Dynamic evaluation and survey engine
- Audit log and provenance
- Notification preferences and routing
- Rules engine and decisioning
- Import and export pipelines
- Search, filters, and saved views
- Idempotency, outbox, retries, and DLQ
- Custom fields and extensible attributes

## Failure modes catalog (starter set: 8–12)
- Token replay due to weak session controls.
- Misconfigured scopes exposing excessive API access.
- MFA channel outages blocking legitimate login.
- Federation metadata drift causing auth failures.
- Provisioning lag creating stale access rights.
- Group/role sync mismatch between systems.
- Brute-force attacks not throttled effectively.
- Session revocation not propagating in time.
- Account recovery abuse due to weak verification.
- Audit gaps for privileged admin actions.

## Observability baseline
### Key traces
- Registration to verification journey.
- Login to token issuance path.
- Provisioning event propagation to downstream systems.

### Key metrics
- Authentication success/failure rates.
- MFA challenge success and timeout rates.
- Token issuance and revocation latency.
- Provisioning lag and error rates.
- Suspicious login detection counts.

### Audit events
- Credential, factor, and recovery method changes.
- Admin policy and scope changes.
- Privileged login and override actions.
- Provisioning and deprovisioning outcomes.
- Session revocation and anomaly responses.

## Minimal architecture diagram (C4-ish, 1 page)
- Context: end users, relying applications, federation partners, security operations.
- Containers: identity UI, auth API, token service, policy engine, provisioning workers, identity store, audit and risk engine.
- Relationships: auth services issue tokens and evaluate policy; workers propagate identity changes; audit/risk observes all high-risk flows.

## Implementation notes and stack variants
- Keep protocol compliance (OAuth/OIDC/SCIM) explicit in interface contracts.
- Separate interactive auth from machine-to-machine auth paths.
- Use event-driven provisioning with replay-safe handlers.
- Treat key management and rotation as first-class operational concerns.

## Licensing & source attribution notes
- Content is synthesized from open standards and OSS practices.
- Avoid direct reuse of vendor-specific guidance text.
- Add detailed source notes during final editorial QA.
