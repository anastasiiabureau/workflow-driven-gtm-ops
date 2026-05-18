# 🗺️ Role-Based Operations Workspace

> **A centralized no-code operations platform** built on a single shared Airtable base — 5 role-specific interfaces, 14 native automations, and 3 Make integration pipelines connecting the studio to the outside world.
>
> **Roles covered:** HR Manager (contracts & staff) · Studio Admin (front desk & scheduling) · Sales Manager (CRM & leads) · Marketing Manager (campaigns, events & website) · Front Desk

[![Web Ops Hub — Events Board](../assets/interfaces/web_ops_events_board.gif)](../assets/interfaces/web_ops_events_board.gif)

*Website event management without code — one toggle publishes in 3 languages.*

[![Events Gallery — Live Website](../assets/interfaces/events_gallery1.gif)](../assets/interfaces/events_gallery1.gif)

*Events gallery on the live website.*

> Each team member works exclusively in their own scoped hub. No one touches the raw database. Airtable is the single source of truth: internal operations — HR, CRM, scheduling, and finance — run on native automations. Make connects the platform to external systems: inbound leads arrive with full UTM attribution, Instagram content syncs to the website, and events publish in three languages via AI translation. Operational data feeds into 6 role-scoped Looker Studio dashboards automatically.

**Contents:** [⚡ The Challenge](#challenge) · [🖥️ Interface Demos](#demos) · [💡 The Problem & Solution](#problem-solution) · [🏗️ How the Workspace Works](#workspace) · [⚡ Automation Coverage](#automation-overview) · [📚 Documentation Index](#docs)

---

<a id="challenge"></a>
## ⚡ The Challenge

Before this system existed, the studio had no shared operational workspace. Client registrations lived in Google Sheets or notebooks. Leads had no qualification process. Teacher schedules were managed manually. Contract renewals had no tracking. Publishing an event to the website required a developer. There was no visibility into campaign ROI, client retention, or revenue trends.

Every workflow depended on people remembering to coordinate — and most things fell through the gaps.

**The solution — built across four layers:**

| Layer | What it does |
|---|---|
| **14 native Airtable automations** | Internal operations: contract renewals, lead migration, session generation, transaction creation — triggered by real business events, never manual |
| **5 role-specific interfaces** | One scoped workspace per role — staff work exclusively through interfaces and never access the raw database |
| **3 Make integration pipelines** | External connections: inbound leads with UTM attribution, Instagram gallery sync, website event publishing in 3 languages |
| **6 Looker Studio dashboards** | Role-scoped analytics: marketing ROI, lead funnel, client retention, session capacity — updated automatically via ETL pipeline |

→ [Full project documentation & architecture overview](https://github.com/anastasiiabureau/workflow-driven-gtm-ops)

---

<a id="demos"></a>
## 🖥️ Interface Demos

---

### 🌐 Web Operations Hub

Website publishing workspace. The marketing team publishes events and curates the Instagram gallery with a single toggle — no developer, no code, no file transfers.

#### 📅 Events Manager

[![Web Ops Hub — Events Board](../assets/interfaces/web_ops_events_board.gif)](../assets/interfaces/web_ops_events_board.gif)

*Website event management without code — one toggle publishes in 3 languages.*

[![Events Gallery — Live Website](../assets/interfaces/events_gallery1.gif)](../assets/interfaces/events_gallery1.gif)

*Events gallery.*

#### 📸 Instagram Gallery Sync

Instagram gallery curation — review imported posts, assign a category, toggle to publish.

[![Web Ops Hub — Instagram Gallery Manager](../assets/interfaces/web_ops_instagram_gallery.gif)](../assets/interfaces/web_ops_instagram_gallery.gif)

*Interface: review and publish from Airtable.*

[![Instagram Gallery — Live Website](../assets/interfaces/instagram_gallery2.gif)](../assets/interfaces/instagram_gallery2.gif)

*Instagram gallery on the live website.*

→ [Web Operations Hub — full documentation](./web-ops-hub-README.md)
→ [Frontend](../frontend/frontend-README.md)

---

### 📣 Marketing Ops Hub

Campaign management workspace. Register campaigns, generate UTM-tracked links, manage the event lifecycle, and track partner relationships. Inbound leads are attributed to campaigns automatically.

[![Marketing Campaigns Manager](../assets/interfaces/Marketing_Ops_Manager.mp4)](../assets/interfaces/Marketing_Ops_Manager.mp4)

*Campaign lifecycle manager — track all campaigns from Concept to Completed, monitor lead attribution and conversion.*

[![Campaign Attribution — Leads Linked to Campaign](../assets/interfaces/acquisition_campaigne.png)](../assets/interfaces/acquisition_campaigne.png)

*Leads linked to a campaign — source attribution visible directly in the campaign record.*

→ [Marketing Ops Hub — full documentation](./marketing-ops-hub-README.md)

---

### 💼 Sales Ops Hub

CRM and lead qualification workspace. Kanban board for managing the full lead funnel, activity logging, and client portfolio health monitoring.

[![CRM Lead Management Board](../assets/interfaces/CRM_lead_management_board-ezgif.com-video-to-gif-converter.gif)](../assets/interfaces/CRM_lead_management_board-ezgif.com-video-to-gif-converter.gif)

*Lead qualification Kanban — MQL → SQL → Positive. Notes and follow-up dates logged automatically.*

[![Client Portfolio & Health Insights](../assets/interfaces/CRM_Clients_Protfolio.mp4)](../assets/interfaces/CRM_Clients_Protfolio.mp4)

*Client portfolio — VIP, Regular, At-Risk, Churned segments calculated automatically by formula fields.*

→ [Sales Ops Hub — full documentation](./sales-ops-hub-README.md)

---

### 🏢 Check-in & Operations Hub

Front desk and scheduling workspace. New client registration, subscription sales, class check-ins, and the monthly studio calendar — all in one place.

[![New Client Registration & Sale](../assets/interfaces/7.OPS_Hub_New_Client_Sale.png)](../assets/interfaces/7.OPS_Hub_New_Client_Sale.png)

*New client registration — client record and transaction created simultaneously on form submit.*

[![Monthly Studio Planner](../assets/interfaces/OPS_HUB_planner.mp4)](../assets/interfaces/OPS_HUB_planner.mp4)

*Monthly studio planner — shared with marketing for events; recurring sessions generate automatically.*

→ [Check-in & Operations Hub — full documentation](./checkin-operations-hub-README.md)

---

### 🧑‍💼 Studio HR Hub

HR and contracts workspace. Staff directory, CDD renewal pipeline, teacher–class assignment, onboarding, and absence tracking.

[![Staff Directory](../assets/interfaces/HR_Staff_Directory.mp4)](../assets/interfaces/HR_Staff_Directory.mp4)

*Staff directory — new hire records, teacher specialization management, approval status.*

[![Contract Renewal Management](../assets/interfaces/HR_Contract_Renewal%20.mp4)](../assets/interfaces/HR_Contract_Renewal%20.mp4)

*Contract renewal pipeline — HR writes a note, the state machine handles every stage transition.*

→ [Studio HR Hub — full documentation](./studio-hr-hub-README.md)

---

<a id="problem-solution"></a>
## 💡 The Problem & Solution

| Problem | Solution |
|---|---|
| **Client management & transactions.** Registrations and subscription sales logged in Google Sheets or written by hand. No unified client record — no purchase history, no class balance, no subscription status. | All client records live in one base. A front-desk admin fills one form → client record and transaction are created and linked automatically. |
| **Lead management & customer journey.** Leads from Instagram, events, and referrals landed in a flat spreadsheet with no qualification stages. Follow-ups depended on memory. When a lead converted, data had to be manually copied to a separate file. | A sales manager works a Kanban board. Every interaction is logged automatically. When a lead is marked Positive → the record migrates to the correct table with all data pre-filled. No manual copying. |
| **Scheduling & teacher coordination.** Class schedules managed manually. Recurring sessions re-entered every week. Finding a substitute meant phone calls and message threads. | Recurring sessions generate themselves. Teacher absences are logged in the system — absence tracker gives real-time coverage visibility to admin and HR. |
| **HR & contracts.** CDD renewal deadlines tracked in spreadsheets or not at all. Teacher-to-class assignments updated manually. | Contract renewals advance through a tracked pipeline automatically. Teacher assignments sync to class rosters the moment a specialization is updated. |
| **Website content.** Publishing an event required a developer, manual codebase edits, and multilingual copy-paste into JSON. | Marketing flips one toggle in Airtable. Photo upload, AI translation into 3 languages, GitHub push, Cloudflare deployment — all automatic. Live in seconds. |

---

<a id="workspace"></a>
## 🏗️ How the Workspace Works

The studio runs on one shared Airtable base. But **no team member accesses tables directly.**

Each role gets a dedicated interface: a purpose-built workspace that surfaces only the data and actions relevant to their job. This design solves three problems simultaneously:

> #### 🔒 Security & access control
> Table-level access is restricted. Interfaces act as the controlled access layer — a front-desk admin can register a client and process a sale without seeing HR pipeline data, contract terms, or the financial table structure.

> #### ⚙️ Workflow-driven, not data-driven
> Interfaces are organized around real business processes — not database views. A sales manager opens a Kanban board where leads are already staged. A marketing manager moves campaign cards through a lifecycle pipeline. An admin opens a daily check-in board showing only today's sessions.

> #### 🔗 Cross-team coordination without manual handoffs
> When one team takes action in their interface, the effects propagate to other tables and interfaces automatically — through native automations or Make pipelines. Teams stay in sync through the system, not through messages.

> **Note:** Not every workflow is automation-driven. Client lifecycle segmentation (VIP, Regular, At-Risk, Churned), subscription status, contract expiry countdowns, and session fill rates are computed in real time from formula fields — no automation required.

---

<a id="automation-overview"></a>
## ⚡ Automation Coverage

The platform runs on two layers of automation: **14 native Airtable automations** for internal operations, and **3 Make integration pipelines** that connect Airtable to external systems.

---

### 📁 Native Airtable Automations

14 automations across HR, CRM, operations, and finance — each triggered by a real business event, never manual.
→ [Full Airtable automation reference](../automations/airtable/airtable-README.md)

**HR & Staff Management — 6 automations**
Contract renewal state machine (4 automations) that advances CDD records through the renewal cycle automatically, and a teacher–class sync (2 automations) that keeps class rosters up to date on approval or specialization change.
→ [Full deep dive](../automations/airtable/hr-staff-management-README.md)

**CRM & Lead Management — 5 automations**
Lead migration router (4 automations) that creates a fully populated record in the correct destination table the moment a lead is marked Positive, and an activity log (1 automation) that archives every sales interaction automatically.
→ [Full deep dive](../automations/airtable/crm-lead-management-README.md)

**Operations & Scheduling — 2 automations**
Recurring session generator that creates next week's session on completion, and an event-to-calendar sync that adds marketing events to the studio timetable the moment a campaign goes live.
→ [Full deep dive](../automations/airtable/operations-scheduling-README.md)

**Finance & Transactions — 1 automation**
Form-triggered transaction sync that creates a linked transaction record the moment a new client registration form is submitted — a sale is never registered without a financial entry.
→ [Full deep dive](../automations/airtable/finance-transactions-README.md)

---

### 🔄 Make Integration Pipelines — 3 external workflows

3 pipelines connecting Airtable to the outside world — website publishing, lead capture, and Instagram sync.
→ [Full Make pipelines reference](../automations/make/make-README.md)

**Automated Event Publishing** — Marketing flips a toggle → photo uploaded to Cloudinary, AI translation into EN + FR, JSON pushed to GitHub, Cloudflare deploys. No developer involved.
→ [Full pipeline documentation](../automations/make/website-sync-README.md)

**Inbound Lead Capture** — Website form submission → Make webhook → lead created with full UTM attribution, linked to the source campaign, email alert sent to team.
→ [Full pipeline documentation](../automations/make/inbound-leads-README.md)

**Instagram Gallery Sync** — Make fetches posts from Instagram API on schedule, uploads media to Cloudinary, generates AI titles in 3 languages. Marketing publishes via one toggle.
→ [Full pipeline documentation](../automations/make/instagram-gallery-sync-README.md)

---

> 📊 All operational data — leads, sessions, transactions, campaigns — feeds automatically into **6 role-scoped Looker Studio dashboards**. → [Business Intelligence & Analytics](../business-intelligence-analytics/business-intelligence-analytics-README.md)

---

<a id="docs"></a>
## 📚 Documentation Index

| Interface | Domain | Key Workflows | Stakeholders | Governance | Sub-README |
|---|---|---|---|---|---|
| **🌐 Web Operations Hub** | Content | Event publishing · Instagram gallery curation · AI translation review | Marketing Manager | Marketing Manager owns. No developer access required. Toggle-based publish/unpublish. | [web-ops-hub-README.md](./web-ops-hub-README.md) · [Event Publishing](../automations/make/website-sync-README.md) · [Instagram Sync](../automations/make/instagram-gallery-sync-README.md) |
| **📣 Marketing Ops Hub** | Campaigns | Campaign lifecycle · UTM link generation · Partner management · Event coordination | Marketing Manager | Marketing Manager owns. Event publishing to calendar is automated on status change. | [marketing-ops-hub-README.md](./marketing-ops-hub-README.md) · [Operations & Scheduling](../automations/airtable/operations-scheduling-README.md) · [Inbound Leads](../automations/make/inbound-leads-README.md) |
| **💼 Sales Ops Hub** | CRM | Lead qualification funnel · Follow-up logging · Client portfolio health | Sales Manager, Admin | Sales Manager owns the acquisition funnel. Admin has equivalent access for walk-in leads. | [sales-ops-hub-README.md](./sales-ops-hub-README.md) · [CRM automation](../automations/airtable/crm-lead-management-README.md) |
| **🏢 Check-in & Operations Hub** | Front Desk & Scheduling | New client registration & sale · Class check-ins · Monthly studio calendar · Recurring sessions | Admin, Marketing Team (planner only) | Admin owns all front-desk and scheduling workflows. Marketing has view + edit access to events in the planner. | [checkin-operations-hub-README.md](./checkin-operations-hub-README.md) · [Finance automation](../automations/airtable/finance-transactions-README.md) · [Operations & Scheduling](../automations/airtable/operations-scheduling-README.md) |
| **🧑‍💼 Studio HR Hub** | People & Contracts | Contract renewal pipeline · Staff onboarding · Teacher–class sync · Absence tracking | HR Manager, Admin | HR Manager owns. Admin has read access to absence and scheduling views. | [studio-hr-hub-README.md](./studio-hr-hub-README.md) · [HR & Staff automation](../automations/airtable/hr-staff-management-README.md) |

---

*[← Back to main project README](https://github.com/anastasiiabureau/workflow-driven-gtm-ops)* · *[🏗️ Architecture](../architecture/hld.md)* · *[🗄️ Database Schema](../architecture/database.md)* · *[⚙️ Automations](../automations/automations-README.md)*
