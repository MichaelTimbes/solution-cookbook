# Two-Level Software Cookbook Landscape Research

## A. Executive Summary

**Finding: a substantial unified two-level cookbook does not exist in public literature.**  
Across reputable books, standards, vendor architecture centers, and open-source “handbooks,” the ecosystem is rich—but **fragmented**. The strongest sources tend to specialize in **either**:

- **Level 1 (archetypes / product-system blueprints):** what “a CRM” or “a ticketing system” includes, its modules, workflows, and high-level information model; or  
- **Level 2 (capability recipes):** reusable “front-to-back” solutions like outbox/idempotency, workflow approvals, saved views, audit logs, notification preferences, form/survey engines.

What’s missing is a single coherent cookbook that consistently delivers **both levels** *and* includes end-to-end artifacts (UI + API + data model + background jobs + observability + failure modes) in a reusable way.

### Evidence for the “no unified cookbook” conclusion

**Level 1 sources exist but are typically narrow or domain-bound.**  
A concrete example in the CRM archetype is the academic/reference-architecture work that identifies common CRM modules and system interactions (e.g., Account, Sales, Marketing, Service, Scheduler, Administration; plus portal/contact center/KB/workflow/analytics integrations). citeturn12view0turn12view2turn12view1  
This is closer to “product shape” than most architecture books—but it is primarily application-layer architecture and does not deliver broad Level 2 recipes across archetypes (nor deep ops/observability guidance). citeturn12view1turn12view3

**Level 2 sources exist but rarely include full product archetypes.**  
For example, reliable messaging patterns like **Transactional Outbox** and **Idempotent Consumer** are well documented as patterns, including key failure modes (e.g., duplicate publish => consumer must be idempotent). citeturn15search0turn15search12  
But these sources generally do not say what a CRM / CMS / DMS “typically includes” as a product blueprint.

**End-to-end “capability implementations” do exist, but each capability is scattered across multiple sources.**  
A single capability such as “saved views + filters” often spans an admin UX library (e.g., index filters + saved views) citeturn16search0 and an implementation framework (how filters persist and flow via URL or storage) citeturn16search14turn16search7 plus observability guidance (context propagation) citeturn35search0, but no single place connects them into a consistent recipe template across archetypes.

### The closest “small set” combination that approximates a two-level cookbook

No small set fully closes the gap, but the closest practical bundle looks like this:

1. **Archetype/industry component models and API data models:**  
   - **TM Forum Open Digital Architecture + Open APIs** (Apache-2.0 licensed repos) provide large-scale componentization and concrete API/data models for telco/OSS-BSS-style business capabilities. citeturn21search9turn21search0turn21search7  
2. **Capability pattern catalogs (backend + reliability):**  
   - Microservices.io patterns for saga/outbox/idempotency citeturn15search8turn15search0turn15search12, Debezium’s outbox implementation guidance citeturn15search1, and strongly operational sources like Release It! (via publisher page) citeturn5search2 plus OpenTelemetry concepts/specs citeturn35search4turn35search22  
3. **Admin UX patterns for data-heavy products:**  
   - Polaris index filters + saved views citeturn16search0turn16search12 and react-admin saved queries / persistence primitives citeturn16search3turn16search14

Even combined, this bundle still leaves major gaps: cross-archetype product blueprints, canonical data model skeletons, and unified end-to-end recipes tied to real failure modes and operational runbooks.

## B. Source Matrix

### Rubric (0–3)
- **L1**: Covers Level 1 archetypes (product/system blueprints)  
- **L2**: Covers Level 2 capability recipes (end-to-end solutions)  
- **Prac**: Practicality (steps, pitfalls, tradeoffs, failure modes)  
- **Impl**: Implementation guidance (data model + APIs + workflows)  
- **UX**: UX guidance (admin patterns, tables/filters, dashboards)  
- **Ops**: Ops guidance (observability, retry, idempotency, monitoring)  
- **Reuse**: Licensing allows reuse/adaptation for a community cookbook (constraints noted)

> **Link column uses citations as clickable sources** (per the “no raw URLs” constraint).

