# ⚙️ Make Integration Pipelines

> **4 Make pipelines** connecting Airtable to external systems — website publishing, Instagram sync, inbound lead capture, and analytics. Native Airtable automations handle internal workflows; Make handles everything that crosses system boundaries.

---

## 🔄 Pipelines

---

### 🌐 Automated Event Publishing
Marketing flips a toggle in Airtable → photo uploaded to Cloudinary, AI translation into EN + FR, `events.json` pushed to GitHub, Cloudflare deploys automatically. No developer involved.

`Airtable` → `Make` → `Cloudinary` + `AI` → `GitHub API` → `Cloudflare Pages`

[![Web Ops Hub — Events Board](../../assets/interfaces/web_ops_events_board.gif)](../../assets/interfaces/web_ops_events_board.gif)

*One toggle in the interface — the event appears on the website in 3 languages within seconds.*

[![Events Gallery — Live Website](../../assets/interfaces/events_gallery1.gif)](../../assets/interfaces/events_gallery1.gif)

→ [Full pipeline documentation & demo](./website-sync-README.md)

---

### 📸 Instagram Gallery Sync
Make runs on a schedule and fetches the latest posts from the studio's Instagram account. Media is uploaded to Cloudinary, AI generates website-ready titles in RU / EN / FR, records are created in Airtable. The marketing team reviews and publishes with one toggle.

`Instagram API` → `Make` → `Cloudinary` + `AI` → `Airtable` → `GitHub API` → `Cloudflare Pages`

[![Instagram Gallery Manager](../../assets/interfaces/web_ops_instagram_gallery.gif)](../../assets/interfaces/web_ops_instagram_gallery.gif)

*Review imported posts in Airtable — check media, edit AI titles, toggle to publish.*

[![Instagram Gallery — Live Website](../../assets/interfaces/instagram_gallery2.gif)](../../assets/interfaces/instagram_gallery2.gif)

→ [Full pipeline documentation & demo](./instagram-gallery-sync-README.md)

---

### 📋 Inbound Lead Capture
Website form submission → Cloudflare Function proxies to Make webhook → lead created in Airtable with full UTM attribution, linked to the source campaign, instant email alert sent to the team.

`Website Form` → `Cloudflare Function` → `Make Webhook` → `Airtable` + `Gmail`

[![Website Form Data Flow](../../assets/interfaces/11-website_form_workflow.drawio(3).png)](../../assets/interfaces/11-website_form_workflow.drawio(3).png)

→ [Full pipeline documentation & demo](./inbound-leads-README.md)

---

### 📊 ETL — Analytics Pipeline
Operational data from Airtable is extracted on a schedule, transformed, and loaded into Google Sheets — which feed 6 role-scoped Looker Studio dashboards automatically. Marketing ROI, lead funnel, client retention, session capacity, and revenue trends update without any manual export.

`Airtable` → `Make` → `Google Sheets` → `Looker Studio`

→ [Full pipeline documentation](./etl-README.md) · [Business Intelligence & Analytics](../../business-intelligence-analytics/business-intelligence-analytics-README.md)

---

*[← Back to Automations](../automations-README.md)* · *[← Back to main README](../../README.md)* · *[🖥️ Interfaces](../../interfaces/interfaces-README.md)*
