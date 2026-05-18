# ⚙️ Airtable Automations — ERP / CRM / Ops

> **14 native Airtable automations** across HR, CRM, Operations, and Finance — paired with **5 role-specific interfaces** that centralize studio management and eliminate manual workflows. Each automation is triggered by a real business event: a contract expiring, a lead converting, a class completing.

> ⚠️ **Data Privacy Note:** All datasets are synthetically generated. Names, contact details, and financial figures are fictional and used for demonstration purposes only.

[![Staff Directory](../../assets/interfaces/hr_stuff_directory.gif)](../../assets/interfaces/hr_stuff_directory.gif)

*Teacher specialization updated in the Staff Directory — the automation adds them to the class schedule through the interface instantly.*

---

<a id="interface-map"></a>
## 🖥️ Interface Map

5 role-specific Airtable interfaces serve as the operational layer — no team member accesses raw tables directly. Each hub is scoped to a role and surfaces only the data and workflows relevant to that stakeholder.

| Interface | Purpose | Sub-README |
|---|---|---|
| **🧑‍💼 Studio HR Hub** | Hiring, contracts, onboarding, teacher–class assignment, absence tracking | [studio-hr-hub-README.md](../../interfaces/studio-hr-hub-README.md) |
| **🏢 Check-in & Operations Hub** | Front-desk registration, plan sales, class check-ins, monthly studio calendar | [checkin-operations-hub-README.md](../../interfaces/checkin-operations-hub-README.md) |
| **📣 Marketing Ops Hub** | Campaign lifecycle, UTM tracking, partner management, event coordination | [marketing-ops-hub-README.md](../../interfaces/marketing-ops-hub-README.md) |
| **💼 Sales Ops Hub** | Lead qualification funnel, client portfolio health, retention metrics | [sales-ops-hub-README.md](../../interfaces/sales-ops-hub-README.md) |
| **🌐 Web Operations Hub** | Website event publishing, Instagram gallery curation, AI-translated content | [web-ops-hub-README.md](../../interfaces/web-ops-hub-README.md) |

→ [Full interface breakdown — pages, stakeholders, automation links & demos](../../interfaces/interfaces-README.md)

---

<a id="automation-overview"></a>
## ⚡ Automation Overview

---

### 📁 HR & Staff Management — 6 automations

Contract renewals no longer fall through the gaps — a 4-automation state machine advances every CDD record through the full renewal cycle automatically, triggered by date conditions and field updates. Teacher–class assignment is just as seamless: the moment a teacher is approved or their specialization updated, the class roster syncs automatically.

| # | Automation | Trigger |
|---|---|---|
| 1 | [HR] Auto-start Renewal | `Contract(Renew)` updated |
| 2 | Done: Auto-mark Renewal as Done | `CDD_End_Date` updated + conditions met |
| 3 | Non-Renewal: Auto-Close | Record matches termination conditions |
| 4 | [HR] Renewal: Finalize & Reset | `CDD_Renewal Progress = Done` |
| 5 | Teacher Approval to Class Workflow | New teacher approved + Specialization filled |
| 6 | Update Teacher Sync Class | `Specialization` field updated |

[![Staff Directory](../../assets/interfaces/hr_stuff_directory.gif)](../../assets/interfaces/hr_stuff_directory.gif)

*Staff directory — new hire records, teacher specialization management, approval status.*

[![Contract Renewal Management](../../assets/interfaces/HR_Contract_Renewal-ezgif.com-video-to-gif-converter.gif)](../../assets/interfaces/HR_Contract_Renewal-ezgif.com-video-to-gif-converter.gif)

*Contract renewal pipeline — HR writes a note, the state machine handles every stage transition.*

→ [Full deep dive & demo](./hr-staff-management-README.md)

---

### 📁 CRM & Lead Management — 5 automations

Leads from Instagram, website, events, and referrals all land in one table. When a sales manager marks a lead as Positive, a 4-automation router instantly creates a fully populated record in the correct destination table — Client, Partner, or Staff — with all data pre-filled. No manual copying. A fifth automation archives every interaction note automatically, keeping the activity log current without any extra steps.

| # | Automation | Trigger |
|---|---|---|
| 7 | LEAD MIGRATION: Clients | `Qualify_Status = Positive` + `Contact_Type = Client` |
| 8 | LEAD MIGRATION: Partners | `Qualify_Status = Positive` + `Contact_Type = Partner` |
| 9 | LEAD MIGRATION: Stuff | `Qualify_Status = Positive` + `Contact_Type = Hiring_Stuff` |
| 10 | LEAD MIGRATION: Teachers | `Qualify_Status = Positive` + `Contact_Type = Hiring_Teacher` |
| 11 | Lead Management: Archive Notes | `Notes` + `Next_Step_Date` both filled |

[![CRM Lead Management Board](../../assets/interfaces/CRM_lead_management_board-ezgif.com-video-to-gif-converter.gif)](../../assets/interfaces/CRM_lead_management_board-ezgif.com-video-to-gif-converter.gif)

*Lead qualification Kanban — MQL → SQL → Positive. Notes and follow-up dates logged automatically.*

[![Client Portfolio & Health Insights](../../assets/interfaces/CRM_Clients_Protfolio-ezgif.com-video-to-gif-converter.gif)](../../assets/interfaces/CRM_Clients_Protfolio-ezgif.com-video-to-gif-converter.gif)

*Client portfolio — VIP, Regular, At-Risk, Churned segments calculated automatically by formula fields.*

→ [Full deep dive & demo](./crm-lead-management-README.md)

---

### 📁 Operations & Scheduling — 2 automations

Recurring classes generate themselves — when a session is completed with the Recurring toggle on, the next week's session appears immediately with all details carried over. Marketing events land in the studio calendar the moment a campaign goes live, so operations and marketing always see the same timetable without any manual coordination.

| # | Automation | Trigger |
|---|---|---|
| 12 | Recurring Sessions Generator | `Session_Status = Completed` + `Recurring = ✅` |
| 13 | Sync Event to Studio Calendar | Campaign `In Progress` + `Campaigne_Type = Event/Workshop` |

[![Monthly Studio Planner](../../assets/interfaces/studio_planner.gif)](../../assets/interfaces/studio_planner.gif)

*Monthly studio planner — admin marks a session Completed, the next week's session appears instantly.*

→ [Full deep dive & demo](./operations-scheduling-README.md)

---

### 📁 Finance & Transactions — 1 automation

A sale is never registered without a transaction. When an admin submits the New Client Registration form at the front desk, a transaction record is created and linked to the client and subscription plan simultaneously — before the admin even leaves the page.

| # | Automation | Trigger |
|---|---|---|
| 14 | SYNC TRANSACTIONS TO NEW CLIENT | Form `New Client Registration & Sale` submitted |

[![New Client Registration & Sale](../../assets/interfaces/7.OPS_Hub_New_Client_Sale.png)](../../assets/interfaces/7.OPS_Hub_New_Client_Sale.png)

*New client registration form — client record and transaction created simultaneously on submit.*

→ [Full deep dive & demo](./finance-transactions-README.md)

---

*[← Back to Automations](../automations-README.md)* · *[← Back to main README](../../README.md)* · *[🖥️ Interfaces](../../interfaces/interfaces-README.md)* · *[🗄️ Database Schema](../../architecture/database.md)*
