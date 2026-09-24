# Influx Sales Navigator: Requirements

- **Status:** Draft v0.1, based on one customer interview
- **Date:** 2026-09-24
- **Product sources:** influxdata.com product, customer, partner and blog pages, reviewed 2026-09-24 (see §10)

---

## 1. Summary

Sales Navigator is an **internal tool for InfluxData sales staff**. It works as the sales script. During a live call or while writing to a prospect, the rep enters the customer's use cases and needs. The tool then recommends **one specific InfluxData product** (plus a data-collection layer where relevant). It backs that recommendation with a short rationale and **relevant customer stories** from influxdata.com.

### 1.1 What the customer asked for (interview notes)

| # | Statement | Where it's covered |
| --- | --- | --- |
| I-1 | Internal tool: "sales navigator" | §2, NFR-SEC-1 |
| I-2 | Sales runs it as the sales script | FR-SCRIPT |
| I-3 | Used during a sales call **or** in email communication | FR-MODE |
| I-4 | Rep enters the customer's use cases and needs | FR-INTAKE |
| I-5 | Drives a **very specific** product suggestion across InfluxDB (overview), Cloud Serverless, Cloud Dedicated, Telegraf Enterprise and Telegraf | FR-REC, §6 |
| I-6 | References customer stories from the Partners, Blog and Customers pages | FR-STORY, §7 |

Everything else in this document is **derived** from these six points and the source pages, and is labeled as such. Anything not settled in the interview is listed in §11 (Open Questions).

---

## 2. Users and Context

| Persona | Goal | When they use it |
| --- | --- | --- |
| **Account Executive (AE)** (primary) | Qualify the prospect, land on the right product, and move the deal forward | Live discovery and qualification calls |
| **Sales Development Rep (SDR)** | Run a consistent first conversation and hand off a qualified lead | First-touch calls and outbound email |
| **Sales Engineer (SE)** | Check the technical fit and refine the recommendation | Technical deep-dive calls |
| **Sales enablement / content owner** (admin) | Keep product rules and the story library accurate | Offline maintenance |

**Operating context (derived):** the rep is talking to a customer while using the tool. It must be fast, easy to scan, and must never make the rep stall. The prospect never sees the tool directly. Only the outputs the rep chooses to share (such as an email draft) reach the customer.

---

## 3. Scope

### 3.1 In scope (MVP)

- A guided discovery script that captures the customer's use case and needs
- A deterministic recommendation engine covering the products in §6
- Customer-story matching from a curated library (§7)
- Two working modes: **Live Call** and **Email**
- Session summary and export (copy to clipboard or Markdown) for CRM notes and follow-up
- An admin way to maintain product rules and the story library

### 3.2 Out of scope (MVP)

- Customer-facing or self-serve use
- Price quotes, discounting or order forms (the tool may *point to* pricing pages)
- Automatic sending of email (the tool drafts; the rep sends)
- Two-way CRM sync (see OQ-3)
- Competitive battlecards (see OQ-7)

---

## 4. Functional Requirements

Priority: **M** = Must (MVP), **S** = Should, **C** = Could.

### 4.1 Modes: FR-MODE

| ID | Requirement | Pri |
| --- | --- | --- |
| FR-MODE-1 | The tool offers a **Live Call** mode: one question at a time, with suggested talk tracks and a short read-aloud summary of the recommendation. | M |
| FR-MODE-2 | The tool offers an **Email** mode: the rep pastes or types what the prospect wrote. The tool shows which discovery answers are still missing and produces a draft reply containing the recommendation and linked customer stories. | M |
| FR-MODE-3 | The rep can switch modes in the middle of a session without losing answers already entered. | S |

### 4.2 Guided sales script: FR-SCRIPT

| ID | Requirement | Pri |
| --- | --- | --- |
| FR-SCRIPT-1 | The tool presents an ordered discovery script: **opener → use case → workload/scale → deployment and operations → security and compliance → data collection → timeline and budget → recommendation → next step**. | M |
| FR-SCRIPT-2 | Each step shows a suggested question the rep can say out loud, plus the structured answer fields behind it. | M |
| FR-SCRIPT-3 | The rep can skip any step. The recommendation still appears and marks which inputs were assumed or unknown. | M |
| FR-SCRIPT-4 | The script adapts. For example, it asks about fleet size and configuration management only after the customer says they collect data from many hosts or devices. | S |
| FR-SCRIPT-5 | Each step can show a "why we ask" note that ties the question to the product decision. This helps new reps learn. | C |

