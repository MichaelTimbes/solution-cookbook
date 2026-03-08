# Recurring Enterprise System Architecture Archetypes for a Solution Cookbook Catalog

## Scope and validation criteria

This research targets **recurring software system architecture shapes** (archetypes) that appear repeatedly across industries and implementations, and that are meaningfully distinct from the catalog’s current archetypes (Case/Ticket, CRM, Document Management, Workflow/BPM). The focus is on **recognizable recurring structures**: domain model, lifecycle engines, indexing/retrieval layers, orchestration components, and integration boundaries—not SaaS category labels or vendor packaging. citeturn2search0turn2search5

Validation used the following “must-haves,” aligned to your definition:

An archetype is accepted when it exhibits (a) stable recurring workflows, (b) a repeating core entity model, (c) a characteristic architecture signature, and (d) multiple real-world implementations spanning OSS and enterprise platforms. citeturn2search5turn0search1turn1search22

Where a candidate is **not** accepted as an archetype, it is classified as either:
- **Variant**: a specialization of another archetype (same architectural shape, different domain constraints).
- **Capability**: a reusable subsystem pattern (e.g., search, rules, notification) that appears inside many archetypes. citeturn2search0

## Candidate archetypes and classification

The table lists **additional recurring archetypes** that are architecturally distinct from the four already in your catalog, plus a small number of “boundary” candidates to clarify variants/capabilities.

| Archetype | Description | Evidence |
|---|---|---|
| Identity & Access Management platform (IAM / IdP) **[Archetype]** | Centralizes identity lifecycle, authentication, federation, token issuance, and provisioning across many applications; shaped by standardized protocols and administration workflows. | Protocol-driven interoperability is formalized by OAuth 2.0, OpenID Connect, SAML 2.0, and SCIM. citeturn5search1turn5search2turn5search4turn5search0turn0search28turn0search24 |
| Master Data Management hub (MDM / Golden Record) **[Archetype]** | Builds and governs “golden records” for key entities (customer, product, supplier, location) using match/merge/survivorship and publishes mastered data to downstream systems. | Repeating components: master data hub, matching/survivorship, stewardship workflow, and integration layer. citeturn0search1turn0search5turn0search37turn0search21 |
| Configuration/Service relationship registry (CMDB / configuration graph) **[Archetype]** | Maintains a configuration-item graph (CIs + relationships), fed by discovery and reconciled across sources; supports impact analysis and service mapping. | Repeating CI class hierarchies, relationships, service maps, and identification/reconciliation to prevent duplicates. citeturn8view0turn8view1turn8view2turn1search15turn0search14 |
| API management platform (Gateway + control plane + developer portal) **[Archetype]** | Manages the lifecycle of APIs and enforces runtime policies via a gateway, with a management plane and developer-facing onboarding/subscription flows. | Canonical decomposition: gateway, management plane, developer portal; recurring policies like rate limiting. citeturn0search27turn0search3turn0search7turn9search7 |
| Analytics warehouse & BI platform (DW/Lakehouse + semantic model + reporting) **[Archetype]** | Integrates data from many operational sources into analytical storage, transforms it, and serves it via semantic models and reports/dashboards with governance. | Repeating layered structure: ingestion → preparation → warehouse → semantic models → reports. citeturn1search12turn1search20turn1search37 |
| Enterprise search & knowledge discovery platform **[Archetype]** | Connects to many repositories, builds secure indexes, and executes ranked retrieval (often with relevance tuning); enforces permissions at query/index time. | Recurring “connect → index → query” pipelines with security trimming. citeturn1search22turn1search1turn1search14 |
| Observability platform (logs/metrics/traces + alerting) **[Archetype]** | Ingests telemetry, stores it in fit-for-purpose backends, correlates signals, and drives alerts/dashboards for operational decision loops. | The “three pillars” (logs, metrics, traces) + collectors/pipelines are widely standardized and implemented. citeturn1search3turn3search2turn1search21turn1search29 |
| Order management system (OMS) **[Archetype]** | Tracks and coordinates order lifecycle across channels; orchestrates fulfillment steps and integrates with inventory, shipping, and billing/settlement systems. | Repeatable lifecycle focus and hub role in order-to-cash integrations. citeturn2search2turn2search6turn2search10 |
| Collaboration messaging platform (team chat) **[Archetype]** | Real-time, multi-device messaging built around channels/rooms, websockets/push, durable message history, and integrations/bots. | OSS reference architectures explicitly describe modular components for scale and real-time communication. citeturn4search0turn4search1turn4search5 |
| Collaborative knowledge base / wiki **[Archetype, lower confidence]** | Page-centric collaborative authoring with revision history, diffs, permissions, and link graph; differs architecturally from file-centric document management. | Core data model revolves around page+revision tables and page history/compare workflows. citeturn4search3turn4search7turn4search10 |
| Enterprise asset management / CMMS **[Archetype, lower confidence]** | Asset hierarchy + work orders + preventive maintenance scheduling + spare parts; often integrates meters/IoT and scheduling. | Recurring work-order and preventive maintenance workflows and asset hierarchies. citeturn2search23turn2search33turn2search15 |
| Feature flag / feature management **[Archetype, emerging]** | Manages runtime change rollout via flags, targeting rules, environments, audit, and flag lifecycle (including retirement/archival). | OSS platforms and docs emphasize enterprise lifecycle management for flags and staged rollout control. citeturn3search5turn3search1turn3search13 |
| Data pipeline orchestrator **[Capability or Variant of Workflow/BPM]** | DAG scheduling, retries, backfills, and task execution for data/ops; structurally close to workflow orchestration but specialized around batch/ETL tasks. | Airflow explicitly frames itself as workflow scheduling/monitoring with modular orchestration. citeturn10search6turn10search2 |
| Search engine (e.g., index store/query engine) **[Capability]** | Indexing and query execution component used inside enterprise search, observability, and other systems; not, by itself, the full enterprise-search archetype. | Open source search suites emphasize ingest/search/analyze, commonly embedded in larger solutions. citeturn10search3turn1search22 |

