# Authoring Guide — RaceTales

The repeatable workflow for adding a new adventure from raw photos to live on racetales.com.

---

## End-to-End Workflow

```
CAPTURE → ORGANIZE → UPLOAD → DESIGN → EXPORT → DEPLOY
```

Total estimated time for a complete adventure: 3–6 hours depending on photo volume and story complexity.

---

## Step 1 — Capture & Cull (iPhone / Camera)

- Shoot photos and video during the adventure
- After the trip, open **macOS Photos**
- Create a new Album named after the adventure: e.g. `Grand Canyon 2026`
- Cull to your best shots — aim for 20–60 photos per adventure

---

## Step 2 — Organize & Rename (macOS Photos)

This is the critical step that ties photos to your story structure.

1. Decide your narrative chapters before renaming. Example chapters:
   - `Descent`, `BoxCanyon`, `RiverCamp`, `TontoTraverse`, `Ascent`, `Rim`
2. In the album, rename photos sequentially by chapter:
   ```
   Descent_1.jpg
   Descent_2.jpg
   Descent_3.jpg
   BoxCanyon_1.jpg
   BoxCanyon_2.jpg
   RiverCamp_1.jpg
   ...
   ```
3. Export photos from the album at full resolution to a local folder:
   `/Users/saulsicard/RaceTales/{adventure-slug}/photos/`

**Naming rules:**
- No spaces — use underscores
- Capitalize the chapter name, underscore, number
- Keep chapter names to one word where possible
- Numbers are zero-padded if over 9 photos in a chapter: `Descent_01.jpg`

---

## Step 3 — Upload to Cloudflare R2

1. Open [Cloudflare Dashboard](https://dash.cloudflare.com) → R2 → `racetales-photos` bucket
2. Create a folder for the adventure: `grand-canyon-2026/`
3. Upload all renamed photos into that folder
4. Note the public URL pattern for this adventure:
   ```
   https://pub-{your-hash}.r2.dev/grand-canyon-2026/Descent_1.jpg
   ```
5. Save this base URL — you'll reference it in Claude design

**For video:**
1. Go to Cloudflare Stream → Upload your master edit
2. Copy the **Video ID** from the Stream dashboard
3. Your embed URL: `https://iframe.cloudflarestream.com/{video-id}`

---

## Step 4 — Build the Adventure Page in Claude Design

Open [claude.ai/design](https://claude.ai/design) and start a new design session.

**Prompt template to use:**

```
I'm building an adventure page for racetales.com. 

Adventure: [Title]
Date: [Month Year]
Location: [Location]
Distance/Stats: [Key stats]
Tagline: [One sentence summary]

Photo base URL: https://pub-{hash}.r2.dev/{slug}/
Video embed URL: https://iframe.cloudflarestream.com/{video-id}

Chapter structure:
1. [Chapter name] — photos: [list filenames]
2. [Chapter name] — photos: [list filenames]
...

Story: [Paste your written narrative here, or write it section by section]

Build this as a cinematic, editorial adventure page. Long-form, photo-driven. 
Dark/moody aesthetic. Full-width hero image. Sections separated by large 
atmospheric photos. Use the photo filenames in the order listed for each chapter.
Reference the existing Grand Canyon page aesthetic as the design baseline.
```

**Design session tips:**
- Give Claude the full chapter list upfront so photo references flow in order
- Write your story draft before the session — paste it in sections
- Iterate on sections — ask Claude to adjust photo sizing, typography, spacing
- The video should go in the most dramatic section of the story
- Always preview on mobile before exporting

---

## Step 5 — Export HTML from Claude Design

1. In Claude design, use **Export** → **Download HTML**
2. Save the file as `index.html`
3. Move it to: `/racetales/adventures/{slug}/index.html`

**Before committing, verify:**
- [ ] All photo URLs use the R2 base URL (not placeholder or base64)
- [ ] Video embed uses the correct Stream video ID
- [ ] Page title tag matches the adventure title
- [ ] Meta description is filled in
- [ ] Open Graph image tag points to a hero photo URL

---

## Step 6 — Update the Home Page

Open `racetales/index.html` and add a new adventure card to the grid:

```html
<a href="/adventures/grand-canyon-2026/" class="adventure-card">
  <img src="https://pub-{hash}.r2.dev/grand-canyon-2026/Hero_1.jpg" alt="Grand Canyon 2026">
  <div class="card-info">
    <span class="card-location">Grand Canyon, Arizona</span>
    <h2 class="card-title">Rim to River, Through the Box, and Back</h2>
    <span class="card-date">April 2026</span>
    <p class="card-tagline">34 miles. 11,000 feet. One day.</p>
  </div>
</a>
```

Add new adventures to the TOP of the grid (newest first).

---

## Step 7 — Commit and Deploy

```bash
cd racetales
git add .
git commit -m "Add {adventure-slug} adventure page"
git push origin main
```

Cloudflare Pages detects the push and deploys automatically. Live in ~60 seconds.

**Verify live:**
- `racetales.com` — home page shows new card
- `racetales.com/adventures/{slug}/` — adventure page loads
- Photos load from R2
- Video plays from Stream
- Mobile layout looks correct

---

## Adventure Checklist

Copy this for each new adventure:

```
[ ] Photos culled in macOS Photos
[ ] Photos renamed by chapter (Section_#.jpg)
[ ] Photos exported to local folder
[ ] Photos uploaded to R2 (folder: {slug}/)
[ ] Master video uploaded to Cloudflare Stream
[ ] R2 base URL saved
[ ] Stream video ID saved
[ ] Story draft written
[ ] Claude design session complete
[ ] HTML exported as index.html
[ ] Placed in /adventures/{slug}/index.html
[ ] R2 URLs verified in HTML (not placeholders)
[ ] Stream video ID verified in HTML
[ ] Home page card added
[ ] Committed and pushed to main
[ ] Live URL verified on desktop
[ ] Live URL verified on mobile
```

---

## Slug Naming Convention

```
{location-kebab-case}-{year}

Examples:
  grand-canyon-2026
  chamonix-2025
  san-juans-2025
  dolomites-2026
  loon-mountain-2026
```

---

## R2 Folder Structure

```
racetales-photos/ (R2 bucket)
├── grand-canyon-2026/
│   ├── Hero_1.jpg
│   ├── Descent_1.jpg
│   ├── Descent_2.jpg
│   └── ...
├── chamonix-2025/
│   ├── Hero_1.jpg
│   └── ...
└── san-juans-2025/
    └── ...
```