### 4.3 Customer intake: FR-INTAKE

The tool captures these inputs. Each one should be a structured field (pick-list, range or toggle) with an optional free-text note.

| ID | Input | Example values | Pri |
| --- | --- | --- | --- |
| FR-INTAKE-1 | **Primary use case** (from the Customers page use-case filters) | IoT and sensor monitoring, IIoT, DevOps monitoring, infrastructure/application monitoring, network monitoring, real-time analytics, APM, Kubernetes monitoring, ML/anomaly detection, stream processing, metrics as a service, data historian replacement | M |
| FR-INTAKE-2 | **Industry** (from the Customers page industry filters) | Technology, Energy, Manufacturing/Agriculture, Financial Services, Telecom, Healthcare, Aerospace/Space, Retail, Public Sector, Transportation, Gaming, Security, Education | M |
| FR-INTAKE-3 | **Deployment preference** | Fully managed cloud / self-managed (on-premises or own cloud) / edge / AWS-native / undecided | M |
| FR-INTAKE-4 | **Workload scale** | Write rate (points/sec), number of unique series (cardinality), expected growth, query latency needs | M |
| FR-INTAKE-5 | **Workload maturity** | Prototype/PoC, small production, scaling production, mission-critical | M |
| FR-INTAKE-6 | **Tenancy and isolation needs** | Shared infrastructure is fine / needs single-tenant | M |
| FR-INTAKE-7 | **Network and security needs** | Private connectivity (AWS PrivateLink / Azure Private Link), required certifications (SOC 2 Type II, ISO 27001, ISO 27018), encryption, data residency | M |
| FR-INTAKE-8 | **Availability needs** | High availability, multi-node, read replicas, uptime SLA | M |
| FR-INTAKE-9 | **Pricing model preference** | Consumption / pay-as-you-go vs. committed/annual | S |
| FR-INTAKE-10 | **Data collection** | Sources (hosts, containers/Kubernetes, MQTT, Modbus, OPC, Kafka, cloud services, etc.), current agent (if any), **number of agents/hosts**, number of distinct configurations | M |
| FR-INTAKE-11 | **Collection-fleet pain points** | Configuration drift, silent agent failures, no fleet visibility, needs RBAC across teams, needs SLA-backed support | M |
| FR-INTAKE-12 | **Incumbent / system being replaced** | e.g. OSIsoft PI or another legacy historian, Graphite, Zabbix, Nagios, New Relic, Prometheus, in-house tooling | S |
| FR-INTAKE-13 | **Ecosystem** | Grafana, Kafka, preferred cloud (AWS/Azure/GCP), data lake or warehouse, AI/ML pipelines | S |
| FR-INTAKE-14 | **Timeline, budget and decision process** | Free text plus a timeline pick-list | S |

### 4.4 Recommendation engine: FR-REC

| ID | Requirement | Pri |
| --- | --- | --- |
| FR-REC-1 | The tool produces **exactly one primary database recommendation**. It must not present a menu of options. | M |
| FR-REC-2 | The tool produces **a data-collection recommendation** (none, Telegraf OSS or Telegraf Enterprise) whenever the customer has collection needs. This is separate from the database recommendation. | M |
| FR-REC-3 | Each recommendation includes: product name, a 2–3 sentence rationale **quoting the customer's own inputs**, the product page link, and the top 2–3 deciding factors. | M |
| FR-REC-4 | The tool shows a **confidence level** (High / Medium / Low) and lists the missing inputs that would raise it. Each missing input comes with the question to ask next. | M |
| FR-REC-5 | The tool shows **why not the runner-up** in one line (for example, "Not Serverless: customer needs AWS PrivateLink"). This gives the rep an answer ready if the customer pushes back. | M |
| FR-REC-6 | The logic is deterministic and rules-based, following §6, and every rule that fired can be shown. The same inputs always give the same output. | M |
| FR-REC-7 | Rules live in configuration an admin can edit, not in hard-coded logic. Every rule change is versioned. | S |
| FR-REC-8 | The recommendation updates live as answers change during the call. | S |
| FR-REC-9 | Hard disqualifiers override softer preferences. For example, a need for private connectivity always rules out Serverless. | M |