## Deep analysis of top archetype candidates

image_group{"layout":"carousel","aspect_ratio":"16:9","query":["identity and access management reference architecture diagram oauth oidc saml scim","master data management hub architecture golden record match merge survivorship diagram","API management architecture diagram gateway management plane developer portal","data warehouse business intelligence solution architecture semantic model diagram"],"num_per_query":1}

### Identity & access management platform

**Purpose**  
A dedicated system whose core job is to **control digital identity and access** across many relying applications: authenticate users, issue tokens/assertions, federate external identities, and keep user/group lifecycle synchronized with downstream services. citeturn0search4turn0search24turn5search0

**Core workflows**  
Most implementations converge on these lifecycle loops (terminology varies, structure repeats):
- **Authenticate** (interactive login, MFA, session management) and **federate** to external identity providers (IdP-to-IdP or workforce federation). citeturn0search4turn0search28  
- **Authorize** via token or assertion issuance to relying parties (APIs and web apps). citeturn5search1turn5search2turn5search4  
- **Provision/deprovision** accounts and group membership to SaaS/apps using SCIM-style automated provisioning. citeturn5search0turn5search15  
- **Admin governance loop**: client/app registration, key rotation, policy configuration, audit/review. citeturn0search4turn3search4

**Core entities**  
A stable cross-product entity model appears repeatedly:
- User, group, role, permission (or policy)  
- Client / application (relying party), redirect URI / callback  
- Identity provider / federation connection  
- Credential / factor / authenticator  
- Session, token, claim/assertion, audit event citeturn5search2turn5search4turn5search0turn0search4

