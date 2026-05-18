# ⚙️ Automations

> **18 automations across two layers** — a complete operational ecosystem built on a single Airtable base. 14 native automations keep internal operations running without manual intervention: HR contracts advance through renewal pipelines, leads migrate to the right table the moment they convert, recurring classes generate themselves, and every sale triggers a transaction record automatically. 4 Make pipelines connect the studio to the outside world: leads arrive from the website with full UTM attribution, Instagram content syncs to the website gallery, events publish in 3 languages with one toggle, and all operational data flows into 6 analytics dashboards automatically.
>
> **Roles covered:** HR Manager · Studio Admin · Sales Manager · Marketing Manager · Front Desk
>
> Every workflow runs through a dedicated role-scoped interface — no team member ever touches raw Airtable tables.

> ⚠️ **Data Privacy Note:** All datasets are synthetically generated. Names, contact details, and financial figures are fictional and used for demonstration purposes only.

[![Web Ops Hub — Events Board](../assets/interfaces/web_ops_events_board.gif)](../assets/interfaces/web_ops_events_board.gif)

*Marketing flips one toggle in the Web Ops workspace — photo uploaded, AI-translated into 3 languages, pushed to GitHub, Cloudflare deploys. No raw data, no developer, just a user-friendly workspace. → [Web Operations Hub](../interfaces/web-ops-hub-README.md)*

[![Events Gallery — Live Website](../assets/interfaces/events_gallery1.gif)](../assets/interfaces/events_gallery1.gif)

*The event appears on the live website within seconds. → [Frontend](../frontend/frontend-README.md)*