### 4.5 Customer stories: FR-STORY

| ID | Requirement | Pri |
| --- | --- | --- |
| FR-STORY-1 | For each recommendation, the tool suggests **1–3 customer stories**. They are ranked by how well they match on product, then use case, then industry, then scale. | M |
| FR-STORY-2 | Each story card shows: company, industry, use case, product(s) used, one headline number (e.g. "1M points/sec", "$55M savings"), a one-line talk track, and a link to the source URL. | M |
| FR-STORY-3 | Stories come only from the approved sources: `influxdata.com/customers/`, `/partners/` and `/blog/` (the "Use Cases" category). | M |
| FR-STORY-4 | Every story in the library carries a **"last verified" date**. Stories not re-checked within a set window (e.g. 180 days) are flagged. | M |
| FR-STORY-5 | A story counts as evidence for a specific product only if the source page names that product. Otherwise its product field is "unspecified". | M |
| FR-STORY-6 | The rep can search and filter the story library by industry, use case, product and incumbent replaced. | S |
| FR-STORY-7 | The tool prefers stories that match the customer's incumbent (e.g. "replaced OSIsoft PI"). | C |

### 4.6 Outputs: FR-OUT

| ID | Requirement | Pri |
| --- | --- | --- |
| FR-OUT-1 | **Call summary**: captured inputs, the recommendation with rationale, the stories referenced and agreed next steps. It can be copied as plain text or Markdown for CRM notes. | M |
| FR-OUT-2 | **Follow-up email draft**: a personalized recap, the recommended product with a link, 1–2 story links and a proposed next step (trial, technical deep-dive, pricing conversation). The rep can edit it before copying. | M |
| FR-OUT-3 | The tool suggests a **next step** based on the product. For example: Serverless → sign up (free tier, then credit on upgrade); Dedicated → technical scoping call; Telegraf Enterprise → free tier (≤20 configs / ≤100 agents) or pilot. | S |
| FR-OUT-4 | Outputs never include internal-only notes, confidence scores or "why not" lines unless the rep explicitly includes them. | M |

### 4.7 Administration: FR-ADMIN

| ID | Requirement | Pri |
| --- | --- | --- |
| FR-ADMIN-1 | An admin can add, edit and retire products, rules and talk tracks. | M |
| FR-ADMIN-2 | An admin can add, edit, verify and retire customer stories, including tags and the source URL. | M |
| FR-ADMIN-3 | The tool can suggest new or changed stories by checking the three source pages. Nothing goes live until a person approves it. | C |
| FR-ADMIN-4 | The tool keeps a change log of rules and content (who changed what, and when). | S |

---

## 5. Non-Functional Requirements

| ID | Requirement | Pri |
| --- | --- | --- |
| NFR-SEC-1 | **Internal only.** Access requires company SSO. The tool is not reachable from the public internet without authentication. | M |
| NFR-SEC-2 | Prospect data entered in a session is treated as confidential. The tool stores the minimum needed, deletes it after a set retention period, and never sends it to third parties without approval. | M |
| NFR-SEC-3 | If any AI/LLM features are added (such as parsing a pasted email in FR-MODE-2), prospect text goes only to approved providers under a no-training agreement. Model output is shown as a draft for the rep to edit and is never sent automatically. | M |
| NFR-PERF-1 | Moving between script steps and refreshing the recommendation takes **≤300 ms** (p95). The tool must never slow down a live call. | M |
| NFR-UX-1 | Works on a laptop alongside a video-call window (usable at ~50% screen width). All key actions work from the keyboard. | M |
| NFR-UX-2 | A new rep can finish a full discovery-to-recommendation run in **under 10 minutes** of call time. | S |
| NFR-A11Y-1 | Meets WCAG 2.2 AA. | S |
| NFR-ACC-1 | Product claims shown to reps match the current influxdata.com wording. Each claim links to its source page. | M |
| NFR-MAINT-1 | Product rules and the story library live as data files or database records, separate from the application code. | M |
| NFR-AUDIT-1 | Each recommendation logs the rule-set version and inputs used (without prospect identifiers) so results can be reproduced and rules tuned. | S |