**Architecture structure**  
A recurring “shape” is visible across vendors and OSS:
- **Identity store** (directory or internal DB) + optional federation to external directories  
- **Authentication service** handling interactive flows (including MFA)  
- **Token/assertion service** implementing OAuth2/OIDC and/or SAML issuance  
- **Federation/brokering layer** (IdP connections, workforce federation)  
- **Provisioning service** (SCIM server/client, connectors, reconciliation)  
- **Admin UI + audit/logging** and often a policy/authorization layer citeturn0search4turn5search1turn5search2turn5search4turn5search0

**Integrations**  
IAM integrates “outward” to:
- SaaS applications and internal apps (OIDC/SAML) and APIs (OAuth2/OIDC). citeturn5search1turn5search2turn0search28  
- Provisioning endpoints of downstream systems (SCIM) for user/group lifecycle sync. citeturn5search0turn5search15

**Example systems**  
- entity["organization","Keycloak","oss iam server"] (OSS IAM server using OIDC/SAML, administered as a separate authentication server) citeturn3search4turn3search8  
- entity["company","Okta","identity provider company"] (commercial identity provider aligned to OAuth/OIDC/SAML usage guidance) citeturn0search16  
- entity["company","Google Cloud","cloud provider"] workforce identity federation (explicit integration of IdP via OIDC/SAML) citeturn0search28

**Why this is not a variant**  
IAM is structurally different from Case/Ticket, CRM, Document Management, and Workflow/BPM because its organizing center is **protocol-mediated trust and identity lifecycle** (federation, token issuance, provisioning), not business records, documents, or workflow steps. Its “lifecycle engine” is fundamentally the authentication/provisioning state machine shaped by standards (OAuth/OIDC/SAML/SCIM). citeturn5search1turn5search2turn5search4turn5search0turn0search24

---

### Master data management hub

**Purpose**  
An MDM hub exists to **create and govern authoritative master entities** (“golden records”) by consolidating inputs from many systems, resolving duplicates, and publishing mastered data as a shared source of truth. citeturn0search1turn0search5turn0search37

**Core workflows**  
Recurring workflows show a stable cadence across MDM implementations:
- **Ingest** entity records from source systems (batch/stream/API) into a mastering workspace. citeturn0search1turn0search5  
- **Match & link** candidate duplicates, then **merge** into a mastered record using survivorship/conflict rules. citeturn0search1turn0search21  
- **Stewardship loop**: human review of ambiguous matches, exceptions, and policy-driven remediation. citeturn0search5turn0search21  
- **Publish & synchronize** golden records back to consuming systems to maintain consistency. citeturn0search5turn0search1

**Core entities**  
Common “mastered” entity sets recur regardless of industry:
- Customer/party, product, supplier, employee, location (as master entity types)  
- Source record, match candidate link, golden record  
- Attribute-level survivorship rule, validation rule, exception/case  
- Stewardship task, audit event, lineage metadata citeturn0search5turn0search1turn0search21

**Architecture structure**  
A recognizable architecture signature shows up repeatedly:
- **Master data hub** (golden record store)  
- **Matching & survivorship engine** (identity resolution, conflict handling)  
- **Data quality/governance layer** (standards, validations, lineage/security policies)  
- **Stewardship UI** (task queues, review screens)  
- **Integration layer** (APIs, ETL/ELT, event streams/message brokers, orchestration) citeturn0search1turn0search5turn0search21

**Integrations**  
MDM is defined by its integration boundary: it sits between many producers and many consumers, commonly integrating with operational systems and analytics stacks. citeturn0search1turn0search5

**Example systems**  
- entity["company","Informatica","data management company"] MDM guidance explicitly describes a master hub with golden records, matching, and an integration layer. citeturn0search1  
- entity["company","Pimcore","data management platform vendor"] MDM offering framed as unified “source of truth” consolidation. citeturn9search1  
- entity["company","Talend","data integration company"] open-source-oriented MDM positioning (also illustrating that MDM is implemented beyond a single vendor ecosystem). citeturn9search4turn9search8

