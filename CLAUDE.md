# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a **Hugo Blox** academic CV website (domus-aurea.ie) built with the Academic CV template. It uses Hugo as the static site generator, with Tailwind CSS v4 for styling and Preact for interactive components. The site is deployed to GitHub Pages via GitHub Actions.

## Key Technologies

- **Hugo Extended v0.152.2** - Static site generator (requires extended version for SCSS/SASS)
- **Hugo Blox Builder** - Academic template framework with modular blocks
- **Go v1.19+** - Required for Hugo modules
- **Tailwind CSS v4** - Styling framework
- **Preact** - Lightweight React alternative for interactive components
- **pnpm v10.14.0** - Package manager

## Development Commands

### Local Development
```bash
# Install dependencies (first time setup)
pnpm install

# Run local development server
pnpm dev
# Equivalent to: hugo server --disableFastRender

# Build for production
pnpm build
# Equivalent to: hugo --minify
```

### Hugo Commands
```bash
# Start Hugo server (with fast render disabled for complete rebuilds)
hugo server --disableFastRender

# Build with minification
hugo --minify

# Build with garbage collection and base URL
hugo --gc --minify --baseURL "https://domus-aurea.ie/"
```

## Architecture

### Hugo Modules System
The site uses **Hugo Modules** (not npm/node modules) for theme management via `go.mod`. Two key modules are imported:
- `blox-plugin-netlify` - Netlify deployment integration
- `blox-tailwind` - Tailwind CSS integration

Module configuration in `config/_default/module.yaml` mounts custom blocks from `hugo-blox/blox/` directories.

### Configuration Structure
Hugo Blox uses a split configuration system in `config/_default/`:
- `hugo.yaml` - Core Hugo settings (site title, baseURL, taxonomies, markup)
- `params.yaml` - Site-specific parameters (appearance, SEO, header, footer)
- `languages.yaml` - Multi-language configuration
- `menus.yaml` - Navigation menu structure
- `module.yaml` - Hugo module imports and mounts

### Content Organization
Content is in `content/` with standard Hugo sections:
- `_index.md` - Homepage with Hugo Blox blocks/widgets
- `authors/` - Author profiles
- `blog/` - Blog posts
- `courses/` - Course materials and guides
- `events/` - Event listings
- `experience.md` - Professional experience
- `projects/` - Project showcases
- `publications/` - Academic publications

### Hugo Blox Blocks System
The homepage (`content/_index.md`) uses Hugo Blox's block/widget system. Each section is a YAML block definition with parameters like `block`, `content`, `design`, etc. Custom blocks can be added to `layouts/_partials/blox/`.

### Asset Pipeline
- Custom layouts: `layouts/` (currently only `layouts/partials/`)
- Assets: `assets/` for custom CSS, JS, images
- Static files: `static/` for files served as-is
- Tailwind CLI processes styles during build

## GitHub Pages Deployment

The site automatically deploys via `.github/workflows/hugo.yml` on push to `main` branch:

1. **Build environment setup**: Installs Dart Sass, Go, Hugo Extended, Node.js
2. **Dependency installation**: Runs `npm ci` for package-lock.json
3. **Hugo build**: Builds with `--gc --minify` and Hugo cache
4. **Pages deployment**: Uploads to GitHub Pages with artifact upload

**Important versions** (defined in workflow):
- Hugo: 0.152.2 (extended)
- Go: 1.25.3
- Node.js: 22.20.0
- Dart Sass: 1.93.2

## Important Notes

- Always use **Hugo Extended** - required for SCSS/Tailwind processing
- Use **pnpm** as package manager (specified in package.json)
- Git must be configured with `core.quotepath false` for proper Unicode handling
- Hugo modules require Go to be installed
- The site uses `disableFastRender` in dev for complete rebuilds (Hugo's fast render can miss some updates)
- Content files use YAML frontmatter with Hugo Blox's block syntax
- The workflow caches Hugo build artifacts to speed up deployment

## Customization Areas

- **Theme/Colors**: Modify `params.yaml` appearance section
- **Navigation**: Edit `menus.yaml`
- **SEO**: Update marketing section in `params.yaml`
- **Custom blocks**: Add HTML to `layouts/_partials/blox/`
- **Styling**: Add custom Tailwind classes or CSS to `assets/`