| Source | Category | Type | Pub date | What it covers (why it resembles the cookbook) | Link | L1 | L2 | Prac | Impl | UX | Ops | Reuse | License notes |
|---|---|---|---:|---|---|---:|---:|---:|---:|---:|---:|---:|---|
| entity["book","Patterns of Enterprise Application Architecture","fowler 2002"] | Enterprise patterns/books | Book | 2002 | Canonical enterprise app patterns (domain logic, data mapping, transaction script vs domain model). Great “recipe” building blocks but not archetype blueprints. citeturn4search18 | citeturn4search18 | 0 | 2 | 2 | 2 | 0 | 1 | 1 | Copyrighted; reuse is via paraphrase only. |
| entity["book","Analysis Patterns","fowler 1996"] | Enterprise patterns/books | Book | 1996 | Domain object model patterns across domains; useful for “data model skeleton thinking.” citeturn7search0turn7search12 | citeturn7search0 | 1 | 1 | 1 | 1 | 0 | 0 | 1 | Copyrighted; not a sharable cookbook directly. |
| entity["book","Enterprise Integration Patterns","hohpe woolf 2003"] | Integration patterns | Book/site | 2003 | “Pattern catalog” for messaging/routing; foundational Level 2 integration recipes (conceptual, not full UI). citeturn4search19 | citeturn4search19 | 0 | 2 | 2 | 1 | 0 | 2 | 1 | Copyrighted (book); concepts reusable, text not. |
| entity["book","Designing Data-Intensive Applications","kleppmann 2017"] | Enterprise patterns/books | Book | 2017 | Deep reliability/data tradeoffs: streams, storage, consistency; great for failure modes + ops thinking. citeturn5search7 | citeturn5search7 | 0 | 2 | 2 | 2 | 0 | 2 | 1 | Copyrighted; reuse via synthesis only. |
| entity["book","Release It! Second Edition","nygard 2018"] | Enterprise patterns/books | Book | 2018 | Production failure modes and resilience patterns; excellent ops-focused “recipe” input. citeturn5search2 | citeturn5search2 | 0 | 2 | 3 | 1 | 0 | 3 | 1 | Copyrighted; reuse via synthesis only. |
| entity["book","Site Reliability Engineering","google 2016"] | Ops guidance | Book (free online) | 2017 (online text) | Monitoring/SLO/toil/incident practices; strong ops “chapter recipes.” Licensed CC BY‑NC‑ND 4.0 (no derivatives). citeturn36search3turn5search14 | citeturn36search3 | 0 | 1 | 2 | 1 | 0 | 3 | 0 | CC BY‑NC‑ND prevents derivative cookbook content. citeturn36search3 |
| entity["organization","TM Forum","industry association"] Open APIs repos | Capability maps / composable | Standard + OSS repos | active | Concrete API + data model assets, published as Apache-2.0 repos; provides reusable domain APIs (catalog, customer, order, payment). citeturn21search0turn21search7turn20search1 | citeturn21search0 | 2 | 2 | 2 | 3 | 1 | 1 | 3 | Apache-2.0 enables reuse; still telco-shaped. citeturn21search0 |
| entity["organization","The Open Group","standards consortium"] IT4IT | Capability maps / composable | Standard (PDF) | (varies) | “Value chain” operating model for IT management; helps taxonomy thinking more than exact product blueprints. citeturn20search4turn20search24 | citeturn20search24 | 1 | 0 | 1 | 0 | 0 | 0 | 1 | Standard access/licensing varies; not a permissive cookbook. citeturn20search24 |
| entity["organization","APQC","process framework org"] PCF | Capability maps / composable | Standard/framework | 1992+ | Widely used process taxonomy; helps Level 1 “map” but reuse restricted by APQC terms. citeturn20search18turn21search6 | citeturn20search18 | 2 | 0 | 1 | 0 | 0 | 0 | 0 | Terms restrict redistribution/public display. citeturn21search6 |
| CRM reference architecture (Cruz dissertation) | Reference architectures / archetypes | Thesis/PDF | 2015 | Explicit CRM modules + interacting systems; closer to Level 1 blueprint than most. citeturn12view0turn12view2turn12view1 | citeturn12view0 | 3 | 0 | 1 | 1 | 0 | 0 | 1 | Academic document; reuse depends on institution/publisher; safest via paraphrase. citeturn11view1 |
| IBM Case Manager Redbook | BPM / case mgmt | Book/PDF | 2015 | End-to-end case management build guidance incl. UI widgets + external data services; concrete for case/ticket archetype + some recipes. citeturn13search6turn8view1 | citeturn13search6 | 3 | 2 | 2 | 2 | 2 | 1 | 1 | IBM Redbooks are redistributable PDFs but not permissive for derivative reuse. citeturn13search6 |
| entity["organization","Salesforce","crm company"] Integration Patterns (architect portal) | Integration patterns | Vendor pattern catalog | active | Maintained integration pattern guides and selection matrices; strong Level 2 integration guidance (platform-specific). citeturn13search1turn13search17 | citeturn13search1 | 1 | 2 | 2 | 1 | 0 | 2 | 0 | Vendor docs reuse constrained by terms; adapt via synthesis. citeturn13search1 |
| entity["company","Amazon Web Services","cloud provider"] SaaS architecture fundamentals | Reference architectures | Vendor whitepaper | active | Multi-tenancy models + tradeoffs; strong infra-to-platform guidance but not product archetypes. citeturn13search2turn13search18 | citeturn13search2 | 0 | 1 | 2 | 1 | 0 | 2 | 0 | Vendor docs; reuse constrained. citeturn13search2 |
| AWS SaaS Factory EKS reference architecture repo | Reference architectures | OSS sample | active | End-to-end SaaS reference arch incl. isolation/identity/routing/ops; helpful “platform recipe.” citeturn13search22 | citeturn13search22 | 0 | 1 | 2 | 2 | 0 | 2 | 2 | GitHub sample licensing varies by repo; verify per repo before reuse. citeturn13search22 |
| BPMN (OMG) | BPM/workflow | Standard | 2010/2014 | Standard process notation intended to bridge business and implementation precision. citeturn14search4turn14search7 | citeturn14search7 | 0 | 1 | 1 | 0 | 0 | 0 | 1 | Spec IPR modes apply; reuse is via referencing standard. citeturn14search7 |
| DMN (OMG) | Rules / decisioning | Standard | 2021 (DMN 1.3) | Standard for decision models + expression language; helps rules-engine recipe structure. citeturn14search1 | citeturn14search1 | 0 | 2 | 1 | 1 | 0 | 0 | 1 | Spec licensing/terms apply; use as referenced standard. citeturn14search1 |
| entity["company","Camunda","bpm vendor"] Best Practices | BPM/workflow | Vendor docs | active | Practical implementation best practices for BPMN/DMN on Camunda stack. citeturn14search2turn14search14 | citeturn14search2 | 1 | 2 | 2 | 2 | 1 | 1 | 0 | Vendor docs reuse constrained; concepts reusable. citeturn14search2 |
| entity["company","Temporal Technologies","workflow company"] Use cases + cookbook | BPM/workflow | Docs/cookbook | 2025–2026 | Human-in-the-loop and durable workflow patterns (signals, timers); concrete recipe-style guidance (often code). citeturn14search6turn14search3turn14search9 | citeturn14search6 | 1 | 3 | 3 | 2 | 0 | 2 | 0 | Docs reuse constrained; strong recipe exemplar. citeturn14search6 |
| Microservices.io patterns | Integration patterns | Pattern catalog | active | Transactional outbox, saga, idempotent consumer and related patterns with rationale and key failure modes. citeturn15search0turn15search8turn15search12 | citeturn15search4 | 0 | 3 | 3 | 2 | 0 | 2 | 0 | Site content is copyrighted; reuse via synthesis only. citeturn15search4 |
| entity["organization","Debezium","cdc project"] Outbox docs | Integration patterns | OSS docs | stable | Concrete outbox implementation: outbox table + CDC connector + routing transforms; includes consistency story. citeturn15search1turn15search5turn15search9 | citeturn15search1 | 0 | 3 | 3 | 3 | 0 | 2 | 2 | OSS docs generally reusable per project license; verify per repo. citeturn15search1 |
| entity["company","Stripe","payments company"] idempotency + billing webhooks docs | Payments/billing + reliability | Vendor API docs | active | Concrete idempotency semantics + billing event flows; great “capability recipe” input. citeturn15search3turn32search2turn32search10 | citeturn15search3 | 1 | 3 | 3 | 2 | 0 | 2 | 0 | Vendor docs reuse constrained; behaviors are referenceable. citeturn15search3 |
| entity["organization","OpenTelemetry","observability project"] spec + concepts | Ops guidance | Spec + OSS | active | Vendor-neutral observability model: context propagation, semantic conventions; supports “observability” section in recipes. citeturn35search0turn35search1turn35search22 | citeturn35search4 | 0 | 2 | 2 | 1 | 0 | 3 | 3 | Apache-2.0 spec repo supports reuse/adaptation. citeturn35search1 |
| Shopify Polaris (Index filters, saved views) | UX pattern libraries | Design system docs | active | Concrete admin UX patterns: filtering/search/sort + saved views for “index” tables. citeturn16search0turn16search12 | citeturn16search0 | 0 | 2 | 3 | 1 | 3 | 0 | 2 | Polaris code is MIT, but product-context constraints exist; verify scope. citeturn37search1turn37search21 |
| entity["organization","Atlassian","software company"] Design System + Dynamic Table | UX pattern libraries | Design system docs | active | Data-heavy UI components (sorting/pagination/drag) + admin primitives; strong UX reference. citeturn16search5turn37search2 | citeturn16search5 | 0 | 1 | 2 | 0 | 3 | 0 | 0 | License grant is limited to Atlassian add-ons context. citeturn37search2turn37search10 |
| Salesforce Lightning Design System repo | UX pattern libraries | Design system + OSS assets | active | Data table and “displaying data” patterns; code packages are BSD-3; icons/images may be separately licensed. citeturn16search2turn38search4turn38search0turn38search9 | citeturn38search4 | 0 | 1 | 2 | 1 | 3 | 0 | 2 | Multiple licenses/asset constraints; treat as partial reuse. citeturn38search0 |
| React-admin (SavedQueriesList, filter persistence) | UX + implementation | OSS framework docs | active | Practical admin implementation: filter state in URL/localStorage + saved queries component. citeturn16search3turn16search14turn37search0 | citeturn16search3 | 0 | 2 | 3 | 2 | 2 | 0 | 3 | MIT license enables reuse/adaptation. citeturn37search0 |
| SurveyJS Form Library | Survey/form engines | OSS library docs | active | JSON-based dynamic forms, conditional logic, branching; MIT licensed. citeturn17search13turn17search1turn17search9 | citeturn17search13 | 0 | 3 | 2 | 2 | 2 | 0 | 3 | MIT license supports reuse. citeturn17search13 |
| ODK + XLSForm | Survey/form engines | Standard + OSS docs | active | Spreadsheet-authored forms with complex logic; portability + versioning via .xlsx workflows. citeturn17search20turn17search4 | citeturn17search20 | 0 | 2 | 2 | 1 | 1 | 0 | 2 | Mixed licensing; generally open. Verify per repo. citeturn17search4 |
| Form.io JSON schema / builder docs | Survey/form engines | Platform + OSS components | 2024–2025 | Schema-driven forms; builder generates schema and (platform) APIs; strong end-to-end idea but licensing is mixed. citeturn17search10turn17search14 | citeturn17search10 | 0 | 2 | 2 | 2 | 2 | 0 | 1 | Some OSS components; platform/commercial terms apply. citeturn17search10 |
| docxtemplater | Document generation | OSS library | active | Practical docx templating; dual-licensed (MIT/GPLv3). citeturn18search0turn18search13 | citeturn18search0 | 0 | 2 | 2 | 2 | 0 | 0 | 2 | MIT path is reusable; GPLv3 considerations if chosen. citeturn18search0 |
| Liquid template language | Document generation / templating | OSS language | 2006+ | Safe, non-eval templating separation of compile/render; useful merge-field recipe input. citeturn18search1turn18search5 | citeturn18search5 | 0 | 2 | 1 | 1 | 0 | 0 | 3 | MIT licensed (repo). citeturn18search1 |
| docassemble | Document generation | OSS system | active | Guided interviews + document assembly; code MIT, docs CC BY 3.0 (derivative-friendly). citeturn18search12turn18search2 | citeturn18search12 | 1 | 2 | 2 | 2 | 2 | 1 | 3 | Strong reuse posture (MIT code, CC BY docs). citeturn18search12 |
| Twilio SendGrid unsubscribe groups | Notification patterns | Vendor docs | active | Preference groups (“types of email”), API-managed suppression; concrete for notification-preferences recipe. citeturn19search0turn19search4 | citeturn19search0 | 0 | 2 | 2 | 1 | 1 | 0 | 0 | Vendor docs reuse constrained. citeturn19search0 |
| RFC 8058 one-click unsubscribe | Notification patterns | Standard (IETF RFC) | 2017 | Standard method for safe one-click list unsubscribe signaling. citeturn19search2 | citeturn19search2 | 0 | 1 | 1 | 0 | 0 | 0 | 2 | RFCs are publicly readable; cookbook can reference/implement. citeturn19search2 |
| Nextcloud logging + admin audit app | DMS / audit log | OSS admin docs | active | Shows audit.log separation + logging configuration; concrete “audit capability” in a DMS context. citeturn25search1turn25search5 | citeturn25search1 | 2 | 1 | 2 | 1 | 0 | 1 | 2 | OSS docs; verify Nextcloud license if reusing text. citeturn25search1 |
| CMIS 1.1 (OASIS) | DMS / CMS interoperability | Standard | 2012+ | Defines a **domain model + REST/JSON bindings** for content repositories—rare example of an archetype-ish standard. citeturn25search0turn25search4 | citeturn25search0 | 2 | 1 | 1 | 2 | 0 | 0 | 1 | Standards reuse depends on OASIS terms; implementers can build on it. citeturn25search0 |
| Alfresco audit / REST audit logs docs | DMS / audit log | Vendor docs | active | Shows audit disabled-by-default for perf + REST management of audit logs. citeturn25search6turn25search14 | citeturn25search6 | 2 | 1 | 2 | 2 | 0 | 1 | 0 | Vendor docs reuse constrained. citeturn25search6 |
| Zammad triggers + scheduler | Case/ticket systems | OSS admin docs | active | End-to-end automation inside ticketing: if/then triggers + scheduled jobs; practical. citeturn26search0turn26search16turn26search12 | citeturn26search0 | 2 | 2 | 3 | 1 | 1 | 1 | 2 | Zammad OSS licensing varies by edition; verify for reuse. citeturn26search0 |
| GLPI ticket mgmt + notifications | Case/ticket systems | OSS docs | 2025–2026 | ITIL-aligned ticket workflow notions + notifications; useful archetype reference. citeturn26search17turn26search1turn26search5 | citeturn26search17 | 2 | 1 | 2 | 1 | 1 | 0 | 2 | OSS project docs; verify license for derivative reuse. citeturn26search17 |
| ERPNext CRM docs | Open-source building blocks | OSS docs | 2026 | Concrete CRM flows (lead → opportunity → quotation → sales order). citeturn22search0turn22search14 | citeturn22search0 | 2 | 1 | 2 | 1 | 1 | 0 | 2 | GPLv3 code; docs CC BY-SA 3.0. citeturn23search3 |
| Cal.com API + repo | Scheduling archetype | OSS product + API docs | active | Scheduling platform with booking APIs; shows recurring booking types; AGPLv3 constraints. citeturn27search10turn28search4turn28search0 | citeturn27search10 | 2 | 1 | 2 | 2 | 1 | 0 | 1 | AGPLv3 impacts reuse in downstream products. citeturn28search0turn28search4 |
| Timefold employee scheduling docs | Scheduling/rostering | OSS docs + sample | active | Gives explicit input dataset model (shifts + availability), plus examples; good recipe skeleton. citeturn27search1turn28search9 | citeturn27search1 | 1 | 2 | 2 | 2 | 0 | 0 | 3 | Apache-2.0 community edition supports reuse. citeturn28search9 |
| Kill Bill docs + overdue/dunning | Payments/billing | OSS platform docs | active | Practical billing internals: invoices, payment retries, overdue policies; strong failure-mode guidance. citeturn32search7turn32search3turn32search1 | citeturn32search7 | 2 | 3 | 3 | 2 | 0 | 2 | 3 | Apache-2.0 code; docs generally reusable with attribution norms. citeturn32search1 |
| Apache Superset security + dashboards docs | Analytics Platform | OSS project docs | active | RBAC/permissions + dashboard access patterns; Analytics Platform archetype reference. citeturn29search0turn29search8turn29search6 | citeturn29search0 | 2 | 1 | 2 | 1 | 1 | 1 | 3 | Apache-2.0. citeturn29search6 |
| Metabase permissions docs | Analytics Platform | OSS/commercial docs | active | Practical permissions model (data vs collection permissions); good admin UX guidance. citeturn29search9turn29search1turn29search15 | citeturn29search9 | 2 | 1 | 2 | 1 | 2 | 0 | 1 | Mixed licensing (AGPL + commercial). citeturn29search15turn29search3 |
| NIST SP 800-63-4 | Identity/CIAM | Standard | 2025 | Current digital identity guidelines suite covering proofing/auth/federation requirements. citeturn33search3turn33search0 | citeturn33search3 | 1 | 1 | 2 | 0 | 0 | 1 | 2 | Public standard guidance; can be referenced/implemented. citeturn33search3 |
| OAuth 2.0 + OIDC + SCIM RFCs/specs | Identity/CIAM | Standards | 2012–2015+ | Core protocols for CIAM APIs, auth flows, and provisioning—essential for archetype blueprint & recipes. citeturn33search1turn33search5turn33search2 | citeturn33search1 | 2 | 2 | 1 | 1 | 0 | 0 | 2 | Standards are referenceable; implementers can build compliant systems. citeturn33search1 |
| Keycloak server admin docs | Identity/CIAM | OSS product docs | 2026 | Shows protocol-based architecture (OIDC/SAML); practical admin-server model. citeturn22search5turn23search2 | citeturn22search5 | 2 | 1 | 2 | 1 | 1 | 1 | 3 | Apache-2.0. citeturn23search2 |