**Why this is not a variant**  
MDM is not a CRM variant: CRM optimizes sales/service interactions, while MDM is an **entity mastering and governance hub** whose defining mechanisms are match/merge/survivorship + publishing mastered entities to many systems. Its architecture is dominated by mastering pipelines and stewardship workflows rather than opportunity/activity tracking. citeturn0search1turn0search21turn0search5

---

### Configuration/service relationship registry

**Purpose**  
A CMDB-style system exists to maintain **accurate, reliable information about digital services and the infrastructure that supports them**, with a strong emphasis on **configuration item (CI) relationships** and service mapping. citeturn8view0turn8view1turn0search14

**Core workflows**  
Across implementations, the repeating workflows are:
- **Discover/import** CIs and attributes from multiple sources. citeturn8view1turn8view2  
- **Identify & reconcile**: prevent duplicates and resolve attribute conflicts using authoritative sources and identification rules (a recurring “reconciliation engine” concept). citeturn8view2turn1search15  
- **Model relationships** among CI instances (depends on / runs on / connects to, etc.). citeturn8view0turn1search2  
- **Service mapping**: assemble CI relationship subsets representing end-to-end service delivery to support diagnostics and impact analysis. citeturn8view1  
- **CI lifecycle management**: decommission/archive, drift validation, periodic certification. citeturn8view2

**Core entities**  
The domain model is unusually stable and graph-shaped:
- CI class hierarchy, CI instance  
- CI attribute, attribute source-of-truth, reconciliation rule  
- Relationship type, relationship edge (CI↔CI)  
- Service CI, service map (subset graph), ownership metadata citeturn8view0turn8view1turn1search15

**Architecture structure**  
A CMDB archetype typically contains:
- **Configuration graph store** (often a relational store with graph semantics or a graph DB abstraction)  
- **Discovery collectors/importers** (horizontal discovery for components + vertical discovery for services)  
- **Identification/reconciliation engine** (dedupe + attribute authority control)  
- **Service mapping layer** (service topology views)  
- **Governance & certification workflows** to keep the graph trustworthy citeturn8view0turn8view1turn8view2turn1search15

**Integrations**  
CMDB systems integrate with discovery sources and with operational processes that consume CI graphs (incident/change/impact workflows), because CI data is only valuable if it drives decisions. citeturn8view0turn8view1

**Example systems**  
- NetBox (“network source of truth”) as an OSS implementation of infrastructure modeling and authoritative inventory/documentation. citeturn3search3turn3search7turn3search29  
- ServiceNow CMDB design guidance (clear articulation of CI classes, relationships, service mapping, and reconciliation engine). citeturn8view0turn8view1turn8view2  
- Atlassian’s CMDB overview reflecting the recurring definition around relationships between hardware/software/networks. citeturn0search14

**Why this is not a variant**  
Although CMDBs often *associate* with IT ticketing, they are not “Incident/Case variants” because the architectural center is a **configuration graph** plus dedupe/reconciliation and discovery-driven maintenance. Ticketing systems optimize queueing/SLA/assignment, whereas CMDB optimizes correctness and navigability of an asset/service dependency model. citeturn8view0turn8view2turn1search2

---

### API management platform

**Purpose**  
An API management system governs and exposes APIs by combining runtime enforcement (gateway) with lifecycle management and developer onboarding (management plane + portal). citeturn0search27turn0search7turn9search7

**Core workflows**  
The repeating lifecycle is strongly consistent across products:
- **Design/publish/version** API definitions into a catalog/portal. citeturn9search7turn0search27  
- **Subscribe/approve** consumers (API keys, subscriptions, usage plans). citeturn0search27turn0search7  
- **Enforce policies** at runtime: authN/authZ, rate limits/quotas, transformations, and governance. citeturn0search3turn0search7turn0search15  
- **Monitor & analyze** traffic (analytics dashboards, logs/metrics). citeturn0search7turn9search7turn0search27  
- **Deprecate/retire** APIs while keeping backward compatibility and audit trails (varies in UX; repeats in governance). citeturn9search7turn0search27

