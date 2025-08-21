# Revamp Plan: emaniaditya.github.io (Hugo + Blog)

Last updated: 2025-08-20
Owner: E S Aaditya Reddy (GitHub: EmaniAditya)

---

## 1) Current State (Audit)
- Hugo project present with theme `hugo-bearblog`.
  - Config `hugo.toml` currently set to Mano Sriram (wrong baseURL/title/author/GA).
  - Custom partials exist: `layouts/partials/nav.html`, `style.html`, `custom_body.html` (dark-mode toggle, custom CSS).
  - Blog content under `content/posts/` (appears copied; not your voice yet).
  - `static/` has `resume.pdf`, images, and favicon.
- Static portfolio variants:
  - Root `index.html` + `styles.css` (minimal portfolio page).
  - `legacy/` contains a richer static portfolio (`legacy/index.html`, `legacy/styles.css`, `legacy/profile-photo.jpg`).
- Build/hosting:
  - `netlify.toml` configured to build Hugo (publish `public/`).
  - `public/` folder committed (built output) — should not be versioned if using Netlify or GH Actions.

Risk: Mixed approaches (direct static in root vs Hugo) will confuse hosting and future maintenance. We should consolidate into Hugo.

---

## 2) Goals
- Single Hugo-powered site for: Home (portfolio), Blog, Projects, Contact, Resume.
- Preserve/port the look-and-feel you prefer from `legacy/` but keep Hugo’s simplicity.
- Clean configuration with your details, analytics removed (or replaced with your ID), fast CI deploy.

---

## 3) Decisions
- SSG: Keep Hugo + `hugo-bearblog` (lightweight, Markdown-first, easy to theme).
- Hosting: Choose one of the two (recommended: Netlify). Alternative: GitHub Pages via GH Actions.
- Portfolio: Implement as Hugo home page using custom layout that mirrors `legacy/` sections (Experience, Projects, Skills, Education, Contact).
- Blog: Keep `content/posts/` with proper front matter, tags, RSS, code highlighting.
- Repo hygiene: Remove committed `public/` and the conflicting root `index.html`/`styles.css` after migration.

---

## 4) Implementation Plan (Step-by-step)

### Phase A — Configure Hugo to your profile
1. Update `hugo.toml` (site identity & menus):
   - baseURL = "https://emaniaditya.github.io/" (or your Netlify subdomain / custom domain)
   - title = "E S Aaditya Reddy"
   - theme = "hugo-bearblog"
   - params:
     - description = "Software Developer | MERN | Node.js"
     - author = "E S Aaditya Reddy"
     - favicon = "favicon.svg"
     - hideMadeWithLine = true
   - menus:
     - home -> "/"
     - blog -> "/posts/"
     - projects -> "/projects/" (to be created)
     - resume -> "/resume.pdf"
   - remove or replace Google Analytics `services.googleAnalytics.id`.

2. Verify `archetypes/default.md` suits your posts (draft true by default is fine).

3. Branding in partials:
   - Keep `layouts/partials/style.html` and tweak colors/typography if needed.
   - `layouts/partials/nav.html` already supports menu + dark-mode button.
   - `layouts/partials/custom_body.html` handles theme toggle (kept).

Acceptance: `hugo server` shows menus and your title/author/description; no Mano references.

---

### Phase B — Migrate portfolio (Home) into Hugo
1. Create `content/_index.md` with your bio and links (replace Mano text). Use concise intro; detailed sections will be in custom home layout.
2. Create custom home layout based on `legacy/` content:
   - `layouts/index.html` (or `layouts/_default/baseof.html` + `layouts/index.html`) to render sections:
     - About (brief)
     - Experience (timeline)
     - Projects (grid/list)
     - Skills
     - Education
     - Contact (links)
   - Move assets (e.g., profile-photo) into `static/img/`.
   - Inline or share CSS via existing `style.html` variables (prefer not to add separate global CSS unless needed).

3. Projects:
   - Create `content/projects/_index.md` (list page) and one file per project under `content/projects/<slug>.md` with front matter (title, role, tech, links).
   - Add callouts/buttons linking to Live Demo and GitHub.

Acceptance: Home renders as a consolidated portfolio (legacy look adapted), projects list exists, and detail pages open.

---

