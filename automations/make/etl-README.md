# 🔄 Make Integration Pipelines

> **4 Make pipelines** connecting Airtable to external systems — website publishing, Instagram gallery sync, inbound lead capture, and analytics. Native Airtable automations handle internal operations; Make handles everything that crosses system boundaries.

[![Instagram Gallery Manager](../../assets/interfaces/web_ops_instagram_gallery.gif)](../../assets/interfaces/web_ops_instagram_gallery.gif)

*Review imported posts in Airtable — check media, edit AI titles, toggle to publish. → [Web Operations Hub](../../interfaces/web-ops-hub-README.md)*

[![Instagram Gallery — Live Website](../../assets/interfaces/instagram_gallery2.gif)](../../assets/interfaces/instagram_gallery2.gif)

*Posts appear in the website gallery with multilingual titles. → [Frontend](../../frontend/frontend-README.md)*

---

## 🔄 Pipelines

---

### 🌐 Automated Event Publishing

Publishing an event used to require a developer, manual codebase edits, and multilingual copy-paste. Now the marketing team flips one toggle in Airtable and the event is live on the website in 3 languages within seconds — no developer, no file transfers, no coordination required.

Technically: the toggle triggers a Make scenario that uploads the photo to Cloudinary, runs AI translation into EN + FR, pushes the updated `events.json` to GitHub via API, and Cloudflare Pages deploys automatically.

`Airtable` → `Make` → `Cloudinary` + `AI` → `GitHub API` → `Cloudflare Pages`

[![Web Ops Hub — Events Board](../../assets/interfaces/web_ops_events_board.gif)](../../assets/interfaces/web_ops_events_board.gif)

*One toggle in the Events Board — the pipeline fires automatically.*

[![Events Gallery — Live Website](../../assets/interfaces/events_gallery1.gif)](../../assets/interfaces/events_gallery1.gif)

*The event appears on the website in 3 languages within seconds.*

→ [Full pipeline documentation & demo](./website-sync-README.md) · [🌐 Web Operations Hub](../../interfaces/web-ops-hub-README.md) · [🖥️ Frontend](../../frontend/frontend-README.md)

---

### 📸 Instagram Gallery Sync

The website gallery stays current without any manual uploads or copy-pasting from Instagram. Make fetches new posts on a schedule, handles media hosting and multilingual titling automatically, and creates a draft record in Airtable. The marketing team reviews and publishes with one toggle.

Technically: Make calls the Instagram Graph API, downloads media to Cloudinary, runs AI to generate titles in RU / EN / FR, and creates a record in Airtable. From there the same publishing pipeline as events takes over — a toggle pushes the gallery JSON to GitHub and Cloudflare deploys.

`Instagram API` → `Make` → `Cloudinary` + `AI` → `Airtable` → `GitHub API` → `Cloudflare Pages`

[![Instagram Gallery Manager](../../assets/interfaces/web_ops_instagram_gallery.gif)](../../assets/interfaces/web_ops_instagram_gallery.gif)

*Review imported posts in Airtable — check media, edit AI titles, toggle to publish.*

[![Instagram Gallery — Live Website](../../assets/interfaces/instagram_gallery2.gif)](../../assets/interfaces/instagram_gallery2.gif)

*The post appears in the website gallery with multilingual titles.*

→ [Full pipeline documentation & demo](./instagram-gallery-sync-README.md) · [🌐 Web Operations Hub](../../interfaces/web-ops-hub-README.md) · [🖥️ Frontend](../../frontend/frontend-README.md)

---

### 📋 Inbound Lead Capture

Every lead submitted through the website lands in Airtable automatically — categorized by type, attributed to the exact campaign that drove it, and with an instant email alert to the team. No manual data entry, no missed leads, no lost attribution.

Technically: a Cloudflare Pages Function proxies the form payload to a Make webhook (keeping the endpoint hidden from the frontend). Make looks up the matching campaign by UTM parameter, validates required fields, then simultaneously creates the lead record in Airtable linked to the campaign and sends a formatted HTML email with lead details, attribution, and NEXT STEPS.

`Website Form` → `Cloudflare Function` → `Make Webhook` → `Airtable` + `Gmail`

[![Website Form Data Flow](../../assets/interfaces/11-website_form_workflow.drawio(3).png)](../../assets/interfaces/11-website_form_workflow.drawio(3).png)

*Full customer journey — from campaign link click to CRM record with UTM attribution.*

[![Email Notification — Inbound Lead Alert](../../assets/interfaces/email_crm.png)](../../assets/interfaces/email_crm.png)

*Instant HTML email alert to the team — lead details, campaign attribution, and NEXT STEPS.*

[![Campaign Attribution — Lead Linked to Source Campaign](../../assets/interfaces/acquisition_campaigne.png)](../../assets/interfaces/acquisition_campaigne.png)

*Lead linked to the source campaign directly in Airtable — conversion tracking without manual attribution.*

→ [Full pipeline documentation & demo](./inbound-leads-README.md) · [📣 Marketing Ops Hub](../../interfaces/marketing-ops-hub-README.md) · [💼 Sales Ops Hub](../../interfaces/sales-ops-hub-README.md) · [🖥️ Frontend](../../frontend/frontend-README.md)

---

### 📊 ETL — Analytics Pipeline

All operational data — campaigns, leads, sessions, clients — flows into 6 role-scoped Looker Studio dashboards automatically. Marketing ROI, lead funnel, client retention, session capacity, and revenue trends update without any manual export or calculation.

Technically: 4 Make scenarios run on a monthly schedule, each extracting a slice of Airtable, transforming it into analytics-ready structure, and loading it into a dedicated Google Sheets tab. Looker Studio connects to Sheets natively and refreshes all dashboards automatically. Any scenario can be triggered manually with one click when fresh data is needed outside the schedule.

`Airtable` → `Make` → `Google Sheets` → `Looker Studio`

[![Dashboards Overview](../../assets/analytics/dashboards.gif)](../../assets/analytics/dashboards.gif)

*6 dashboards across all operational layers — updated automatically on a monthly schedule.*

→ [Business Intelligence & Analytics](../../business-intelligence-analytics/business-intelligence-analytics-README.md) · [![Live Dashboard](https://img.shields.io/badge/Live_Dashboard-Looker_Studio-blue?style=for-the-badge&logo=googlelookerstudio)](https://datastudio.google.com/s/jH8JAT6_iVs)

---

*[← Back to Automations](../automations-README.md)* · *[← Back to main README](../../README.md)* · *[🖥️ Interfaces](../../interfaces/interfaces-README.md)* · *[🌐 Frontend](../../frontend/frontend-README.md)*
