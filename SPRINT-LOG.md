# Sprint Log — RaceTales

---

## Sprint 1 — Foundation & Deployment Pipeline
**Status:** 🟡 In Progress  
**Goal:** racetales.com is live with the Grand Canyon adventure page deployed via GitHub → Cloudflare Pages

### Stories

| # | Story | Status |
|---|---|---|
| RT-001 | Create GitHub repo `racetales` with folder structure from README | ⬜ |
| RT-002 | Set up Cloudflare Pages project connected to GitHub repo | ⬜ |
| RT-003 | Point racetales.com DNS to Cloudflare (update Hostinger nameservers) | ⬜ |
| RT-004 | Configure racetales.com as custom domain in Cloudflare Pages | ⬜ |
| RT-005 | Export Grand Canyon HTML from Claude design, verify R2 URLs | ⬜ |
| RT-006 | Add Grand Canyon page to repo at `/adventures/grand-canyon-2026/index.html` | ⬜ |
| RT-007 | Build v1 home page (`index.html`) with Grand Canyon card | ⬜ |
| RT-008 | Commit and push → verify live on racetales.com | ⬜ |
| RT-009 | Verify mobile layout on both home and adventure pages | ⬜ |

### Definition of Done
- racetales.com loads the home page
- racetales.com/adventures/grand-canyon-2026/ loads the full adventure page
- Photos load from R2, video plays from Stream
- Mobile layout is correct
- Push to main auto-deploys in < 2 minutes

---

## Sprint 2 — Adventure Template & Second Adventure
**Status:** ⬜ Not Started  
**Goal:** Adventure template locked, Chamonix or San Juans adventure live

### Stories (Draft)

| # | Story | Status |
|---|---|---|
| RT-010 | Create `_templates/adventure-template.html` from GC page pattern | ⬜ |
| RT-011 | Document Claude design prompt template in AUTHORING-GUIDE | ⬜ |
| RT-012 | Select second adventure (Chamonix 2025 or San Juans 2025) | ⬜ |
| RT-013 | Organize and rename photos for second adventure | ⬜ |
| RT-014 | Upload photos to R2, video to Stream | ⬜ |
| RT-015 | Build second adventure page in Claude design | ⬜ |
| RT-016 | Export, add to repo, update home page, deploy | ⬜ |

---

## Sprint 3 — Home Page Polish
**Status:** ⬜ Not Started  
**Goal:** Home page is a compelling editorial grid with 2–3 adventures

### Stories (Draft)
- Home page design elevated (Claude design session for index.html)
- Adventure cards: photo, title, location, date, tagline
- Mobile-first responsive grid
- Favicon and Open Graph tags
- Site title / meta description

---

## Decisions Log

| Date | Decision | Rationale |
|---|---|---|
| 2026-05-02 | Hosting: Cloudflare Pages (not Vercel, not Hostinger) | Already in CF ecosystem (Stream + R2), auto-deploy from GitHub, free |
| 2026-05-02 | No framework, no build step | Claude design exports clean HTML; zero friction authoring model |
| 2026-05-02 | Photos in Cloudflare R2, not embedded | URL references keep HTML files small and photos cacheable at CDN edge |
| 2026-05-02 | DNS: Cloudflare (nameservers from Hostinger) | Domain stays at Hostinger registrar, DNS managed in CF for Pages integration |
| 2026-05-02 | Authoring tool: Claude design | Proven workflow from Grand Canyon MVP; visual, photo-driven, exports HTML |
