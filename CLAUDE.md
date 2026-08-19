# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Is

A static website for [Domus Aurea](https://domus-aurea.ie/) built with [Hugo](https://gohugo.io/) using the [HugoBlox Academic CV theme](https://hugoblox.com/). It deploys to GitHub Pages via a CI workflow and is also configured for Netlify deployment.

## Development Commands

```bash
# Install dependencies (uses pnpm)
pnpm install

# Local dev server with live reload — serves at http://localhost:1313
hugo server --disableFastRender
# or
pnpm dev

# Include draft posts (date in future or draft: true in frontmatter)
hugo server --disableFastRender --buildDrafts --buildFuture

# Production build
hugo --gc --minify
# or
pnpm build
```

Hugo Extended is required (version 0.152.x). Also needs Go 1.19+ (for Hugo modules) and Dart Sass.

## Architecture

This is a Hugo static site — no backend, no database, no API. All content is Markdown with YAML frontmatter.

**Config layer** (`config/_default/`):
- `hugo.yaml` — site-wide Hugo settings, baseURL, taxonomies, output formats
- `params.yaml` — theme appearance (light/indigo), navbar, footer, SEO
- `menus.yaml` — navigation links (order controlled by `weight`)
- `module.yaml` — Hugo module imports (HugoBlox Netlify plugin + Tailwind) and mount points for custom blox layouts

**Content** (`content/`): Each section is a directory with an `index.md`. The homepage (`_index.md`) uses `type: landing` with HugoBlox `sections` blocks. Author profile pages are suppressed from rendering (`content/authors/_index.md` sets `render: never`).

**Customization**:
- `assets/css/custom.css` — site-specific style overrides (Tailwind CSS v4 is the base framework)
- `layouts/partials/hooks/head-end/github-button.html` — injects the GitHub buttons script into `<head>`; this is a HugoBlox hook point

**Deployment**:
- GitHub Pages: `.github/workflows/hugo.yml` builds on push to `main` using Hugo Extended 0.152.2
- Netlify: `netlify.toml` uses `pnpm install && hugo --minify` and runs `pagefind` for search indexing after build

## Content Types and How to Edit Them

### Blog Posts

Blog posts live under `content/blog/<post-slug>/index.md`. Each post is a directory (page bundle) so it can include its own images.

Minimal frontmatter:
```yaml
---
title: My Post Title
date: 2025-01-15
summary: One-sentence description shown in listings.
tags:
  - SomeTag
---
```

To show a featured image in the blog grid, place a `featured.jpg` or `featured.png` in the post's directory. The blog listing page (`content/blog/_index.md`) uses `view: article-grid`.

HugoBlox callout syntax works in blog post bodies:
```markdown
> [!NOTE]
> This is a note callout.

> [!TIP]+ Collapsible tip
> Content here.
```

### Simple Pages (Links, Contact, Donations, Catholic Life, etc.)

These use `type: page` in the frontmatter and suppress metadata noise with:
```yaml
reading_time: false
show_related: false
pager: false
```

Body is plain Markdown. Inline `<style>` blocks are used on some pages (e.g. Prayers, Books, Gallery) since HugoBlox renders `unsafe: true` — raw HTML and `<script>` tags are allowed in content files.

### Videos Page

Uses the built-in Hugo YouTube shortcode:
```markdown
{{< youtube VIDEO_ID >}}
```

### Books Page

Uses inline HTML with Tailwind utility classes to render a responsive image grid with a JavaScript lightbox. Images are referenced as absolute paths from `static/` — place book cover images in `content/books/` (they are served from `/books/`).

### Gallery Page

Uses a raw HTML CSS grid in the content body. Images are currently placeholder URLs; replace them with paths to actual images placed in `static/` or `content/gallery/`.

### Homepage (`content/_index.md`)

Uses `type: landing` with a `sections:` list of HugoBlox blocks. The current block is `resume-biography-3`, which pulls from the `admin` author profile. Add more sections by appending block entries — no template editing needed. Available blocks are documented at [https://hugoblox.com/blocks/](https://hugoblox.com/blocks/).

## Adding a New Section

1. Create `content/<section-name>/index.md` with appropriate frontmatter
2. Add a menu entry in `config/_default/menus.yaml`:
   ```yaml
   - name: My Section
     url: my-section/
     weight: 50   # controls nav order; existing items range from 10–43
   ```

## Customizing Styles

All custom CSS goes in `assets/css/custom.css`. The base framework is Tailwind CSS v4 so utility classes are available in content HTML. For scoped page styles, inline `<style>` blocks inside `index.md` content files work fine (unsafe HTML is enabled globally).
