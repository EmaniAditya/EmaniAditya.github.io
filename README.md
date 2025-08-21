# EmaniAditya.github.io

A Hugo site using the hugo-bearblog theme. Content is in Markdown under `content/`, and a few small layout overrides live in `layouts/`.

## Prerequisites
- Install Hugo (extended): https://gohugo.io/installation/
  - Verify: `hugo version`

## Run locally
```bash
hugo server -D
# Visit http://localhost:1313
```
- `-D` shows draft content.

## Project structure
- `content/`
  - `_index.md` — homepage content
  - `posts/` — blog posts (each `*.md` with front matter)
  - `projects/` — project pages
- `layouts/`
  - `index.html` — custom homepage template
  - `_default/single.html` — blog post template (title/date/reading time/tags)
  - `partials/style.html` — site styles (light/dark + small tweaks)
  - `partials/footer.html` — footer with social links
  - `404.html` — not found page
- `static/`
  - Static assets served at site root (e.g., `static/img/profile-photo.jpg` → `/img/profile-photo.jpg`)
- `themes/hugo-bearblog/`
  - Theme files (do not edit directly; override in `layouts/` instead)
- `hugo.toml`
  - Site configuration
  - Menus (`[menu.main]`), social links (`[params.social]`), taxonomies, markdown behavior

## Content basics
- Front matter examples:
```toml
+++
title = "My Post"
date = 2025-08-21T00:00:00Z
draft = true
slug = "my-post"
tags = ["tag1", "tag2"]
+++
```
- Set `draft = false` to publish.
- Projects live under `content/projects/*.md` with optional `tagline`.

## Social links
Configure once in `hugo.toml`:
```toml
[params.social]
  email = "esaadityareddy@gmail.com"
  github = "https://github.com/EmaniAditya"
  linkedin = "https://linkedin.com/in/emaniaditya"
  x = "https://x.com/Emani_Aditya"
```

## Build
```bash
hugo
# output goes to public/ (ignored)
```

## Deploy (GitHub Pages)
- Default workflow triggers on merges to `main` via `.github/workflows/hugo-gh-pages.yml`.
- Working branch: `2-revamp-emaniadityagithubio` → open PR → merge → deploy.
- After first deploy, ensure repo Settings → Pages → Source = GitHub Actions.

## Housekeeping
- Generated/temporary files are ignored via `.gitignore`:
  - `public/`, `resources/`, `.hugo_build.lock`, `.hugo_cache/`
- Do not commit theme changes; override with files in `layouts/`.
- If you ever see `public/` or `resources/` in Git changes, ensure `.gitignore` is up to date.