**Core entities**  
Typically stable across implementations:
- API (product), endpoint, version, environment  
- Policy (rate limit, auth, transform), route, backend mapping  
- Consumer application, subscription, credential (key/token), usage plan  
- Analytics metric, alert threshold, audit event citeturn0search27turn0search3turn9search7

**Architecture structure**  
A recurring decomposition appears explicitly in major reference docs:
- **API Gateway** (data plane)  
- **Management plane** (publisher/admin)  
- **Developer portal** (discovery/onboarding/subscriptions)  
- Often: **identity/key manager** and **traffic/policy manager** for distributed throttling and token services citeturn0search27turn9search7turn0search15turn9search3

**Integrations**  
API management integrates with:
- Enterprise identity (OAuth2/OIDC/SAML and JWT validation) and key/token issuance. citeturn9search3turn5search1turn5search2  
- Observability/monitoring pipelines (logs/metrics) and downstream backends (microservices, legacy systems). citeturn0search7turn1search3

**Example systems**  
- entity["company","Amazon Web Services","cloud provider"] enterprise API management reference (security/governance/monitoring responsibilities in API management). citeturn0search7  
- entity["company","WSO2","api management vendor"] documentation describing management-plane portals (Publisher/Developer Portal/Service Catalog) and architecture components. citeturn9search7turn9search3  
- entity["company","Kong","api gateway vendor"] (representative API gateway/policy enforcement component; illustrates repeated need for gateway-level controls like rate limiting). citeturn0search35turn0search3

**Why this is not a variant**  
API management is not just “integration tooling” and not a workflow system: it has a distinct **dual-plane architecture** (gateway + management/portal) and a distinct lifecycle centered on API publication, subscription, and runtime policy enforcement (e.g., rate limiting), which does not reduce to BPM orchestration. citeturn0search27turn0search3turn9search7

---

### Analytics warehouse & BI platform

**Purpose**  
An analytics platform is designed to **integrate, curate, and serve data for analysis** (decision support), not to run operational transactions. It typically unifies data into analytical stores and exposes it through semantic models and reports. citeturn1search12turn1search20

**Core workflows**  
The repeating workflows align closely across architectures:
- **Source onboarding**: connect to operational data sources and extract/load data. citeturn1search12turn1search37  
- **Preparation/curation**: transform, clean, and model data into analysis-friendly forms. citeturn1search12turn1search20  
- **Semantic modeling**: define reusable metrics/relationships (“semantic models”) used across reports. citeturn1search12  
- **Consumption**: dashboards/reports and often downstream serving patterns (APIs/ML features) depending on maturity. citeturn1search12turn1search20  
- **Governance loop**: access control, lineage, and platform operationalization (monitoring, reliability, cost controls). citeturn1search20

**Core entities**  
Common entities repeat regardless of technology choices:
- Data source, connector, dataset  
- Ingestion job, transformation job, schedule  
- Table/view/model, metric/KPI definition, report/dashboard  
- Access policy, lineage metadata, quality rule citeturn1search12turn1search20

**Architecture structure**  
A stable component signature is visible in major guidance:
- **Data ingestion** (batch/stream), often with staging  
- **Storage layer** (warehouse/lakehouse patterns)  
- **Processing layer** (transformations)  
- **Semantic modeling layer**  
- **Reporting/visualization layer** citeturn1search12turn1search20turn1search37

**Integrations**  
Analytics platforms integrate broadly:
- Upstream with operational systems (CRM, ticketing, finance, etc.) for data sources. citeturn1search12  
- Downstream with BI tools and sometimes operational feedback loops (e.g., curated datasets feeding applications). citeturn1search20turn1search12