## C. Best-of shortlist

These ten are the most “cookbook-like,” either because they provide **pattern catalogs**, **explicit product shapes**, or **end-to-end implementation artifacts**.

**TM Forum Open APIs + ODA assets** — The rare combination of *domain API specs plus data-model schemas* published under Apache-2.0, which makes it uniquely reusable for a community cookbook. It is also one of the few ecosystems that treats “capabilities” as composable building blocks with shared models. citeturn21search0turn20search1turn21search9

**Cruz CRM reference architecture (2015)** — One of the clearest public attempts to define a CRM reference application architecture with explicit modules and system interactions, i.e., the kind of Level 1 “shape of a CRM” material that is usually proprietary. citeturn12view0turn12view2turn12view1

**IBM Case Manager Redbook (2015)** — Extremely concrete for case management: it covers UI widgets/extensions and external data services integration, which looks like real “front-to-back” recipe content rather than pure infrastructure diagrams. citeturn13search6turn8view1

**Microservices.io patterns** — Strongest concise public catalog for outbox/idempotency/sagas with clear failure-mode rationale, highly aligned with the Level 2 integration examples in your prompt. citeturn15search0turn15search8turn15search12

**Debezium Outbox documentation** — Turns the outbox pattern into an implementable pipeline (outbox table + CDC + routing transforms), which is closer to “recipe” than most pattern writeups. citeturn15search1turn15search9