---

## 6. Product Catalog and Decision Rules

> Source: influxdata.com product pages reviewed 2026-09-24. **Sales enablement and product marketing must confirm these rules before launch** (OQ-1).

### 6.1 Catalog

| Product | Deployment | Best fit (per source pages) | Key facts reps may cite |
| --- | --- | --- | --- |
| **InfluxDB 3 Core** (OSS) | Self-managed, single node | Edge deployments, prototypes, smaller workloads | Open source (MIT/Apache 2) |
| **InfluxDB 3 Enterprise** | Self-managed, multi-node | Production that needs high availability | HA, multi-node, read replicas, long-range compaction; "millions of writes/second, billions of series, sub-10ms queries" |
| **InfluxDB Cloud Serverless** | Fully managed, multi-tenant | Smaller or variable workloads on shared infrastructure; cost-conscious buyers | Consumption pricing, free tier, $250 credit on upgrade, unlimited cardinality, SOC 2 Type II / ISO, AWS Marketplace |
| **InfluxDB Cloud Dedicated** | Fully managed, single-tenant | Growing, high-volume workloads that need isolation | Dedicated infrastructure, AWS PrivateLink / Azure Private Link, SOC 2 Type II, ISO 27001/27018, uptime SLA, 24/7 monitoring, dedicated CSM |
| **Amazon Timestream for InfluxDB** | AWS-native, fully managed | AWS-first organizations | Listed on the InfluxDB overview page; how sales handles it is **TBD** (OQ-2) |
| **Telegraf** (OSS) | Agent, self-run | Collecting metrics from infrastructure, apps and devices | 400+ plugins; single binary; MQTT, Kafka, Kubernetes, Docker, Prometheus, AWS/Azure/GCP, etc. |
| **Telegraf Enterprise** | Management layer for Telegraf fleets | Large agent fleets where drift, silent failures or lack of visibility put the business at risk | Central configuration, parameterized templates, bulk operations, agent health, visual config builder (170+ plugins), RBAC/API tokens, Gold-level support SLAs; free tier ≤20 configs / ≤100 agents; entry packages from $18,000/yr; GA June 2026 |

### 6.2 Database decision rules (evaluated in order; the first match wins)

| # | If… | Recommend | Why not the runner-up (example) |
| --- | --- | --- | --- |
| R1 | Customer wants **managed** AND needs any of: single-tenant isolation, private connectivity, a dedicated CSM, or a mission-critical / high-volume scaling workload | **Cloud Dedicated** | "Not Serverless: it's multi-tenant and has no private connectivity." |
| R2 | Customer wants **managed** AND the workload is small, variable or early-stage AND consumption pricing is fine AND there's no R1 trigger | **Cloud Serverless** | "Not Dedicated yet: you can start on Serverless and move up when scale or isolation needs appear." |
| R3 | Customer wants **self-managed** AND needs HA, multi-node, read replicas or production scale | **InfluxDB 3 Enterprise** | "Not Core: it's single-node with no HA." |
| R4 | Customer wants **self-managed** or **edge** AND is running a prototype, edge node or small workload | **InfluxDB 3 Core** | "Not Enterprise yet: upgrade when you need HA or multi-node." |
| R5 | Customer is **AWS-first** and wants to buy through AWS or run natively in AWS | **Per OQ-2**: Timestream for InfluxDB, or Serverless/Dedicated via AWS Marketplace | — |
| R6 | Deployment preference is unknown | Ask for it next; show the leading candidate at **Low** confidence | — |

### 6.3 Data-collection rules

