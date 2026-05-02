# RaceTales — Adventure Portfolio

**Live site:** [racetales.com](https://racetales.com)  
**Owner:** Saul Sicard  
**Stack:** Static HTML/CSS/JS → Cloudflare Pages → racetales.com  
**Media:** Photos in Cloudflare R2 · Videos via Cloudflare Stream  

---

## What This Is

A cinematic, editorial adventure portfolio. 30–50 total adventures. Each adventure is a standalone HTML page — a long-form visual narrative with photos, video, and written story. No framework, no CMS, no backend. Pure HTML files authored in Claude design, deployed via GitHub → Cloudflare Pages.

---

## Repository Structure

```
racetales/
├── README.md                        ← this file
├── index.html                       ← home page (adventure index/grid)
├── assets/
│   ├── css/
│   │   └── global.css               ← shared fonts, resets, variables
│   └── images/
│       └── og-default.jpg           ← default Open Graph share image
├── adventures/
│   ├── grand-canyon-2026/
│   │   └── index.html               ← adventure page (exported from Claude design)
│   ├── chamonix-2025/
│   │   └── index.html
│   └── san-juans-2025/
│       └── index.html
├── _templates/
│   └── adventure-template.html      ← starter shell for new adventures
├── docs/
│   ├── ARCHITECTURE.md              ← technical decisions & stack rationale
│   ├── AUTHORING-GUIDE.md           ← repeatable workflow for every new adventure
│   └── SPRINT-LOG.md                ← work history & decisions
└── .github/
    └── (Cloudflare Pages auto-deploys from main — no workflow file needed)
```

---

## Tech Stack

| Layer | Tool | Why |
|---|---|---|
| Page authoring | Claude design | Visual, photo-driven, exports clean HTML |
| Version control | GitHub | Source of truth, enables auto-deploy |
| Hosting & CDN | Cloudflare Pages | Free, fast, auto-deploys from GitHub |
| DNS | Cloudflare (via racetales.com) | Same ecosystem, simple routing |
| Video | Cloudflare Stream | Already in use, performant embeds |
| Photos | Cloudflare R2 | Object storage, referenced as URLs in HTML |
| Domain registrar | Hostinger | Domain only — DNS managed in Cloudflare |

---

## Adventures

| Slug | Title | Status |
|---|---|---|
| `grand-canyon-2026` | Rim to River, Through the Box, and Back | 🟡 In Progress |
| `chamonix-2025` | France / Switzerland — 90km du Mont-Blanc | ⬜ Not Started |
| `san-juans-2025` | Colorado San Juan Mountains | ⬜ Not Started |

---

## Quick Links

- [Authoring Guide](docs/AUTHORING-GUIDE.md) — how to add a new adventure
- [Architecture](docs/ARCHITECTURE.md) — technical decisions
- [Sprint Log](docs/SPRINT-LOG.md) — work history