**Example systems**  
- entity["organization","Apache Superset","oss bi project"] as an OSS BI/reporting layer commonly paired with warehouses (illustrating recurring BI “front end” components). citeturn10search4turn10search16  
- entity["company","Databricks","data platform company"] data ingestion reference architecture showing standardized ingestion foundations into an analytics platform. citeturn1search37  
- Microsoft guidance explicitly enumerating BI solution architecture components (sources → ingestion → warehouse → semantic models → reports). citeturn1search12

**Why this is not a variant**  
Analytics systems differ architecturally from Document Management and Workflow/BPM because they are organized around **data integration, curation, and analytical serving**, with semantic modeling and reporting layers as defining components. Their “lifecycle” is data pipeline + model governance, not document versioning or long-running approval orchestration. citeturn1search12turn1search20

---

### Enterprise search & knowledge discovery platform

**Purpose**  
Enterprise search systems enable users (or applications) to find relevant content across a heterogeneous enterprise landscape (structured + unstructured sources), while enforcing permissions and ranking results. citeturn1search1turn1search22

**Core workflows**  
A highly repeatable end-to-end loop appears across products:
- **Collect**: crawl/connect to repositories through connectors/APIs. citeturn1search22  
- **Index**: normalize content, extract metadata, and build searchable indexes. citeturn1search22turn1search7  
- **Query & rank**: query processing, ranking/relevance tuning, and results presentation. citeturn1search22turn1search1  
- **Security enforcement**: ensure users only see results they are allowed to see; often combines index-time and query-time controls. citeturn1search22turn1search14

**Core entities**  
Common entities across implementations:
- Source/connector, crawl job, document/content item  
- Metadata fields, extracted permissions/ACL  
- Index/shard, query, ranking profile/relevance configuration  
- User identity reference and authorization context citeturn1search22turn1search14

**Architecture structure**  
The signature looks like a pipeline + serving stack:
- **Connector framework** (source adapters, incremental sync)  
- **Ingestion/processing pipeline** (parsing, enrichment, dedupe)  
- **Indexing layer** (text/vector indexes depending on system)  
- **Query/ranking layer** (relevance logic, query rewriting)  
- **Access control layer** integrated into retrieval (“security trimming”) citeturn1search22turn1search14

**Integrations**  
Enterprise search integrates with:
- Content systems (document repositories, wikis, ticketing, source control, intranet/search portals) via connectors. citeturn1search22turn1search1  
- IAM systems for identity context and permissions propagation/validation. citeturn1search22turn5search0

**Example systems**  
- entity["company","Elastic","search company"] enterprise search framing (enterprise search as a solution for finding information within organizations). citeturn1search1  
- entity["company","Happeo","intranet software company"] description of enterprise search as connector → index → query pipelines with security enforcement. citeturn1search22

**Why this is not a variant**  
Enterprise search is not “Document Management” because it is not primarily a repository-of-record. Its defining architectural challenge is **federated ingestion and secure retrieval across many systems**, including permission synchronization and relevance tuning—capabilities that remain distinct even when documents are among the indexed sources. citeturn1search22turn1search14

---

### Observability platform

**Purpose**  
An observability platform ingests telemetry to make systems understandable and operable, typically by collecting and correlating logs, metrics, and traces and driving alerts/dashboards. citeturn1search3turn1search29turn1search21

**Core workflows**  
Recurring operational workflows are consistent across tools:
- **Instrument & collect** telemetry signals (agent/SDK/collector patterns). citeturn3search2turn3search18  
- **Ingest & process** (filter, enrich, sample/aggregate, route) via pipelines. citeturn3search2  
- **Store & query** across signal types (time series for metrics; event/log stores; trace stores). citeturn1search3turn1search29  
- **Alert** on conditions and route notifications; **triage** using correlated evidence across signals. citeturn1search29turn1search3