| # | If… | Recommend |
| --- | --- | --- |
| C1 | Customer collects from infrastructure, containers, network gear or devices (MQTT, Modbus, OPC, Kafka, etc.) and has no agent standard | **Telegraf** (OSS) |
| C2 | Customer runs or plans a **large Telegraf fleet** (the source page cites 1,000+ agents) **or** reports config drift, silent failures, lack of fleet visibility, multi-team RBAC needs, or a need for SLA-backed agent support | **Telegraf Enterprise** |
| C3 | Fleet is ≤100 agents and ≤20 configs but the customer wants central management | **Telegraf Enterprise (free tier)**, with an upgrade path |
| C4 | Customer only writes from their own applications or existing pipelines | No collection recommendation; mention Telegraf as optional |

> Telegraf Enterprise can be sold **regardless of which database the customer uses** (per the source page). The tool must allow a Telegraf Enterprise recommendation even when the database recommendation is "not InfluxData" or unknown.

---

## 7. Customer Story Library

### 7.1 Story record (data model)

| Field | Required | Notes |
| --- | --- | --- |
| `id` | ✓ | slug |
| `company` | ✓ | |
| `industry` | ✓ | Uses the Customers page industry filters |
| `use_cases[]` | ✓ | Uses the Customers page use-case filters |
| `products[]` | ✓ | Only products the source names; otherwise `unspecified` (FR-STORY-5) |
| `incumbent_replaced` | | e.g. "OSIsoft PI" |
| `headline_metric` | | e.g. "1M points/sec" |
| `talk_track` | ✓ | One sentence the rep can say out loud |
| `source_url` | ✓ | Must be on influxdata.com `/customer/`, `/partners/` or `/blog/` |
| `source_type` | ✓ | `customer` / `partner` / `blog` |
| `last_verified` | ✓ | ISO date |

### 7.2 Seed stories (from source pages, 2026-09-24; **verify each before launch**)

| Company | Industry | Use case | Headline | Product (as stated) | Source |
| --- | --- | --- | --- | --- | --- |
| Eutelsat OneWeb | Aerospace/Space | Satellite telemetry | 15M unique series, 1M points/sec, 600+ LEO satellites | verify | `/customer/eutelsat` |
| LeoLabs | Aerospace/Space | Orbit tracking | 25,000+ objects in LEO (27,000+ per 2026 blog post) | verify | `/customer/leolabs`, `/blog/inside-leo-labs-influxdb` |
| Loft Orbital | Aerospace/Space | Satellite operations | Speed-to-space and reliability | InfluxDB + Telegraf | `/customer/loft-orbital` |
| Seadrill | Energy | Condition-based maintenance on offshore rigs | $55M in asset lifecycle cost savings | verify | `/customer/seadrill` |
| ju:niz Energy | Energy | Renewable energy storage (MQTT, Modbus) | "100× more data per second" | Cloud Dedicated | `/customer/juniz` |
| Capital One | Financial Services | Infrastructure observability | — | Cloud Dedicated (named on the Dedicated page) | `/customer/capital-one` |
| Aquicore | Commercial Real Estate | Building IoT | — | Cloud Serverless | `/customer/aquicore` |
| Humatics | Sensors/Robotics | Real-time sensor data | — | Core (verify) | `/customer/humatics` |
| Texas Instruments | Semiconductors | Manufacturing visibility | 1.5M data points/day | verify | `/customer/texas-instruments` |
| Vonage | Communications | Global SaaS monitoring | 99.999% availability | verify | `/customer/vonage` |
| Teréga | Gas storage and transport | Modern data historian | Replaced legacy historian | verify | `/customer/terega` |
| Ausgrid | Utilities | Electrical network monitoring | Replaced OSIsoft PI | verify | `/customer/ausgrid` |
| WideOpenWest (WOW!) | Telecom | DOCSIS device monitoring | Kafka + Grafana | verify | `/customer/wideopenwest` |
| Red Hat | Technology | Network monitoring | 14,000+ network interfaces | verify | `/customer/red-hat` |
| Olympus Controls | Industrial Automation | Predictive maintenance for robots | — | verify | `/customer/olympus-controls` |

The Customers page lists **~280 stories**. The MVP ships with a curated, verified subset, and the rest are loaded through FR-ADMIN-2 / FR-ADMIN-3.