**Temporal use cases + cookbook pages** — Strongest modern “workflow recipe” style for human-in-the-loop and durable orchestration, with explicit emphasis on long-running processes and durable human input. citeturn14search6turn14search3turn14search9

**Kill Bill billing platform docs** — One of the few open-source ecosystems that deeply documents billing internals, including overdue/dunning and payment retry schedules—ideal for payments/billing archetype plus failure modes. citeturn32search7turn32search3turn32search1

**Shopify Polaris index filters + table views** — Excellent concrete admin UX pattern reference: filtering/search/sort plus saved views and bulk actions. This is highly aligned with “enterprise admin UX,” a gap in most architecture books. citeturn16search0turn16search12

**React-admin saved queries + filter persistence** — A practical implementation template for saved views and list-state persistence; it provides reusable UI building blocks that map directly to your Level 2 “search/filters/saved views” recipe. citeturn16search3turn16search14turn37search0

**OpenTelemetry specification + concepts** — The most reusable, vendor-neutral foundation for observability sections in recipes, including context propagation and semantic conventions. citeturn35search0turn35search1turn35search22

## D. Coverage Map

### Level 1 archetypes coverage

**CRM** — Cruz CRM reference architecture; ERPNext CRM docs and flows; Odoo CRM docs. citeturn12view0turn12view2turn22search0turn22search9  
**CMS / Wiki / Knowledge Base** — Strapi content-type builder + auto-generated REST endpoints (headless CMS); MediaWiki templates/infobox patterns for wiki knowledge shaping. citeturn24search0turn24search16turn24search2turn24search6  
**Document Management System** — CMIS standard (domain model + REST/JSON binding); Nextcloud versioning/retention/logging + admin audit app; Alfresco auditing. citeturn25search0turn25search4turn24search7turn25search1turn25search6  
**Case/Ticket system** — IBM Case Manager Redbook; Zammad triggers/scheduler; GLPI ticket management + notifications + ITIL alignment. citeturn13search6turn26search0turn26search16turn26search17turn26search1  
**Workflow / BPM system** — BPMN and DMN standards; Camunda best practices; Temporal workflow patterns. citeturn14search7turn14search1turn14search2turn14search6  
**Payments / Billing** — Kill Bill docs (open-source billing product shape); Stripe billing webhooks + invoice lifecycle docs as a “reference SaaS billing shape.” citeturn32search7turn32search10turn32search2  
**Scheduling / Rostering** — Cal.com booking APIs; Timefold employee shift scheduling data model examples. citeturn27search10turn27search1  
**Inventory / Catalog** — TM Forum Product Catalog API repo; Saleor product/variant/attribute object model; Medusa inventory module flows; ERPNext item variants/stock ledger patterns. citeturn21search7turn30search0turn30search7turn30search2turn30search11  
**Analytics Platform** — Superset roles/permissions + dashboard access; Metabase data vs collection permissions model. citeturn29search0turn29search8turn29search9turn29search1  
**Identity / Access (CIAM)** — OAuth/OIDC/SCIM specs; NIST identity guidelines; Keycloak admin architecture. citeturn33search1turn33search5turn33search2turn33search3turn22search5

### Level 2 capabilities coverage

**Custom fields / extensible attributes** — Strapi content-type builder (schema evolution + relations); SuiteCRM custom fields; EAV guidance + pitfalls literature; Saleor “attributes” model; ERPNext item variants. citeturn24search0turn22search4turn34search13turn34search1turn30search6turn30search2  
**Dynamic evaluation / survey engine** — SurveyJS JSON-based dynamic forms + branching logic; ODK/XLSForm portable spreadsheet-authored forms; Form.io schema-driven builder (mixed licensing). citeturn17search13turn17search9turn17search20turn17search10  
**Approval workflows / human-in-the-loop orchestration** — Temporal human-in-the-loop examples; BPMN standard + Camunda practices. citeturn14search3turn14search6turn14search7turn14search2  
**Template/merge fields** — Liquid’s safe template language; docxtemplater; docassemble document assembly + interview logic; MediaWiki templates/infobox. citeturn18search1turn18search0turn18search12turn24search2turn24search6  
**Notification preferences + routing** — SendGrid unsubscribe/suppression groups; Twilio advanced opt-out; RFC 8058 one-click unsubscribe. citeturn19search0turn19search5turn19search2  
**Search / filters / saved views** — Polaris index filters + saved views; react-admin saved queries + persistence; Zammad “overviews/object conditions” as saved lists. citeturn16search0turn16search3turn16search14turn26search20  
**Import/export pipelines** — Medusa file service overview (imports/exports depend on storage services) and inventory flows; TM Forum API schemas for interchange; CMIS APIs for repository portability. citeturn31search5turn30search7turn21search7turn25search0  
**Audit log + provenance** — Nextcloud admin audit/log separation; Alfresco auditing + REST audit logs management; OWASP logging guidance; W3C PROV-DM provenance model. citeturn25search5turn25search6turn25search14turn34search3turn34search2  
**Rules engine** — DMN standard as portable decision model; Camunda DMN usage guidance; Kill Bill plugins for billing rules; Zammad triggers as rule-like automation. citeturn14search1turn14search2turn32search0turn26search0  
**Idempotency / outbox / retries / DLQ** — Microservices.io transactional outbox + idempotent consumer; Debezium outbox implementation; AWS SQS DLQ redrive; Stripe idempotency semantics. citeturn15search0turn15search12turn15search1turn15search2turn15search3  
**Observability instrumentation** — OpenTelemetry context propagation + semantic conventions; SRE monitoring discipline (but no-derivatives license limits reuse). citeturn35search0turn35search2turn36search18turn36search3

