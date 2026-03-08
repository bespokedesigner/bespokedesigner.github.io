# CLAUDE.md — Website Project Reference

## Project Overview

Personal creative portfolio for Annette McHattie at https://annette.mchattie.net. Built with Hugo + Tailwind CSS, deployed to GitHub Pages. Showcases piano practice (music blog) and novel writing (Kell & Co project + general writing).

## Tech Stack

- **Hugo** 0.152.2 (extended), with Go modules
- **Theme:** Hugoplate (zeon-studio) — base at `themes/hugoplate/`, overridden in root `layouts/`
- **CSS:** Tailwind CSS 4.x, built via Node/npm
- **Formatting:** Prettier with `prettier-plugin-go-template` and `prettier-plugin-tailwindcss`
- **Deployment:** GitHub Actions (`.github/workflows/hugo.yaml`) → GitHub Pages
- **Contact form:** Formspree (`config/_default/params.toml`)
- **Node version:** 18 (see `.nvmrc`)

## Key Commands

```bash
./serve.sh               # Local dev (hugo server --renderToMemory)
npm run dev              # Same as above via npm
npm run build            # Production build (minified, GC)
npm run format           # Run Prettier over all files
```

## Content Structure

```
content/
├── _index.md                     # Home page (banner + features sections)
├── music/
│   ├── _index.md
│   └── blog/                     # Piano practice blog posts
│       └── 2025/<slug>/index.md
├── writing/
│   ├── _index.md
│   ├── blog/                     # Short stories / general writing posts
│   │   └── 2025/<slug>/index.md
│   └── kell-and-co/              # Kell & Co novel sub-pages
│       ├── _index.md
│       └── <character-profiles>/
├── pages/                        # Static pages (about, contact, privacy)
├── authors/                      # Author profile
└── sections/                     # Reusable sections (CTA, testimonials — currently disabled)
```

## Front Matter Conventions

**Standard fields** (all posts):
```yaml
title: ""
description: ""        # Used for social/meta
date: YYYY-MM-DD
image: "/images/..."
author: "Annette McHattie"
tags: []
draft: false
```

**Music posts** — add the custom taxonomy:
```yaml
pieces: ["Piece Name"]
```

**Pages** — optional extras:
```yaml
meta_title: ""         # SEO title (overrides title)
layout: "about"        # Custom layout name
toc: false             # Suppress table of contents
```

## Custom Taxonomies

| Taxonomy | Usage |
|---|---|
| `tags` | General post tags |
| `categories` | Post categories |
| `pieces` | Piano pieces (music section) |

Permalinks: `music/piano-pieces/:slug`

## Layout Overrides

Custom layouts in `/layouts/` override the theme. Key files:

- `layouts/music/blog/list.html` — Music blog index
- `layouts/music/blog/single.html` — Single music post
- `layouts/writing/list.html` — Writing section index
- `layouts/writing/blog/list.html` / `single.html` — Writing blog
- `layouts/pages/about.html` / `contact.html` — Static pages
- `layouts/partials/components/blog-card.html` — Reusable post card
- `layouts/partials/widgets/piano-pieces.html` — Piano pieces sidebar widget
- `layouts/_default/terms.html` — Taxonomy term page

## Configuration Files

| File | Purpose |
|---|---|
| `config/_default/hugo.toml` | Base URL, taxonomies, permalinks, pagination, TOC |
| `config/_default/params.toml` | Logo, navbar, search, widgets, contact form |
| `data/theme.json` | Fonts (Heebo/Signika) and colors (light/dark) |
| `data/social.json` | Social links (currently GitHub only) |
| `i18n/en.yaml` | UI strings (labels, search text, etc.) |
| `archetypes/default.md` | Template for `hugo new` posts |

## Assets

- Images: `assets/images/` — **not** `static/` (no `static/` directory exists)
- Custom CSS: `assets/css/custom.css`
- Theme CSS/JS: `themes/hugoplate/assets/`

## Hugo Modules

Loaded from `github.com/gethugothemes/hugo-modules`. Provides: accordion, gallery, icons (Font Awesome), search, SEO, PWA, social share, shortcodes (button, notice), mermaid diagrams, and more.

## Site Settings (Notable)

- `mainSections = ["music", "writing"]`
- Theme default: `system` (auto light/dark)
- Navbar: fixed to top
- Summary length: 10 words
- Sidebar widgets: categories, tags
- Search: enabled, scoped to piano section
