# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Personal academic website for Shaoqiang (Charles) Liu, built with **Jekyll** using the [al-folio](https://github.com/alshedivat/al-folio) theme (v0.14.7). Deployed to GitHub Pages at `ghcharleslau.github.io`.

## Build & Development Commands

### Docker (recommended)
```bash
docker compose pull        # Pull latest image
docker compose up          # Dev server at http://localhost:8080
docker compose restart     # Restart after SCSS changes (needed for CSS recompile)
```

### Local Ruby setup
```bash
bundle install
bundle exec jekyll serve   # Dev server at http://localhost:4000
bundle exec jekyll build   # Production build to _site/
```

### Formatting
```bash
npx prettier --write .    # Format Liquid/SCSS/JS
```

## Architecture

**Template Engine**: Liquid (Jekyll). Layouts in `_layouts/*.liquid`, reusable components in `_includes/`.

**Key Data Flow**:
- `_config.yml` — global site config (navbar, features, analytics, library versions, colors)
- `assets/json/resume.json` — CV data (jsonresume.org format), loaded via `jekyll-get-json` into `site.resume`
- `_data/cv.yml` — YAML fallback for CV if JSON is unavailable
- `_data/socials.yml` — social media links
- `_data/presentations.yml` — conference presentations (rendered on Home page)
- `_bibliography/papers.bib` — publications (managed by jekyll-scholar)

**Content Collections**:
- `_posts/` — blog posts (Markdown, currently empty)
- `_projects/` — portfolio projects (currently empty)
- `_news/` — homepage news/announcements (currently empty)
- `_pages/` — site pages (about, cv, blog, publications, etc.)
- `_books/` — book reviews

**Home Page Layout** (`_layouts/about.liquid`):
- Profile image floats right, embedded in bio text (not a CSS Grid two-column layout)
- Presentations section is a separate layout block (not inside `{{ content }}`), controlled by `presentations: true` in front matter
- Selected Papers section is a separate layout block, controlled by `selected_papers: true`
- Order: bio text → Presentations → Selected Publications

**Styling**: SCSS in `_sass/`, compiled to compressed CSS. Key files: `_base.scss`, `_layout.scss`, `_variables.scss`, `_themes.scss`.
- **Fonts**: Self-hosted Inter (WOFF2 in `assets/fonts/`), no Google Fonts dependency
- **Theme color**: Emerald/mint (#00d4aa), defined in `_variables.scss` and `_themes.scss`
- **Custom overrides**: Float-right profile, jekyll-scholar `.note` border override, section spacing — all in `_base.scss` near the end of file

**JavaScript**: Vanilla JS in `assets/js/`. Key modules: `common.js`, `theme.js`, `masonry.js`, `search-setup.js`.

**Features controlled in _config.yml**: `enable_darkmode`, `enable_masonry`, `enable_math`, `enable_progressbar`, `enable_medium_zoom`, `search_enabled`, `navbar_fixed`.

## Deployment

Automatic via GitHub Actions (`.github/workflows/deploy.yml`) on push to `main`. Builds site and deploys to `gh-pages` branch for GitHub Pages.

## Customization Notes

- CV page reads from `resume.json` (priority) or `_data/cv.yml` (fallback)
- Publications use BibTeX with jekyll-scholar — edit `_bibliography/papers.bib`
- Presentations use `_data/presentations.yml` — add new entries as YAML list items
- Profile image goes in `assets/img/` and is referenced in `_pages/about.md`
- Blog posts go in `_posts/` with filename format `YYYY-MM-DD-title.md`
- Third-party library versions and SRI hashes are pinned in `_config.yml` under `third_party_libraries`

## Important Notes

- After modifying SCSS files (`_sass/`), restart Docker container for CSS recompilation
- The `_site/` directory is Jekyll build output (gitignored) — never commit it
- Google Fonts dependency has been removed; Inter is self-hosted in `assets/fonts/`
