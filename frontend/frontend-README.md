# 🌐 Intelligent Yoga — Website

> Multilingual static website for Intelligent Yoga Paris — built with **Eleventy 3** and **Tailwind CSS 4**, deployed on **Cloudflare Pages**. Three languages (FR / RU / EN), live event gallery and Instagram feed managed entirely from the Airtable workspace — the same no-code platform that runs the studio's CRM, ERP, HR, and operations. Events publish to the site with one toggle, Instagram syncs automatically via Make, and every contact form submission lands in the CRM with full UTM attribution.

🌐 **Live site:** [intelligentyogaparis.com](https://intelligentyogaparis.com)

[![Intelligent Yoga Website](../assets/interfaces/website_page1.gif)](../assets/interfaces/website_page1.gif)

---

**Contents:** [🔗 Backend Connection](#backend-connection) · [🛠 Tech Stack](#tech-stack) · [📁 Project Structure](#project-structure) · [📄 Pages](#pages) · [🌍 i18n System](#i18n) · [🚀 Build & Deploy](#build-deploy) · [🎬 Live Demo](#demo)

---

<a id="backend-connection"></a>
## 🔗 How the Frontend Connects to the Backend

The website is a static frontend — no server, no database. Three Make pipelines connect it to Airtable in real time: events publish from the marketing team's workspace, contact form submissions feed the CRM with full campaign attribution, and the Instagram feed syncs automatically on schedule.

---

### 🎯 Events Gallery

Managed entirely from the **Web Ops Hub** interface in Airtable — no developer access required. The marketing team fills in the event details, uploads a photo, and flips the **Display on Website** toggle. Make picks it up, uploads the photo to Cloudinary, runs AI translation into 3 languages, pushes `events.json` to GitHub, and Cloudflare deploys automatically. The gallery updates live within seconds.

→ [Web Operations Hub interface](../interfaces/web-ops-hub-README.md) · [Automated Event Publishing pipeline](../automations/make/website-sync-README.md)

[![Events Gallery](../assets/interfaces/events_gallery1.gif)](../assets/interfaces/events_gallery1.gif)

---

### 📋 Contact Form → CRM

The contact form captures UTM parameters from the URL at page load and attaches them to the submission payload. On submit, a Cloudflare Pages Function proxies the request to a Make webhook (keeping the endpoint hidden from client-side code). Make matches the `utm_campaign` value to the source campaign in Airtable, creates a lead in `Inbound_Leads` linked to that campaign, and sends an HTML email alert to the team — all simultaneously.

→ [Inbound Lead Capture pipeline](../automations/make/inbound-leads-README.md)

[![Contact Form & Event Registration](../assets/interfaces/events_gallery_register.gif)](../assets/interfaces/events_gallery_register.gif)

---

### 📸 Instagram Gallery

Make runs on a schedule, fetches posts from the Instagram Business API, deduplicates by post ID, uploads media to Cloudinary, and creates records in Airtable. AI generates website-ready titles in 3 languages from the Instagram caption. The marketing team reviews and publishes each post via a single toggle in the Web Ops Hub — the gallery JSON updates and Cloudflare deploys.

→ [Instagram Gallery Sync pipeline](../automations/make/instagram-gallery-sync-README.md)

[![Instagram Feed Sync](../assets/interfaces/instagram_gallery1.gif)](../assets/interfaces/instagram_gallery1.gif)

The gallery renders on the website as a responsive grid with a fullscreen modal:

[![Instagram Gallery on Website](../assets/interfaces/instagram_gallery2.gif)](../assets/interfaces/instagram_gallery2.gif)

---

<a id="tech-stack"></a>
## 🛠 Tech Stack

| Layer | Tool |
|---|---|
| Static site generator | [Eleventy (11ty) v3](https://www.11ty.dev/) |
| CSS framework | [Tailwind CSS v4](https://tailwindcss.com/) |
| Hosting | [Cloudflare Pages](https://pages.cloudflare.com/) |
| Form proxy | Cloudflare Pages Function |
| Media CDN | [Cloudinary](https://cloudinary.com/) |
| Backend & CRM | [Airtable](https://airtable.com/) — CRM · ERP · HR · Ops |
| Automation | [Make](https://www.make.com/) |
| Languages | French · Russian · English |

---

<a id="project-structure"></a>
## 📁 Project Structure

```
intelligentyoga-updates/
├── _src/                        # Source files (all edits happen here)
│   ├── _includes/
│   │   ├── base.njk             # Master layout — wraps all pages, loads all scripts
│   │   ├── header.html          # Sticky nav, language switcher, mobile menu
│   │   └── footer.html          # Footer with social links
│   │
│   ├── img/
│   │   ├── content/             # Page images (banners, teachers, sections)
│   │   ├── gallery/             # Community gallery images + manifest.json
│   │   ├── flags/               # FR / RU / EN flag SVGs
│   │   ├── logo/                # Logo variants
│   │   └── social/              # Social icon SVGs
│   │
│   ├── js/
│   │   ├── language-selection.js      # i18n engine — reads i18n.json, applies data-i18n attrs
│   │   ├── gallery-modal.js           # Community photo gallery (inline slider + fullscreen modal)
│   │   ├── gallery-events.js          # Events gallery (3-card slider + modal, fetches events.json)
│   │   ├── bio-modal.js               # Teacher bio modal on About page
│   │   ├── header-buttons.js          # CTA buttons (membership / trial) — pre-fills form type
│   │   ├── mobile-menu.js             # Hamburger menu open/close
│   │   ├── dropdown-menu.js           # Desktop nav dropdown behaviour
│   │   ├── anchor-navigation.js       # Smooth scroll to anchor sections
│   │   ├── navigation-highlighting.js # Highlights active nav link on scroll
│   │   └── form-validation.js         # Contact form validation + UTM capture
│   │
│   ├── index.html               # Page: About
│   ├── contact.html             # Page: Join
│   ├── styles.css               # Tailwind source + custom CSS variables and components
│   ├── i18n.json                # All translatable strings (FR / RU / EN)
│   ├── events.json              # Events data — updated by Make automation
│   ├── gallery.json             # Community gallery image list
│   └── instagram-gallery.json   # Instagram feed data — updated by Make automation
│
├── _site/                       # Build output (auto-generated, do not edit)
├── .eleventy.js                 # Eleventy config (passthrough copy for assets)
├── package.json
└── README.md
```

---

<a id="pages"></a>
## 📄 Pages

### `/` — About

| # | Section ID | Description |
|---|---|---|
| 1 | `#intro` | Full-width photo banner with title (hidden on mobile) |
| 2 | `#community` | Community gallery — inline photo slider with fullscreen modal |
| 3 | `#philosophy` | About section — text block + photo |
| 4 | `#events` | Events gallery — 3-card slider fed from `events.json` |
| 5 | `#history-philosophy` | Studio history — text block + photo |
| 6 | `#teachers` | Teacher cards — click opens bio modal |

[![About Page](../assets/interfaces/website_page1.gif)](../assets/interfaces/website_page1.gif)

### `/contact/` — Join

| # | Section ID | Description |
|---|---|---|
| 1 | `#intro` | Full-width photo banner with title (hidden on mobile) |
| 2 | `#contacts` | Address, phone, social links |
| 3 | `#offers` | Membership options — text + photo |
| 4 | `#form` | Contact / registration form — UTM params captured, proxied to Make via Cloudflare Function |

[![Contact Page](../assets/interfaces/website_page2.gif)](../assets/interfaces/website_page2.gif)

---

<a id="i18n"></a>
## 🌍 i18n System

All text is managed via `data-i18n` attributes and `i18n.json`. No text is hardcoded in HTML.

```html
<h2 data-i18n="header.community"></h2>
```

```json
{
  "header.community": {
    "fr": "Notre communauté",
    "ru": "Наше сообщество",
    "en": "Our Community"
  }
}
```

`language-selection.js` reads the saved language from `localStorage`, applies translations on every page load, and fires a `languageChanged` event that the galleries listen to for re-rendering countdown labels and UI strings.

---

<a id="build-deploy"></a>
## 🚀 Build & Deploy

```bash
npm install          # Install dependencies
npm start            # Dev server (Tailwind watch + Eleventy serve)
npm run build        # Production build → _site/
```

**Cloudflare Pages settings:**
- Build command: `npm run build`
- Output directory: `_site`

Deployments trigger automatically on every push to `main`.

---

<a id="demo"></a>
## 🎬 Live Demo

<a href="https://intelligentyogaparis.com" target="_blank">
  <img src="../assets/frontend/preview.png" alt="Intelligent Yoga Website Preview">
</a>

> Click the preview to open the live site.

**Deep links:**
- [Events gallery](https://intelligentyogaparis.com/#events)
- [Community gallery](https://intelligentyogaparis.com/#community)
- [Contact form](https://intelligentyogaparis.com/contact/#form)

---

*[← Back to main README](../README.md)* · *[🏗️ Architecture](../architecture/hld.md)* · *[⚡ Event Publishing pipeline](../automations/make/website-sync-README.md)* · *[⚡ Inbound Leads pipeline](../automations/make/inbound-leads-README.md)* · *[⚡ Instagram Gallery Sync](../automations/make/instagram-gallery-sync-README.md)*