## E. Gap Analysis

The public ecosystem is missing a **coherent, reusable, product-level cookbook** that combines Level 1 archetype blueprints with Level 2 end-to-end recipes. The major gaps (and what a new community cookbook would uniquely provide) are:

### Missing: consistent “product shape” blueprints across archetypes
The closest public archetype blueprint work (e.g., CRM reference architecture) is *rare* and tends to be **one-off** or domain-specific. citeturn12view0turn12view2  
Open-source products (ERPNext/Odoo/Zammad/etc.) provide “what the product does,” but not a neutral “typical archetype skeleton” abstracted away from product-specific terminology and licensing constraints. citeturn22search0turn26search0

### Missing: a standard recipe format that merges UI + API + data + jobs + observability
Where end-to-end recipes exist, they are **capability-bound** and **stack-bound**:
- Workflow recipes are often tied to a specific workflow engine (Temporal/Camunda) citeturn14search6turn14search2  
- Integration recipes are tied to messaging/CDC stacks (Debezium/Kafka/SQS) citeturn15search1turn15search2  
- Admin UX recipes are tied to specific design systems/frameworks (Polaris, react-admin) citeturn16search0turn16search14

A new cookbook would unify these: “capability recipe card” that always includes **data model**, **API**, **UI**, **jobs**, **failure modes**, and **observability**—regardless of tech stack.

### Missing: failure-mode catalogs attached to product workflows
Some domains (billing) begin to show this (e.g., payment retries and dunning/overdue configuration guidance). citeturn32search7turn32search3  
But for most archetypes (CRM, DMS, ticketing), you rarely see organized failure-mode catalogs like:
- “merge field rendering errors + partial delivery”  
- “rules engine version drift”  
- “saved view permissions leakage”  
- “import pipeline poison records + DLQ semantics”

### Missing: licensing-friendly “community cookbook” inputs
Many of the best sources are **not adaptable** for a community cookbook:
- CC BY‑NC‑ND (no derivatives) blocks derivative cookbook content (Google SRE books). citeturn36search3  
- Design system licenses can be scope-limited (Atlassian ADS license grant). citeturn37search2turn37search10  
- Vendor docs are referenceable but not reusable verbatim. citeturn13search1turn15search3  
Conversely, Apache-2.0 / MIT ecosystems exist (TM Forum repos, OpenTelemetry, many OSS projects) but they don’t provide the unified two-level structure. citeturn21search0turn35search1turn37search0

## F. Recommendations

### Proposed taxonomy and navigation for a new community cookbook

A community cookbook should make the **two-level structure explicit**, with cross-linking:

**Navigation spine**
- **Archetypes (Level 1)**  
  Each archetype page includes:
  - “What it is / what it isn’t”
  - Typical modules & core workflows
  - A minimal canonical data model skeleton
  - Permission model patterns
  - Integration touchpoints
  - Shared embedded capabilities (links to Level 2 recipes)
- **Capabilities (Level 2)**  
  Each capability page includes:
  - Recipe card (problem/when/ingredients/flow/variants/failure modes/security/observability)
  - Reference implementations in 2–3 common stacks (optional)
  - Testing checklist + operational runbook checklist
- **Cross-cutting concerns**
  - Identity & authorization model patterns (RBAC/ABAC, auditability, multi-tenant isolation)
  - Data lifecycle (retention, deletion, export, GDPR-style constraints)
  - Reliability patterns (idempotency, DLQ, backpressure)
  - Observability (trace correlation, audit provenance, redaction)
- **Blueprint gallery**
  - Visual “starter diagrams” (C4-ish) and domain flows per archetype
  - Sample OpenAPI/JSON schema fragments (where licensing permits)

This design borrows the “component + shared model” mindset from TM Forum’s ODA assets citeturn21search9turn20search1 and the “capability recipe” mindset from microservices patterns and workflow cookbooks. citeturn15search0turn14search6

### Top Level 1 archetypes to publish first

These align with your examples and also map to strong existing public references:

**CRM** (anchor blueprint from Cruz + OSS CRM flows). citeturn12view0turn22search0  
**CMS / Wiki / Knowledge Base** (Strapi + MediaWiki templating). citeturn24search0turn24search2  
**Document Management System** (CMIS + audit/versioning patterns). citeturn25search0turn24search7turn25search5  
**Case/Ticket system** (IBM case mgmt + Zammad/GLPI). citeturn13search6turn26search0turn26search17  
**Workflow/BPM system** (BPMN/DMN + Temporal). citeturn14search7turn14search1turn14search6  
**Payments/Billing** (Kill Bill + Stripe lifecycle). citeturn32search7turn32search10  
**Scheduling/Rostering** (Cal.com + Timefold scheduling model). citeturn27search10turn27search1  
**Inventory/Catalog** (TMF Product Catalog + Saleor/Medusa/ERPNext). citeturn21search7turn30search0turn30search7turn30search2  
**Analytics Platform** (Superset + Metabase permissions models). citeturn29search0turn29search9  
**Identity/Access (CIAM)** (OAuth/OIDC/SCIM + NIST + Keycloak). citeturn33search1turn33search5turn33search2turn33search3turn22search5

#### Mini “recipe-card” outlines for Level 1 archetypes

Below are **starter archetype cards**; each is intended to expand into a full blueprint page.

**CRM archetype**  
Problem: manage accounts/contacts/leads/opportunities and interactions across channels. citeturn12view0turn22search0  
When to use: sales/service orgs needing pipeline + customer history.  
Ingredients: account/contact graph; lead/opportunity pipeline; activity timeline; segmentation; reporting; integrations with calendar, docs/KB, contact center. citeturn12view0turn12view2  
Core flow: capture lead → qualify → convert to opportunity → quote → order (variant across implementations). citeturn22search0turn22search14  
Variants: B2B vs B2C; territory-based sales; public sector citizen case linkage (observed in CRM reference work). citeturn12view1turn12view2  
Failure modes: duplicate identities; pipeline stage drift; integration lag between CRM and downstream systems.  
Security/privacy: PII handling; fine-grained access on accounts/contacts.  
Observability: change history on key entities; correlation IDs across lead→order flows (OpenTelemetry). citeturn35search0