**Contents:** [💡 The Problem](#the-problem) · [🗂️ Two Layers](#two-layers) · [⚡ Airtable Automations](#airtable) · [🔄 Make Pipelines](#make) · [📚 Section Index](#index)

---

<a id="the-problem"></a>
## 💡 The Problem

Before this system, every workflow depended on people remembering to coordinate — and most things fell through the gaps.

HR tracked contract renewal deadlines in spreadsheets, or didn't track them at all — renewals were missed, termination deadlines forgotten. Updating teacher schedules meant calling or messaging the right person and hoping they updated the right file. When a lead came in through the website, someone had to read the email, open Airtable, and manually create a new record — and if that email was missed, the lead went cold with no record anywhere. Publishing an event to the website required a developer: manual codebase edits, multilingual copy-paste into JSON, a deployment. Recurring classes had to be re-entered every week. Sales conversion data required manual counting. Analytics required manual exports from multiple places into a spreadsheet.

Every missed step meant lost data, a delayed response, or a developer pulled into operational work that shouldn't require one.

---

<a id="two-layers"></a>
## 🗂️ Two Layers

The automation system runs on two distinct layers — each handling a different scope of work.

**[⚡ Airtable — internal operations.](./airtable/airtable-README.md)** Everything that stays inside the platform: HR pipelines, CRM workflows, scheduling logic, financial records. 14 automations trigger on real business events — a field update, a form submission, a status change — and advance the next step without anyone initiating it.

**[🔄 Make — the outside world.](./make/etl-README.md)** Everything that crosses system boundaries: website publishing, Instagram sync, inbound lead capture, and analytics data export. 4 pipelines connect Airtable to Cloudinary, the GitHub repo, Cloudflare Pages, Instagram Graph API, Gmail, Google Sheets, and Looker Studio.

Both layers are managed exclusively through **5 role-specific interfaces** — purpose-built workspaces scoped to each role. No team member accesses raw tables directly.

| Interface | Role | Workspace |
|---|---|---|
| 🧑‍💼 Studio HR Hub | HR Manager | Contracts, staff directory, teacher assignments, absence tracking |
| 🏢 Check-in & Operations Hub | Admin | Front desk, client registration, class check-ins, studio calendar |
| 📣 Marketing Ops Hub | Marketing Manager | Campaigns, UTM links, event lifecycle, partner management |
| 💼 Sales Ops Hub | Sales Manager | Lead qualification Kanban, CRM, client portfolio health |
| 🌐 Web Operations Hub | Marketing Manager | Website event publishing, Instagram gallery curation |

→ [Full interface breakdown — pages, stakeholders & demos](../interfaces/interfaces-README.md)

---

<a id="airtable"></a>
## ⚡ Native Airtable Automations — 14 automations

All internal operations — triggered by real business events, runs entirely inside Airtable. No one needs to remember to do a follow-up step: when one thing happens, the next thing fires automatically.

→ [Deep dive — all 14 automations with demos](./airtable/airtable-README.md) · [Interface overview](../interfaces/interfaces-README.md)

| Domain | Automations | What they automate | Interface |
|---|---|---|---|
| 🧑‍💼 HR & Staff | 6 | Contract renewal state machine · teacher–class assignment sync | [Studio HR Hub](../interfaces/studio-hr-hub-README.md) |
| 💼 CRM & Leads | 5 | Lead migration router (4 destination tables) · activity log | [Sales Ops Hub](../interfaces/sales-ops-hub-README.md) |
| 🏢 Operations | 2 | Recurring session generator · event-to-calendar sync | [Check-in & Operations Hub](../interfaces/checkin-operations-hub-README.md) · [Marketing Ops Hub](../interfaces/marketing-ops-hub-README.md) |
| 💰 Finance | 1 | New client transaction sync on form submit | [Check-in & Operations Hub](../interfaces/checkin-operations-hub-README.md) |

[![Staff Directory](../assets/interfaces/hr_stuff_directory.gif)](../assets/interfaces/hr_stuff_directory.gif)

*Teacher specialization updated in the Staff Directory — Studio HR Hub interface — the automation adds them to the class roster instantly.*

[![CRM Lead Management Board](../assets/interfaces/CRM_lead_management_board-ezgif.com-video-to-gif-converter.gif)](../assets/interfaces/CRM_lead_management_board-ezgif.com-video-to-gif-converter.gif)

*Lead marked Positive in the Sales Ops Hub — record migrated to the correct destination table automatically, all data pre-filled.*

→ [Deep dive — HR & Staff](./airtable/hr-staff-management-README.md) · [CRM & Leads](./airtable/crm-lead-management-README.md) · [Operations](./airtable/operations-scheduling-README.md) · [Finance](./airtable/finance-transactions-README.md)

---

<a id="make"></a>
## 🔄 Make Integration Pipelines — 4 pipelines

Everything that crosses system boundaries — connecting Airtable to the website, Instagram, email, and analytics. Triggered by a toggle, a schedule, or a form submission.

→ [Deep dive — all 4 pipelines with demos](./make/etl-README.md)

| Pipeline | What it does | Technical flow |
|---|---|---|
| [🌐 Automated Event Publishing](./make/website-sync-README.md) | Publishes events to the website in 3 languages with one toggle — no developer needed | Airtable → Cloudinary + AI → GitHub → Cloudflare Pages |
| [📸 Instagram Gallery Sync](./make/instagram-gallery-sync-README.md) | Syncs Instagram posts to the website gallery automatically — AI titles, media hosting, one-toggle publish | Instagram API → Cloudinary + AI → Airtable → website |
| [📋 Inbound Lead Capture](./make/inbound-leads-README.md) | Every website form submission lands in the CRM instantly, attributed to the source campaign | Website form → Make webhook → Airtable + Gmail |
| [📊 ETL Analytics Pipeline](./make/etl-README.md) | Keeps all 6 analytics dashboards up to date — no manual exports | Airtable → Google Sheets → Looker Studio |

[![Instagram Gallery Manager](../assets/interfaces/web_ops_instagram_gallery.gif)](../assets/interfaces/web_ops_instagram_gallery.gif)

*Imported Instagram posts reviewed in the Web Operations Hub — check media, edit AI titles, toggle to publish. → [Web Operations Hub](../interfaces/web-ops-hub-README.md)*

[![Instagram Gallery — Live Website](../assets/interfaces/instagram_gallery2.gif)](../assets/interfaces/instagram_gallery2.gif)

*Posts appear in the website gallery with multilingual titles. → [Frontend](../frontend/frontend-README.md)*

---

### 📊 Analytics — Automated Data Sync

All operational data — leads, sessions, clients, campaigns — flows into 6 role-scoped Looker Studio dashboards automatically on a monthly schedule. Marketing ROI, lead funnel, client retention, session capacity, and revenue trends update without any manual export.

[![Dashboards Overview](../assets/analytics/dashboards.gif)](../assets/analytics/dashboards.gif)

*6 dashboards across all operational layers — updated automatically.*

→ [Business Intelligence & Analytics](../business-intelligence-analytics/business-intelligence-analytics-README.md) · [![Live Dashboard](https://img.shields.io/badge/Live_Dashboard-Looker_Studio-blue?style=for-the-badge&logo=googlelookerstudio)](https://datastudio.google.com/s/jH8JAT6_iVs)

---

<a id="index"></a>
## 📚 Section Index

| Section | Covers | Sub-READMEs |
|---|---|---|
| [⚡ Airtable Automations](./airtable/airtable-README.md) | 14 native automations across HR, CRM, Operations, Finance | [HR & Staff](./airtable/hr-staff-management-README.md) · [CRM](./airtable/crm-lead-management-README.md) · [Operations](./airtable/operations-scheduling-README.md) · [Finance](./airtable/finance-transactions-README.md) |
| [🔄 Make Pipelines](./make/etl-README.md) | 4 external integration pipelines + ETL | [Event Publishing](./make/website-sync-README.md) · [Instagram Sync](./make/instagram-gallery-sync-README.md) · [Lead Capture](./make/inbound-leads-README.md) · [ETL Analytics](./make/etl-README.md) |

---

*[← Back to main README](../README.md)* · *[🖥️ Interfaces](../interfaces/interfaces-README.md)* · *[🌐 Frontend](../frontend/frontend-README.md)* · *[📊 Business Intelligence & Analytics](../business-intelligence-analytics/business-intelligence-analytics-README.md)* · *[🏗️ Architecture](../architecture/hld.md)*