---

## 8. Example Flow (Live Call)

1. **Opener**: the rep picks the prospect and the mode. The tool shows the opening talk track.
2. **Use case**: "We monitor battery storage sites over MQTT and Modbus." → IoT/sensor, Energy.
3. **Scale**: "About 200 sites, growing fast; millions of series expected."
4. **Deployment**: "We don't want to run databases." → Managed.
5. **Security**: "Our security team requires private connectivity into AWS." → the R1 trigger fires.
6. **Collection**: "Telegraf on each site gateway, about 200 agents, configs drifting." → C2 fires.
7. **Recommendation**: **InfluxDB Cloud Dedicated** + **Telegraf Enterprise**, confidence High. Why not Serverless: "multi-tenant and no PrivateLink."
8. **Stories**: ju:niz Energy (MQTT/Modbus, energy storage), Seadrill (energy, $55M savings).
9. **Next step**: technical scoping call. The tool generates the summary and the follow-up email draft.

---

## 9. Acceptance Criteria (MVP)

- [ ] A rep can finish the full script and get a single primary recommendation, with rationale, confidence, runner-up line and 1–3 linked stories.
- [ ] For each rule in §6.2 and §6.3, at least one test case produces the expected recommendation. A table of the golden test cases is kept under version control.
- [ ] Changing any single deciding input (e.g. toggling "needs PrivateLink") updates the recommendation and the "why not" line in ≤300 ms.
- [ ] Every story shown has a working influxdata.com source URL and a `last_verified` date within the allowed window.
- [ ] No story is shown as evidence for a product its source page doesn't name.
- [ ] The Email mode draft and the call summary can be copied and pasted into Gmail/Outlook and Salesforce with formatting intact.
- [ ] Unauthenticated users cannot reach the tool.
- [ ] Sales enablement has signed off on the rules and talk tracks.

---

## 10. Sources

Product:

- <https://www.influxdata.com/products/influxdb-overview/>
- <https://www.influxdata.com/products/influxdb-cloud/serverless/>
- <https://www.influxdata.com/products/influxdb-cloud/dedicated/>
- <https://www.influxdata.com/products/telegraf-enterprise/>
- <https://www.influxdata.com/time-series-platform/telegraf/>

Customer stories:

- <https://www.influxdata.com/customers/>
- <https://www.influxdata.com/partners/>
- <https://www.influxdata.com/blog/> ("Use Cases" category)

---

## 11. Open Questions

| # | Question | Why it matters |
| --- | --- | --- |
| OQ-1 | Who owns the decision rules and talk tracks (sales enablement? product marketing?), and who signs them off? | FR-REC-7, launch gate |
| OQ-2 | Should the tool recommend **Amazon Timestream for InfluxDB**, or send AWS-first buyers to Serverless/Dedicated through AWS Marketplace? Should **InfluxDB 3 Core/Enterprise** be recommended even though the interview listed only the overview page for them? Is **InfluxDB Clustered** in scope? | Rule R5 and the catalog's completeness |
| OQ-3 | CRM integration: Salesforce? Should the tool read account data or write call notes back? | Scope, auth, data handling |
| OQ-4 | Platform: a standalone web app, a Salesforce component, or a browser extension? | Architecture, SSO |
| OQ-5 | Are there numeric thresholds (write rate, series count, spend) that should move a customer from Serverless to Dedicated? | Makes R1/R2 more precise |
| OQ-6 | Should the tool show pricing figures (e.g. Telegraf Enterprise's $18k/yr entry price), or only link to pricing pages? | FR-OUT, deal desk policy |
| OQ-7 | Should competitive positioning (e.g. vs. Prometheus, TimescaleDB, legacy historians) be included? | Scope |
| OQ-8 | Is AI-assisted parsing of prospect emails wanted, and which LLM providers are approved? | FR-MODE-2, NFR-SEC-3 |
| OQ-9 | How long should session data be kept, and does it hold prospect PII? | NFR-SEC-2 |
| OQ-10 | Is "Sales Navigator" the final name? It clashes with LinkedIn Sales Navigator. | Naming |
