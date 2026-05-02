# Architecture — RaceTales

## Core Philosophy

Static HTML. No framework. No build step. No CMS. Each adventure page is a self-contained HTML file authored visually in Claude design and dropped into the repo. The complexity ceiling stays low permanently so the site can scale to 50 adventures without maintenance burden.

---

## Deployment Pipeline

```
iPhone photos/video
      ↓
Rename in macOS Photos albums (e.g. Descent_1.jpg → Descent_5.jpg)
      ↓
Upload photos → Cloudflare R2 bucket
Upload video  → Cloudflare Stream
      ↓
Build adventure page in Claude design
(reference R2 photo URLs + Stream embed codes)
      ↓
Export HTML from Claude design
      ↓
Drop into /adventures/{slug}/index.html
      ↓
git add . → git commit → git push origin main
      ↓
Cloudflare Pages auto-detects push → deploys in ~60 seconds
      ↓
Live at racetales.com/{slug}
```

No CLI tools required. No build commands. No npm. Just push HTML.

---

## Cloudflare Setup

### Pages (Hosting)
- Project name: `racetales`
- Production branch: `main`
- Build command: *(none — static site)*
- Build output directory: `/` (root)
- Custom domain: `racetales.com`

### R2 (Photos)
- Bucket name: `racetales-photos`
- Public access: enabled (photos are public assets)
- URL pattern: `https://pub-{hash}.r2.dev/{adventure-slug}/{filename}`
- Folder structure per adventure: `grand-canyon-2026/`, `chamonix-2025/`, etc.

### Stream (Video)
- Each adventure master video uploaded directly to Stream dashboard
- Embed via iframe: `<iframe src="https://iframe.cloudflarestream.com/{video-id}" ...>`

### DNS
- Hostinger: nameservers pointed to Cloudflare (`ns1.cloudflare.com`, `ns2.cloudflare.com`)
- Cloudflare DNS: CNAME `racetales.com` → Cloudflare Pages project URL
- SSL: Cloudflare Universal SSL (auto, free)

---

## Page Architecture

### Home Page (index.html)
- Grid of adventure cards
- Each card: hero photo, title, location, date, short tagline, link to adventure
- Minimal JavaScript — no frameworks
- Mobile-first responsive layout

### Adventure Pages (/adventures/{slug}/index.html)
- Exported directly from Claude design
- Self-contained: all styles inline or in a `<style>` block
- Photos referenced as R2 URLs (not embedded base64)
- Video embedded via Cloudflare Stream iframe
- No external dependencies except Cloudflare media URLs

---

## Photo Naming Convention

Photos are organized by narrative section within each adventure. The naming convention ties directly to the story structure used in Claude design:

```
{Section}_{Number}.jpg

Examples:
  Descent_1.jpg
  Descent_2.jpg
  BoxCanyon_1.jpg
  Summit_3.jpg
  Camp_1.jpg
```

This naming is done in macOS Photos albums before upload to R2. The section names match the narrative chapters in the adventure page so Claude design can reference them sequentially.

---

## URL Structure

```
racetales.com/                           ← home / adventure index
racetales.com/adventures/grand-canyon-2026/   ← adventure page
racetales.com/adventures/chamonix-2025/
racetales.com/adventures/san-juans-2025/
```

Slug format: `{location-name}-{year}` (lowercase, hyphenated)

---

## What This Does NOT Use

| Skipped | Why |
|---|---|
| Next.js / React | Overkill for static HTML pages |
| Vercel | Cloudflare already covers everything |
| Netlify | Same |
| A headless CMS | Too much friction for this authoring model |
| A static site generator (Jekyll, Hugo) | Claude design IS the site generator |
| npm / node_modules | No build step needed |
| A database | No dynamic content |

---

## Scaling to 50 Adventures

The architecture handles 50 adventures trivially:
- Each is a folder with one HTML file
- The home page index is manually updated (or eventually scripted)
- R2 storage cost at 50 adventures (~500 photos): negligible
- Cloudflare Pages: free tier handles unlimited static sites

When the home page index becomes tedious to maintain manually (~20+ adventures), a simple JSON data file + vanilla JS render loop can replace the static card grid — no framework required.