**CMS / Wiki / Knowledge Base archetype**  
Problem: create/publish/search content with governance and structured metadata. citeturn24search0turn24search2  
When to use: documentation/knowledge or headless publishing needs.  
Ingredients: content types/fields; templates; versioning; roles/permissions; publish workflow; API exposure. citeturn24search0turn24search16turn24search2  
Core flow: draft → review → publish → update supersedes prior versions.  
Variants: headless CMS (Strapi) vs wiki-style mutable pages (MediaWiki). citeturn24search0turn24search2  
Failure modes: broken template dependencies; orphaned content relations. citeturn24search14  
Security/privacy: content visibility tiers; safe templating (Liquid-style non-eval principles). citeturn18search1  
Observability: publish events + audit trail.

**Document Management System archetype**  
Problem: store/manage files with metadata, versioning, retention, and audit. citeturn24search7turn25search5turn25search0  
When to use: regulated document workflows or enterprise file repositories.  
Ingredients: file object model + metadata; check-in/out or versioning; retention rules; audit log; APIs/interoperability (CMIS). citeturn24search7turn24search15turn25search0turn25search5  
Core flow: upload → annotate metadata → share/approve → retain/delete per policy.  
Variants: CMIS-backed repository integrations; audit optional due to performance cost (Alfresco). citeturn25search6  
Failure modes: retention misconfiguration; audit log growth/rotation; metadata extractor errors. citeturn25search10turn25search1  
Security/privacy: access controls, secure link sharing.  
Observability: separate audit.log stream (Nextcloud) + searchable audit entries (Alfresco REST). citeturn25search5turn25search14

**Case/Ticket system archetype**  
Problem: intake → triage → work → resolve, with SLAs and automation. citeturn13search6turn26search17  
When to use: support/ITSM/case management operations.  
Ingredients: ticket/case entity; queueing/assignment; SLA clocks; status model; automation rules + schedulers; notifications. citeturn26search0turn26search16turn26search6turn26search1  
Core flow: create → classify → assign → work → resolve → close → survey.  
Variants: “adaptive case management” with external data services (IBM external data service REST). citeturn8view1turn13search6  
Failure modes: automation rule ordering bugs; escalations spamming; data-integrity across linked records. citeturn26search12  
Security/privacy: requester/agent separation; auditing.  
Observability: SLA breach events; automation firing logs.

**Workflow/BPM system archetype**  
Problem: define and run multi-step processes and approvals reliably. citeturn14search7turn14search6  
When to use: approvals, onboarding, provisioning, complex orchestration.  
Ingredients: process model (BPMN), decision model (DMN), tasks, timers, human input, audit trail. citeturn14search7turn14search1turn14search6  
Core flow: start → tasks (human/system) → decisions → completion/compensation.  
Variants: engine-managed state (Temporal) vs BPMN engine (Camunda external task pattern). citeturn14search14turn14search9  
Failure modes: stuck workflows due to missing signals; retries causing duplicates.  
Security/privacy: least privilege on task actions.  
Observability: correlate workflow execution across services (context propagation). citeturn35search0

**Payments/Billing archetype**  
Problem: subscriptions/invoices/collections with retries, dunning, entitlements. citeturn32search7turn32search10  
When to use: SaaS billing, usage billing, invoicing.  
Ingredients: customer/account; subscription; invoice/invoice items; payment methods; payment attempts; retry schedule; overdue policy. citeturn32search7turn32search18turn32search14  
Core flow: bill cycle → invoice → attempt payment → retry/dunning → settle/void. citeturn32search3turn32search10  
Variants: manual invoicing vs automatic charge; partial payments (Kill Bill invoice payment model). citeturn32search8  
Failure modes: double charge (idempotency); webhook ordering issues; retry storms. citeturn15search3turn32search2  
Security/privacy: PCI boundaries; tokenization; auditability.  
Observability: payment attempt traces + invoice state transitions.

**Scheduling/Rostering archetype**  
Problem: manage availability, bookings, conflicts, reminders. citeturn27search10turn27search3  
When to use: appointment booking or workforce rostering.  
Ingredients: event types; availability rules; bookings; cancellations; recurrence; reminders; external calendar sync (iCalendar). citeturn27search10turn27search3  
Core flow: define availability → generate slots → book → confirm → notify → reschedule/cancel.  
Variants: consumer scheduling vs constrained rostering (Timefold shift scheduling dataset). citeturn27search1  
Failure modes: race for last slot; timezone bugs; duplicate booking creation.  
Security/privacy: invitee data minimization; link security.  
Observability: booking lifecycle events and correlation.

**Inventory/Catalog archetype**  
Problem: represent sellable items, variants, attributes, availability, movements. citeturn21search7turn30search3turn30search14  
When to use: commerce, ERP, asset management.  
Ingredients: product + variants + attributes; inventory tracking flag; movement ledger; locations; catalog publishing surface. citeturn30search3turn30search14turn30search11  
Core flow: define product → define variants → stock in/out → allocate/reserve → fulfill → reconcile.  
Variants: “inventory module used in flows” (Medusa). citeturn30search7  
Failure modes: oversell; negative inventory; movement reconciliation drift.  
Security/privacy: role separation for finance/stock adjustments.  
Observability: stock ledger/auditability.

**Analytics Platform archetype**  
Problem: enable exploration + dashboards with governance and permissions. citeturn29search2turn29search9  
When to use: internal analytics, metrics portals, embedded BI.  
Ingredients: datasets/semantic layer; permissions model; dashboard ownership; sharing; collections. citeturn29search0turn29search8turn29search1  
Core flow: connect data → define dataset → create charts → assemble dashboard → share/permission. citeturn29search8  
Variants: dataset-permission driven access (Superset) vs collection/data permissions split (Metabase). citeturn29search8turn29search1  
Failure modes: permission leakage; expensive queries causing outages.  
Security/privacy: row-level access; PII masking.  
Observability: query latency, dashboard load telemetry.

**Identity/Access (CIAM) archetype**  
Problem: authenticate, authorize, provision identities across domains. citeturn33search1turn33search5turn33search2turn33search3  
When to use: customer-facing auth, SSO, federation, SaaS provisioning.  
Ingredients: OAuth/OIDC flows; tokens/claims; SCIM provisioning endpoints; admin console and policies; assurance levels guidance (NIST). citeturn33search1turn33search5turn33search2turn33search3turn22search5  
Core flow: register → verify → authenticate → authorize → provision/deprovision.  
Variants: brokered identity providers (Keycloak). citeturn22search8turn22search5  
Failure modes: token replay; provisioning drift; inconsistent group memberships.  
Security/privacy: MFA, session security, data minimization.  
Observability: auth event logs + correlation across downstream provisioning.

### Top Level 2 capability recipes to publish first

These are both widely needed across archetypes and well-supported by public references:

Custom fields/extensible attributes citeturn34search13turn24search0  
Dynamic evaluation/survey engine citeturn17search13turn17search20  
Approval workflows / human in the loop citeturn14search6turn14search3  
Template/merge fields document generation citeturn18search12turn18search0turn18search5  
Notification preferences + routing citeturn19search0turn19search5turn19search2  
Search/filters/saved views citeturn16search0turn16search3turn16search14  
Import/export pipelines citeturn25search0turn31search5  
Audit log + provenance citeturn25search5turn25search14turn34search2turn34search3  
Rules engine / decisioning citeturn14search1turn14search2  
Idempotency + outbox + retries/DLQ citeturn15search0turn15search1turn15search2turn15search3