### Phase C — Blog setup and content hygiene
1. Posts:
   - Review `content/posts/` and remove or rewrite copied posts. Keep 1–2 as drafts to use as structure references.
   - Create at least 3 original posts using `hugo new posts/<slug>.md`.
   - Ensure front matter includes: title, date, tags, draft flag, description (for meta/OG).

2. Listing + single templates:
   - Bear theme already lists posts; ensure `ul.blog-posts` styles fit your brand.
   - Optionally add reading time and tags on single post pages.

3. RSS & taxonomy:
   - Enable RSS (default in Hugo) and optionally categories/tags in `hugo.toml`.

4. Code highlighting:
   - Use Hugo’s built-in Chroma; configure light/dark friendly styles if needed.

Acceptance: `/posts/` lists your posts; individual pages have correct meta, code highlighting, and RSS feed works.

---

### Phase D — Content & assets
1. Resume: Confirm `static/resume.pdf` is current; link in menu works.
2. Favicon: Already `static/favicon.svg`.
3. Social links: Add to bio/footer.
4. 404 page: Add `layouts/404.html` (optional).

Acceptance: All core links work, images load from `static/`.

---

### Phase E — Deployment & cleanup
1. Choose hosting:
   - Netlify (recommended): Keep `netlify.toml` as-is.
   - GitHub Pages: Add GH Action to build Hugo on push, deploy `public/` to `gh-pages` or use `docs/`.

2. Repo hygiene:
   - Remove committed `public/` from version control and add to `.gitignore`.
   - Remove or archive `legacy/` after home is migrated (keep screenshot captures if needed in `/static/img/`).
   - Remove root `index.html` and `styles.css` to avoid confusion once Hugo home is live.

3. SEO/meta:
   - Add `robots.txt` and `sitemap.xml` (Hugo can generate sitemap by default).
   - Add basic Open Graph/Twitter meta in base layout for posts and pages.

Acceptance: Clean repo (no build artifacts), single deploy flow works (Netlify or GH Pages), production site shows Hugo build.

---

## 5) Config snippets (to apply later)

Example `hugo.toml` (to be adapted):
```toml
baseURL = "https://emaniaditya.github.io/"
languageCode = "en-us"
title = "E S Aaditya Reddy"
theme = "hugo-bearblog"

[[menu.main]]
  name = "home"
  url = "/"
  weight = 1

[[menu.main]]
  name = "blog"
  url = "/posts/"
  weight = 2

[[menu.main]]
  name = "projects"
  url = "/projects/"
  weight = 3

[[menu.main]]
  name = "resume"
  url = "/resume.pdf"
  weight = 4

[params]
  description = "Software Developer | MERN | Node.js"
  author = "E S Aaditya Reddy"
  hideMadeWithLine = true
  favicon = "favicon.svg"

# Remove or set your own GA
#[services]
#  [services.googleAnalytics]
#    id = "G-XXXXXXX"
```

---

## 6) Execution checklist
- Update `hugo.toml` with your details.
- Create `layouts/index.html` to implement portfolio home.
- Create `content/projects/*` and update `content/_index.md`.
- Curate `content/posts/` to your writing; add 3 originals.
- Validate local with `hugo server`.
- Choose hosting and set up CI (Netlify or GH Actions).
- Remove `public/` from VCS, delete root `index.html`/`styles.css` post-migration, archive/remove `legacy/`.

---

## 7) Timeline (suggested)
- Day 1: Config + home skeleton + projects list.
- Day 2: Migrate legacy styling, finalize home, create project pages.
- Day 3: Blog cleanup + 3 posts + deploy + repo cleanup.

---

## 8) Definition of Done
- Production site runs on a single deployment flow.
- Homepage shows your portfolio (no Mano references).
- Blog lives at `/posts/` with working RSS.
- Projects listed and linked; resume reachable; dark mode toggle works.
- Clean repo (no built `public/`, no conflicting static roots).

---

## 9) Optional enhancements
- Add search (Lunr/Tipue client-side) for posts.
- Add social previews (OG image generation) per post.
- Add "Now" page and a `/uses` page.
- Add contact form (Netlify Forms) if needed.

---

## 10) Notes
- Keep CSS centralized in `layouts/partials/style.html` to avoid drift.
- Prefer `static/` for assets. Avoid committing build artifacts.
- Use `draft: true` until content is ready.
