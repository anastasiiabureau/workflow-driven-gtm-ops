# 🏗️ Architecture & High-Level Design

> The studio runs on a single Airtable base — the source of truth for all data. Make connects Airtable to the outside world: syncing Instagram content to the website gallery, publishing events in 3 languages with one toggle, capturing inbound leads from the website form, and keeping 6 Looker Studio analytics dashboards up to date automatically. The website is hosted on **Cloudflare Pages** and deployed automatically on every content update. All media — event photos, gallery images — is stored and served from **Cloudinary**, a cloud CDN that handles optimized delivery and generates permanent URLs used across the website. The entire platform is managed by the team through role-scoped workspaces built on Airtable Interfaces — no one ever opens a raw table. Every workflow is designed to be user-friendly: the team works in purpose-built interfaces, the system handles everything behind the scenes.

[![Instagram Gallery Manager](../assets/interfaces/web_ops_instagram_gallery.gif)](../assets/interfaces/web_ops_instagram_gallery.gif)

*Marketing reviews imported Instagram posts in the Web Ops workspace — checks media, edits AI-generated titles, flips a toggle to publish. No file transfers, no developer. → [Web Operations Hub](../interfaces/web-ops-hub-README.md)*

[![Instagram Gallery — Live Website](../assets/interfaces/instagram_gallery2.gif)](../assets/interfaces/instagram_gallery2.gif)

*The post appears on the live website gallery with multilingual titles instantly. → [Frontend](../frontend/frontend-README.md)*

