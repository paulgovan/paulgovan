# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository purpose

This is Paul Govan's personal website/portfolio, served via GitHub Pages at `paulgovan.com` (custom domain set via `CNAME`). It doubles as the GitHub profile README for the `paulgovan` account.

## Structure

- `index.html` — the entire site: single self-contained HTML file with inline `<style>` and inline `<script>`. No build step, no framework, no dependencies, no package.json.
- `README.md` — GitHub profile README (rendered on `github.com/paulgovan`), separate content from `index.html` but overlapping in purpose (bio, projects, contact links).
- `logos/` — static image assets (company logos, project hex stickers) referenced by both `index.html` and `README.md`.
- `headshot*.png/webp`, `apple-touch-icon.png` — profile images used in `index.html` meta tags and hero section.
- `robots.txt`, `sitemap.xml`, `CNAME` — GitHub Pages / SEO config.

## Running locally

Static site, no build/install/lint/test commands. Preview with any static file server, e.g.:

```
python3 -m http.server 8080
```

(A VS Code launch config for this already exists at `.claude/launch.json`.) Then open `http://localhost:8080`.

## Working in index.html

- Everything lives in one file. Sections are ordered: nav → hero → About → Experience → Education → Certifications → Publications (Books/Articles subsections) → Projects → Service → Contact → footer, each with a matching nav anchor (`#about`, `#experience`, etc.).
- Styling uses CSS custom properties defined in `:root` and overridden under `[data-theme="dark"]` for dark mode — when adding new colored elements, use the existing custom properties (`--primary`, `--accent`, `--surface`, `--card`, `--text`, `--muted`, `--border`) rather than hardcoding colors, so dark mode keeps working.
- Responsive breakpoints are handled with plain media queries at `768px` and `380px` near the bottom of the `<style>` block — mirror existing patterns there for new components rather than introducing a new responsive approach.
- Timeline/list entries (Experience, Education, Certifications, Service) follow a repeated `.card` / `.card-inner` markup pattern with a logo image (from `logos/`), title, org, meta line, and description — copy an existing `.card` block when adding an entry.
- Project entries in the Projects grid follow a `.project-card` pattern, often including CRAN badge images (`r-pkg.org`/`cranlogs.r-pkg.org`) for R packages.
- The `<script type="application/ld+json">` block in `<head>` contains Schema.org `Person` structured data (job, employer, alumni, `sameAs` profile links) — keep this in sync when bio/employer/social links change.
- Vanilla JS at the bottom handles: dark mode toggle (persisted to `localStorage`), scroll-triggered fade-in animations, and the back-to-top button. No external JS libraries.

## Keeping content in sync

`index.html` and `README.md` both list projects/bio/contact info independently — when adding or updating a project, check both files. Logo images in `logos/` are shared between them.