#### Mini “recipe-card” outlines for Level 2 capabilities

**Custom fields / extensible attributes**  
Problem: allow tenants/admins to add fields without redeploying schema.  
When to use: CRM/case mgmt/catalog/content types. citeturn24search0turn22search4  
Ingredients: field registry (name, type, validation, scope), storage strategy (JSON, EAV, typed extension tables), indexing strategy. (EAV guidance notes metadata complexity tradeoffs.) citeturn34search13turn34search1  
Core flow: define field → validate → store → query/filter → export.  
Variants: CMS-first modeled types (Strapi) citeturn24search0 vs classic CRM “studio” approach (SuiteCRM) citeturn23search1turn22search4.  
Failure modes: un-indexable fields causing slow list views; type changes corrupting data; EAV integrity gaps. citeturn34search13turn34search5  
Security/privacy: field-level permissions; PII tagging and export controls.  
Observability: field-level query latency; validation error rates.

**Dynamic evaluation / survey engine**  
Problem: build branching, versioned questionnaires with scoring and rules. citeturn17search13turn17search9  
When to use: onboarding, compliance checks, case intake, internal audits.  
Ingredients: form schema DSL (JSON or XLSForm), versioning strategy, response storage, computed values. citeturn17search13turn17search20turn17search1  
Core flow: publish form version → render → collect → validate → score → downstream workflow.  
Variants: JSON runtime (SurveyJS) citeturn17search13turn17search5 vs spreadsheet-authoring (XLSForm). citeturn17search20  
Failure modes: version mismatch; partial submissions; rule changes invalidating historical scoring.  
Security/privacy: sensitive answers encryption; access controls; audit of schema changes.  
Observability: completion funnel; validation error taxonomy.

**Approval workflows / orchestration**  
Problem: reliably coordinate human and system steps over long durations. citeturn14search6turn14search9  
When to use: invoice approvals, content publishing, access requests.  
Ingredients: durable state, task assignment/queues, reminders/timers, escalation rules; optional BPMN diagram. citeturn14search7turn14search6  
Core flow: request → route to approver → approve/deny → execute side effects → notify.  
Variants: workflow engine vs app-native state machine; decision tables (DMN) for routing. citeturn14search1  
Failure modes: duplicate approvals; stuck tasks after identity changes; replayed signals.  
Security/privacy: approver authorization checks; immutable audit trail.  
Observability: time-in-state metrics; orphaned-task alerts.

**Template/merge fields document generation**  
Problem: generate PDFs/DOCX/emails from templates and entity data. citeturn18search12turn18search0turn18search5  
When to use: invoices, letters, contracts, case documents.  
Ingredients: template language (Liquid/docx placeholders), merge-field catalog, rendering service, storage/delivery, template versioning. citeturn18search1turn18search0turn18search5  
Core flow: choose template → bind data → render → validate → store → deliver.  
Variants: guided interviews (docassemble) citeturn18search12; wiki templates (MediaWiki). citeturn24search2  
Failure modes: missing merge fields; injection risks; rendering timeouts; template dependency sprawl. citeturn18search1turn24search14  
Security/privacy: template sandboxing (non-eval) citeturn18search1; redaction rules.  
Observability: render latency; per-template error rates.

**Notification preferences + routing**  
Problem: send the right messages to the right channels while honoring opt-outs. citeturn19search0turn19search5  
When to use: all archetypes; especially ticketing, billing, workflow.  
Ingredients: preference model (category groups), suppression lists, routing rules, batching/coalescing (e.g., push collapse IDs), compliance (one-click unsubscribe). citeturn19search0turn19search2turn19search11  
Core flow: event → policy check → route → deliver → track → handle unsubscribe.  
Variants: category-based suppression groups (SendGrid) citeturn19search4; SMS opt-out keyword customization (Twilio). citeturn19search1turn19search21  
Failure modes: accidental unsubscribe triggers (RFC 8058 motivation) citeturn19search2; duplicate sends; deliverability throttling.  
Security/privacy: notification data minimization; channel verification.  
Observability: delivery success rates; unsubscribe SLAs.

**Search/filters/saved views**  
Problem: let users find and manage records at scale with persistent views. citeturn16search0turn16search14  
When to use: CRM, tickets, inventory, analytics.  
Ingredients: query model, filter DSL, saved-view storage, column config, permissions for shared views. citeturn16search0turn16search14turn16search12  
Core flow: filter/sort/search → save view → reuse/share → export.  
Variants: “index filters + saved views” UX (Polaris) citeturn16search0; technical persistence in URL/localStorage (react-admin). citeturn16search14turn16search7  
Failure modes: slow queries from unbounded filters; saved view drift after schema changes.  
Security/privacy: ensure saved filters don’t bypass row-level constraints.  
Observability: query latency by view; top slow filters.

**Import/export pipelines**  
Problem: safely ingest/export bulk data with validation, mapping, retries. citeturn25search0turn31search5  
When to use: CRM imports, catalog feeds, ticket migration, DMS batch ingest.  
Ingredients: staging tables/storage, schema mapping UI, validation rules, idempotent writes, DLQ for poison rows. (DLQ/Redrive guidance from SQS is a concrete exemplar.) citeturn15search2  
Core flow: upload → parse → validate → stage → apply → report errors → export.  
Variants: CMIS-based repository exchange citeturn25search0; commerce inventory flows with storage plugins (Medusa file service). citeturn31search5turn30search7  
Failure modes: partial imports; duplicate keys; schema mismatch.  
Security/privacy: scanning; least-privileged import roles.  
Observability: per-file success rate; DLQ depth and redrive success. citeturn15search14

**Audit log + provenance**  
Problem: provide tamper-evident history and accountability for actions/data. citeturn25search5turn34search3turn34search2  
When to use: DMS, CIAM, billing, case mgmt, admin actions.  
Ingredients: event schema, actor attribution, object references, diff capture strategy, retention, export API; optional provenance graph (PROV-DM). citeturn34search2  
Core flow: action occurs → write audit event → store/index → query/export → retain/rotate.  
Variants: separate audit.log stream (Nextcloud admin_audit) citeturn25search5; REST-managed audit logs (Alfresco). citeturn25search14  
Failure modes: high volume impacts performance; insufficient context to reconstruct actions; PII leakage in logs (OWASP logging guidance focus). citeturn34search3  
Security/privacy: immutable storage; redaction; access controls to audit views.  
Observability: audit backlog; “missing audit events” detectors.

**Rules engine / decisioning**  
Problem: externalize business logic for routing, validation, pricing, eligibility. citeturn14search1turn14search2  
When to use: approvals, billing, ticket routing, catalog eligibility.  
Ingredients: rule authoring UI, versioned rule sets, evaluation runtime, test harness, rollout strategy.  
Core flow: define rule → test → deploy version → evaluate with inputs → log decision.  
Variants: DMN decision tables for portability citeturn14search1; in-app if/then triggers in ticket systems. citeturn26search0  
Failure modes: rule version drift; unexpected precedence; performance regressions.  
Security/privacy: prevent rule authors from exfiltrating data; approvals for rule publish.  
Observability: decision trace logs; decision distribution monitoring.