**Core entities**  
Common entities repeat across platforms:
- Signal (log/metric/trace), resource/service, attribute/tag  
- Time series, span, log event, trace graph  
- Dashboard, query, alert rule, incident/notification routing configuration citeturn1search3turn3search10

**Architecture structure**  
A recognizable architecture signature:
- **Collector/agent layer** with configurable pipelines (receive → process → export). citeturn3search2turn3search18  
- **Storage backends** optimized per signal type  
- **Query/visualization layer** (dashboards)  
- **Alerting engine** and integrations to incident/ticket systems citeturn1search29turn1search21

**Integrations**  
Observability deeply integrates with:
- Application/runtime environments for telemetry emission and metadata enrichment. citeturn3search10turn1search3  
- Ticket/case systems and on-call workflows for incident response handoff. citeturn1search29turn1search3

**Example systems**  
- entity["organization","OpenTelemetry","observability standard project"] collector architecture explicitly defined as pipeline-based receiving/processing/exporting to multiple backends. citeturn3search2turn3search18  
- entity["company","Datadog","observability company"] definition emphasizing the three pillars (metrics/logs/traces) for visibility into complex systems. citeturn1search29  
- entity["company","Grafana","observability company"] documentation framing observability as making internal state transparent via data produced by systems. citeturn1search21

**Why this is not a variant**  
Observability is architecturally distinct from “infrastructure tools” like a single metrics DB because it is a **full system**: multi-signal ingestion pipelines, correlation semantics, storage/query layers, and a closed-loop alerting workflow. Its domain model (signals, spans, time series, alerts) does not reduce to workflow or ticket records, even though it commonly integrates with them. citeturn3search2turn1search3turn1search29

---

### Order management system

**Purpose**  
An OMS is the operational hub that **tracks and coordinates the order lifecycle from capture to fulfillment and returns**, often federating across multiple channels and fulfillment systems. citeturn2search2turn2search10turn2search6

**Core workflows**  
A stable lifecycle pattern appears across OMS descriptions and integrations:
- **Capture** orders from channels (web, POS, marketplace, call center) and normalize them. citeturn2search10turn2search2  
- **Validate** (fraud/payment authorization, inventory availability), then **reserve/allocate** inventory. citeturn2search10turn2search2  
- **Orchestrate fulfillment** steps across WMS/3PL/warehouse and shipping carriers; update order status. citeturn2search2turn2search6  
- **Handle returns/exchanges** and post-purchase lifecycle closure. citeturn2search18turn2search2

**Core entities**  
Order-centered domain entities repeat across implementations:
- Order, order line, shipment, fulfillment task  
- Customer reference, address, payment authorization/transaction reference  
- Inventory reservation/allocation, channel, return/claim  
- Status history (event stream), audit trail citeturn2search2turn2search10turn2search6

**Architecture structure**  
A characteristic OMS architecture is “hub + orchestrations + connectors”:
- **Order lifecycle engine** (state machine + event history)  
- **Integration boundary** to inventory, warehouse, shipping, payment, billing systems  
- **Orchestration layer** for long-running fulfillment steps (often event-driven)  
- **Customer communication adapters** (status tracking, notifications) citeturn2search6turn2search2turn2search10

**Integrations**  
OMS is defined by integration topology, sitting in the middle of:
- Commerce front ends and marketplaces, inventory management, WMS/3PL, shipping carriers, billing/ERP. citeturn2search6turn2search10turn2search2

**Example systems**  
- Oracle documentation describing integrated order lifecycle management topology and central order management role in order-to-cash integration. citeturn2search6  
- Salesforce OMS overview describing “start to finish” order management and lifecycle transparency. citeturn2search2

**Why this is not a variant**  
An OMS can *contain* workflows, but it is not “Workflow/BPM” because its defining shape is a **domain-specific lifecycle engine** centered on orders, inventory reservation, fulfillment coordination, and returns—plus deep integrations to logistics and payment/billing systems. Those integrations and entity constraints are core to the archetype, not optional add-ons. citeturn2search6turn2search10turn2search2