**Contents:** [🏗️ Architecture Overview](#architecture) · [🔵 Growth & Acquisition](#growth) · [⬛ Frontend Ops & CMS](#frontend-ops) · [⬛ Data & Insights](#data) · [🔴 Internal Back Office](#back-office) · [👥 Stakeholders & Interfaces](#stakeholders) · [🧱 Tech Stack](#tech-stack) · [🔬 Technical Deep Dive](#deep-dive)

---

<a id="architecture"></a>
## 🏗️ Architecture Overview

The platform is organized around four data flows — each covering a distinct functional layer of studio operations:

- **🔵 Growth & Acquisition** — how leads are generated, captured, and converted into clients — including the full customer journey from the moment a lead clicks a campaign link to entering the database and being routed to the right team member
- **⬛ Frontend Ops & CMS** — how website content is published and kept up to date without a developer
- **⬛ Data & Insights** — how operational data flows into analytics dashboards automatically
- **🔴 Internal Back Office** — how the team manages daily studio operations through role-scoped interfaces

The database behind all four flows is a single Airtable base with **11 tables** — covering HR and staff, CRM and lead management, client lifecycle, financial transactions, class scheduling, content and campaigns, and partner relations.

→ [**Database Schema & Data Model**](./database.md) — full table reference: each table's role, how tables link to each other, which automations fire against each table, and which interface surfaces what data.

### Studio Data Flow

*Click the diagram to open full size.*

[![High-Level Design](../assets/architecture/High-Level%20Design%282%29.png)](../assets/architecture/High-Level%20Design%282%29.png)

---

<a id="growth"></a>
## 🔵 Growth & Acquisition

**How leads are generated, captured, and converted — from first campaign click to paid client.**

Marketing creates a campaign in the Marketing Ops Hub, generates a UTM-tracked link, and publishes it on Instagram, in ads, or at events. When a visitor follows that link and submits the contact form, a **Make scenario fires instantly** — the UTM is matched to the source campaign, a lead record is created in Airtable already linked to that campaign, and the team receives an HTML email alert with lead details, attribution, and NEXT STEPS. → [Inbound Lead Capture — Make pipeline](../automations/make/inbound-leads-README.md)

[![Event Registration — Campaign Sync](../assets/interfaces/events_gallery_register.gif)](../assets/interfaces/events_gallery_register.gif)

*Lead visits the event page — the UTM-tracked link captures campaign attribution automatically.*

[![Email Notification](../assets/interfaces/email_crm.png)](../assets/interfaces/email_crm.png)

*Instant HTML email alert the team receives — lead details, source campaign, and NEXT STEPS.*

[![Campaign Attribution](../assets/interfaces/acquisition_campaigne.png)](../assets/interfaces/acquisition_campaigne.png)

*Lead attributed to the source campaign in Airtable — conversion tracking without manual input.*

The lead appears in the Sales Ops Hub where the admin screens for spam first, then routes by contact type — potential clients go to Sales for qualification, yoga teacher and staff candidates go to HR, partner inquiries stay with Marketing. From there, each team member works the lead according to their own process in their dedicated interface. → [Sales Ops Hub](../interfaces/sales-ops-hub-README.md) · [CRM & Lead Management](../automations/airtable/crm-lead-management-README.md)

→ [Marketing Ops Hub](../interfaces/marketing-ops-hub-README.md)

---

<a id="frontend-ops"></a>
## ⬛ Frontend Ops & CMS

**How the website stays current — events and gallery — without involving a developer.**

Content originates in two Airtable interfaces. The marketing team creates campaigns and events in the Marketing Ops Hub. The Web Operations Hub is the publishing workspace — a user-friendly board where content is reviewed and activated with a single toggle. No code, no file transfers, no external tools.

**Event publishing.** Marketing fills in the event details and flips the Publish toggle in the Events Board. Make picks it up: photo is uploaded to Cloudinary CDN, AI generates titles and descriptions in EN and FR, the updated `events.json` is pushed to GitHub via API, and Cloudflare Pages deploys automatically. The event is live in 3 languages within seconds.

[![Web Ops Hub — Events Board](../assets/interfaces/web_ops_events_board.gif)](../assets/interfaces/web_ops_events_board.gif)

*One toggle in the Events Board — photo uploaded, AI-translated into 3 languages, pushed to GitHub, Cloudflare deploys.*

[![Events Gallery — Live Website](../assets/interfaces/events_gallery1.gif)](../assets/interfaces/events_gallery1.gif)

*The event appears on the live website in 3 languages within seconds.*

→ [Event Publishing — Make pipeline](../automations/make/website-sync-README.md)

**Instagram gallery.** Make fetches posts from Instagram on a schedule, uploads media to Cloudinary — a cloud CDN that stores and serves all website images with optimized delivery, generating a permanent URL for each asset — and generates multilingual titles using AI. Draft records appear in Airtable. Marketing reviews in the Instagram Gallery Manager, edits if needed, and flips the toggle — `gallery.json` is pushed to GitHub and Cloudflare deploys.

→ [Instagram Gallery Sync — Make pipeline](../automations/make/instagram-gallery-sync-README.md)

→ [Web Operations Hub](../interfaces/web-ops-hub-README.md) · [Marketing Ops Hub](../interfaces/marketing-ops-hub-README.md) · [Frontend](../frontend/frontend-README.md)

---

<a id="data"></a>
## ⬛ Data & Insights

**How operational data becomes analytics — automatically, without manual exports.**

Airtable is the single source of truth. All data — campaigns, leads, sessions, clients, transactions — lives in one base. Once a month, 4 Make ETL scenarios extract data from the core tables, transform it into analytics-ready structure, and load it into Google Sheets. Looker Studio connects to Sheets natively and refreshes 6 role-scoped dashboards automatically. Every manager opens their dashboard and sees live data — no exports, no formulas in spreadsheets, no coordination needed.

[![Dashboards Overview](../assets/analytics/dashboards.gif)](../assets/analytics/dashboards.gif)

*6 dashboards across all operational layers — updated automatically on schedule.*

[![Live Dashboard](https://img.shields.io/badge/Live_Dashboard-Looker_Studio-blue?style=for-the-badge&logo=googlelookerstudio)](https://datastudio.google.com/s/jH8JAT6_iVs)

| Dashboard | What it shows |
|---|---|
| 📣 Campaign Performance | Which campaigns bring leads and which convert — ROI, MQL/SQL, conversion by channel |
| 🎉 Events & Attendance | Event fill rates, revenue vs budget, no-show rates |
| 🧘 Yoga Directions | Which class styles fill fastest, teacher attendance, room utilization |
| 💰 Sales & Scheduling Insights | Busiest days and time slots, top subscription plans |
| 🎯 Lead Funnel & Customer Value | Drop-off at each qualification stage, LTV by source, days to convert |
| 🔄 Customer Lifecycle & Retention | Segment distribution — VIP / Regular / At-Risk / Churned |

→ [ETL Analytics Pipeline — Make](../automations/make/etl-README.md) · [Business Intelligence & Analytics](../business-intelligence-analytics/business-intelligence-analytics-README.md)

---

<a id="back-office"></a>
## 🔴 Internal Back Office

**How the team manages daily studio operations — entirely through interfaces, never touching raw data.**

The Airtable base powers 5 role-scoped interfaces. Each workspace surfaces only the data and actions relevant to that role. When one team member takes an action, the effects propagate to other tables and interfaces automatically through native automations — teams stay in sync through the system, not through messages.

Operations covered: lead routing and CRM, client registration and subscription sales, class scheduling and attendance, yoga team absence tracking, contract renewals, teacher-to-class assignments, partner management, and event coordination.

### Roles & Interfaces

**🏢 Admin · [Check-in & Operations Hub](../interfaces/checkin-operations-hub-README.md)**
Screens inbound leads for spam and routes them to the right team member. Registers new clients, processes subscription sales, logs class attendance, and manages the studio calendar. Tracks yoga team absences and scheduling coverage.

**💼 Sales Manager · [Sales Ops Hub](../interfaces/sales-ops-hub-README.md)**
Qualifies leads through the Kanban funnel (MQL → SQL → Positive), manages client relationships, and monitors retention. Client segments — VIP, Regular, At-Risk, Churned — are calculated automatically by formula fields.

[![CRM Lead Management Board](../assets/interfaces/CRM_lead_management_board-ezgif.com-video-to-gif-converter.gif)](../assets/interfaces/CRM_lead_management_board-ezgif.com-video-to-gif-converter.gif)

*Lead qualification Kanban — MQL → SQL → Positive. Notes and follow-up dates logged automatically. One status change migrates the record to Clients.*

**🧑‍💼 HR Manager · [Studio HR Hub](../interfaces/studio-hr-hub-README.md)**
Owns the yoga team globally — contracts, onboarding, specialization assignments. Contract renewals advance through a tracked pipeline automatically. Teacher-to-class assignments sync the moment a specialization is updated.

[![Staff Directory](../assets/interfaces/hr_stuff_directory.gif)](../assets/interfaces/hr_stuff_directory.gif)

*Teacher specialization updated in the Studio HR Hub — the automation adds them to the class roster instantly.*

**📣 Marketing Manager · [Marketing Ops Hub](../interfaces/marketing-ops-hub-README.md)**
Manages all campaigns, UTM link generation, event lifecycle, and partner relationships. Partner-attributed leads and collaboration history are visible in one workspace.

→ [Airtable Automations](../automations/airtable/airtable-README.md) · [HR & Staff Management](../automations/airtable/hr-staff-management-README.md) · [CRM & Lead Management](../automations/airtable/crm-lead-management-README.md) · [Operations & Scheduling](../automations/airtable/operations-scheduling-README.md) · [Finance & Transactions](../automations/airtable/finance-transactions-README.md)

---

<a id="stakeholders"></a>
## 👥 Stakeholders & Interfaces

No team member accesses raw Airtable tables directly — every role works exclusively through their scoped interface.

| Interface | Stakeholder | Key Workflows | Governance |
|---|---|---|---|
| 🌐 Web Operations Hub | Marketing Manager | Event publishing · Instagram gallery curation · AI translation review | Marketing Manager owns. Toggle-based publish/unpublish only — no raw content or database access. |
| 📣 Marketing Ops Hub | Marketing Manager | Campaign lifecycle · UTM link generation · Partner management · Event coordination | Marketing Manager owns. Lead attribution is automatic — no manual data entry required. |
| 💼 Sales Ops Hub | Sales Manager, Admin | Lead qualification funnel · Follow-up logging · Client portfolio health | Sales Manager owns the acquisition funnel. Admin has equivalent access for walk-in and spam screening. |
| 🏢 Check-in & Operations Hub | Admin, Marketing (planner) | New client registration · Class check-ins · Monthly studio calendar · Recurring sessions | Admin owns all front-desk and scheduling workflows. Marketing has view + edit access to events in the planner only. |
| 🧑‍💼 Studio HR Hub | HR Manager, Admin | Contract renewal pipeline · Staff onboarding · Teacher–class sync · Absence tracking | HR Manager owns. Admin has read access to absence and scheduling views only. |

→ [Full interface breakdown — pages, stakeholders & demos](../interfaces/interfaces-README.md)

---

<a id="tech-stack"></a>
## 🧱 Tech Stack

| Layer | Tool | Role |
|---|---|---|
| **Database & Automations** | Airtable | Single source of truth — 11 tables, 14 native automations, 5 role-scoped interfaces |
| **Integration & ETL** | Make | 4 pipelines — event publishing, Instagram sync, lead capture, analytics ETL |
| **Media CDN** | Cloudinary | Image and video hosting for website events and gallery |
| **Website** | Cloudflare Pages | Static site hosting + serverless form proxy function |
| **Content Repo** | GitHub API | `events.json` and `gallery.json` pushed programmatically by Make |
| **AI Translation** | Make AI module | Multilingual title and description generation — RU / EN / FR |
| **Social** | Instagram Graph API | Scheduled post import for gallery sync |
| **Email** | Gmail | Instant HTML lead notification alerts to the team |
| **Analytics Warehouse** | Google Sheets | Structured intermediate storage — 4 tabs fed by Make ETL |
| **Dashboards** | Looker Studio | 6 role-scoped dashboards — auto-refreshed from Google Sheets |

---

<a id="deep-dive"></a>
## 🔬 Technical Deep Dive — Automation Layer

The entire platform is held together by automations. No workflow requires a team member to remember a follow-up step — the system advances the next action automatically when a business event occurs.

**Two automation layers work together:**

**⚡ 14 native Airtable automations** handle everything internal — triggered by field updates, form submissions, status changes, and date conditions:
- **HR & Staff (6)** — a 4-stage contract renewal state machine advances CDD records automatically; teacher approvals and specialization changes sync to class rosters instantly
- **CRM & Leads (5)** — a 4-automation lead migration router creates fully populated records in the correct destination table the moment a lead is marked Positive; a fifth automation archives every sales interaction
- **Operations (2)** — recurring sessions generate themselves on completion; marketing events appear in the studio calendar the moment a campaign goes live
- **Finance (1)** — every new client registration form triggers an automatic transaction record

**🔄 4 Make integration pipelines** handle everything external — connecting Airtable to the website, Instagram, email, and analytics:
- **Event Publishing** — toggle in Airtable → Cloudinary + AI + GitHub + Cloudflare Pages
- **Instagram Sync** — scheduled fetch from Instagram API → Cloudinary + AI → Airtable → website
- **Lead Capture** — website form → webhook → Airtable CRM + Gmail alert
- **ETL Analytics** — monthly extract from Airtable → Google Sheets → Looker Studio

→ [All automations — overview & demos](../automations/automations-README.md) · [Airtable Automations](../automations/airtable/airtable-README.md) · [Make Pipelines](../automations/make/etl-README.md)

---

*[← Back to main README](../README.md)* · *[🗄️ Database Schema](./database.md)* · *[⚙️ Automations](../automations/automations-README.md)* · *[🖥️ Interfaces](../interfaces/interfaces-README.md)* · *[📊 Business Intelligence & Analytics](../business-intelligence-analytics/business-intelligence-analytics-README.md)* · *[🌐 Frontend](../frontend/frontend-README.md)*