**Idempotency + outbox + retries + DLQ**  
Problem: guarantee correct outcomes under retries, duplicates, and partial failures. citeturn15search0turn15search12turn15search3turn15search2  
When to use: integrations, billing charges, workflow steps, import pipelines.  
Ingredients: idempotency keys (API layer), consumer dedupe store, outbox table + relay, retry policy + DLQ/redrive. citeturn15search3turn15search0turn15search2  
Core flow: handle request with idempotency → write state + outbox in one transaction → relay publishes → consumer processes idempotently → failures go to DLQ. citeturn15search0turn15search1turn15search2  
Variants: CDC-based relay (Debezium outbox SMT) citeturn15search1; payment provider idempotency headers (Stripe). citeturn15search3turn15search11  
Failure modes: key reuse with different parameters (Stripe rejects mismatched params) citeturn15search3; relay “publish then crash” duplicate publish scenario citeturn15search0; DLQ misconfiguration causing premature dead-lettering. citeturn15search2  
Security/privacy: don’t leak idempotency keys; protect DLQ contents.  
Observability: DLQ depth, retry counts, duplicate-detection rates; trace propagation across async hops (OpenTelemetry context). citeturn35search0

## G. V1 Authoring Plan (Actionable)

This section operationalizes the recommendations into a publishable v1 plan with concrete templates, sequencing, and definition-of-done criteria.

### 1) V1 scope (what ships first)

**Publish in v1:**
- **10 Level 1 archetype pages** (from Section F)
- **10 Level 2 capability recipe pages** (from Section F)
- **4 cross-cutting foundations**:
  1. Identity & authorization patterns
  2. Data lifecycle (retention/deletion/export)
  3. Reliability patterns (idempotency/retries/DLQ)
  4. Observability baseline (traces/metrics/logs + audit provenance)

**Out of scope for v1 (defer to v1.1+):**
- Full reference implementations for every recipe in multiple stacks
- Deep domain variants beyond a “core + 1 variant” per archetype
- Generated docs site automation and diagram pipelines

---

### 2) Canonical page templates

#### 2.1 Level 1 archetype page template (required headings)

1. **What this archetype is / is not**
2. **Typical modules**
3. **Core workflows (top 3–5)**
4. **Canonical data model skeleton**
   - Core entities
   - Key relations
   - Invariants/constraints
5. **Permission model patterns**
6. **Integration touchpoints**
7. **Embedded capabilities** (links to Level 2 pages)
8. **Failure modes catalog (starter set: 8–12)**
9. **Observability baseline**
   - Key traces
   - Key metrics
   - Audit events
10. **Minimal architecture diagram (C4-ish, 1 page)**
11. **Implementation notes and stack variants**
12. **Licensing & source attribution notes**

#### 2.2 Level 2 capability recipe template (required headings)

1. **Problem / when to use**
2. **Ingredients**
   - Data model components
   - API contracts
   - UI surfaces
   - Jobs/workers/async components
3. **Reference flow (happy path + async path)**
4. **Variants** (engine/framework/provider-agnostic where possible)
5. **Failure modes & mitigations**
6. **Security/privacy considerations**
7. **Observability requirements**
   - Trace spans
   - Metrics
   - Structured logs/audit events
8. **Testing checklist**
   - Unit
   - Integration
   - Failure injection/chaos-lite checks
9. **Operational runbook checklist**
10. **Adoption notes by archetype** (which L1 pages use this)
11. **Licensing & source attribution notes**

---

### 3) Priority publishing order (recommended)

#### Wave 1 (highest leverage)
- **L1 Archetypes:** CRM, Case/Ticket, Payments/Billing
- **L2 Capabilities:**
  - Idempotency + outbox + retries + DLQ
  - Search/filters/saved views
  - Approval workflows/human-in-the-loop
  - Audit log + provenance

**Why first:** broad applicability, strongest source backing, and highest risk-reduction impact.

#### Wave 2
- **L1 Archetypes:** DMS, Workflow/BPM, Inventory/Catalog
- **L2 Capabilities:**
  - Custom fields/extensible attributes
  - Notification preferences + routing
  - Import/export pipelines

#### Wave 3
- **L1 Archetypes:** CMS/Wiki/KB, Scheduling/Rostering, Analytics Platform, CIAM
- **L2 Capabilities:**
  - Dynamic evaluation/survey engine
  - Template/merge fields document generation
  - Rules engine/decisioning

---

### 4) Definition of done (DoD)

A page is “done” only if all checks pass:

**For every L1 archetype page:**
- Includes required 12-template sections
- Contains at least one canonical entity-relationship sketch (textual is acceptable in v1)
- Links to at least 5 relevant L2 capabilities
- Includes at least 8 failure modes with mitigation guidance
- Includes minimum observability signals (5 metrics, 5 key events, 3 trace journeys)

**For every L2 capability page:**
- Includes required 11-template sections
- Provides end-to-end flow spanning UI/API/data/async components
- Lists at least 6 concrete failure modes and mitigations
- Provides test checklist and runbook checklist
- References at least 3 archetypes where the recipe is embedded

---

### 5) Governance and contribution model

**Roles (minimum):**
- **Editor:** template compliance and terminology consistency
- **Domain lead:** archetype correctness
- **Reliability lead:** failure modes and runbook quality
- **Licensing reviewer:** reuse and attribution checks

**Contribution workflow:**
1. Open page draft from template
2. Fill mandatory sections
3. Run checklist (DoD gate)
4. Licensing/source review
5. Publish with version tag

**Versioning:**
- Use semantic content versions (e.g., `cookbook.0`, `v1.1`)
- Maintain a “breaking guidance changes” log for renamed sections or taxonomy shifts

---

### 6) Licensing-safe authoring guardrails

Given mixed licensing in source material:

- Prefer **original synthesis** and neutral terminology.
- Avoid verbatim reproduction from copyrighted/vendor docs.
- Use permissive sources (Apache-2.0/MIT/CC-BY where applicable) as reusable seeds.
- Add per-page **“Source & License Notes”** with:
  - Source type (standard/vendor/book/OSS)
  - Reuse mode (reference-only vs adaptable)
  - Attribution requirements

---

### 7) 6-week execution schedule (practical baseline)

**Week 1:** finalize templates + governance + wave-1 outlines  
**Week 2:** draft 3 wave-1 archetypes  
**Week 3:** draft 4 wave-1 capabilities  
**Week 4:** QA for failure modes/ops/licensing + cross-linking  
**Week 5:** wave-2 outline + first 3 pages  
**Week 6:** v1 stabilization pass + publish `v1.0`

---

### 8) Immediate next actions (this week)

1. Create 20 page stubs from the two templates (10 L1 + 10 L2).
2. Populate wave-1 pages first (3 L1 + 4 L2).
3. Add a global glossary (shared terms: “entity,” “workflow state,” “policy,” “runbook event”).
4. Add a single cross-link index table mapping each archetype to embedded capabilities.
5. Run first editorial QA pass using DoD checklists.

This produces a concrete, licensing-aware v1 that demonstrates the two-level cookbook structure quickly, while preserving room for deeper implementations in later versions.