## Boundary clarifications and rejected candidates

Some frequently suggested “system types” are better modeled as variants or reusable capabilities rather than new archetypes:

A standalone **notification system** (routing email/SMS/push) is typically a capability embedded in ticketing, collaboration, IAM (MFA), OMS (status updates), and observability (alerts), rather than a complete archetype with its own stable enterprise domain model. This is visible in how observability and collaboration docs treat notifications as part of the platform rather than the platform itself. citeturn1search29turn4search4turn4search20

A **rules engine** often appears as a cross-cutting capability (e.g., MDM survivorship rules; API policies like rate limiting; IAM authorization policies), but does not consistently form an independent system-of-record with repeated enterprise workflows unless coupled to a broader archetype. citeturn0search21turn0search3turn0search4

A **data pipeline orchestrator** (e.g., Apache Airflow) provides workflow scheduling/monitoring and can be treated as either (a) a specialized variant of Workflow/BPM for batch/data tasks, or (b) a capability inside the analytics archetype—depending on how your catalog draws boundaries. Its own docs define it as workflow scheduling/monitoring, reinforcing this adjacency to workflow orchestration. citeturn10search6turn10search2

A **search engine** (index + query) is a component used in enterprise search, observability/log analytics, and other retrieval-heavy systems; the enterprise-search archetype is the *multi-connector secure retrieval system* built around it. citeturn1search22turn10search3

## Archetype relationship map

The map below describes common relationships between your existing archetypes and the proposed additions, emphasizing **integration boundaries and data/control-flow**.

**IAM → (all operational systems)**  
IAM provides federated authentication/authorization and provisioning to virtually every other archetype (CRM, ticketing, document/workflow, Analytics Platforms, search, collaboration). Protocol standards and SCIM provisioning explicitly target multi-domain enterprise-to-cloud interoperability. citeturn5search1turn5search2turn5search0turn0search28

**MDM ↔ CRM and OMS (and others)**  
MDM publishes mastered party/product/location data to consuming operational systems; CRM consumes customer master data, and OMS consumes product/customer/location masters and often emits transactional facts that later feed analytics. This hub-and-spoke “golden record” positioning is explicit in MDM architecture guidance. citeturn0search1turn0search5

**CMDB ↔ Case/Ticket and Workflow/BPM**  
CMDB graphs (CIs + relationships + service maps) are commonly used by incident/change/impact workflows; CMDB guidance explicitly positions service mapping and relationship modeling as critical for diagnosing service issues and managing CI lifecycle correctness. citeturn8view1turn8view2turn1search2

**API management → integration fabric for multiple archetypes**  
API management frequently becomes the “front door” to back-end services owned by CRM, case systems, OMS, and other operational systems, enforcing consistent runtime policies (e.g., rate limit) and onboarding consumers through a developer portal. citeturn0search27turn0search3turn0search7turn9search7

**Analytics platform ← (all systems) → feeds back into operations**  
Analytics architecture guidance explicitly assumes many upstream data sources and a layered pipeline into semantic models and reports; MDM and OMS commonly contribute mastered and transactional datasets respectively. citeturn1search12turn1search20turn0search5turn2search2

**Enterprise search ↔ Document management / wiki / ticketing / collaboration**  
Enterprise search systems are shaped by connectors to many repositories and by secure indexing/query enforcement; it frequently indexes content from document repositories, collaboration tools, and ticketing systems while respecting permissions. citeturn1search22turn1search14turn1search1

**Observability → Case/Ticket and Workflow/BPM**  
Observability platforms operationalize telemetry into alerts and investigation workflows; operational response frequently routes to case/ticket records, with observability providing the evidence substrate (logs/metrics/traces). citeturn1search29turn1search3turn3search2