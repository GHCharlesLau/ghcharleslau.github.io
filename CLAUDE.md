# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Personal academic website for Shaoqiang (Charles) Liu, built with **Jekyll** using the [al-folio](https://github.com/alshedivat/al-folio) theme. Deployed to GitHub Pages at `ghcharleslau.github.io`.

## Build & Development Commands

### Docker (recommended)
```bash
docker compose pull        # Pull latest image
docker compose up          # Dev server at http://localhost:8080
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
- `_bibliography/papers.bib` — publications (managed by jekyll-scholar)

**Content Collections**:
- `_posts/` — blog posts (Markdown)
- `_projects/` — portfolio projects
- `_news/` — homepage news/announcements
- `_pages/` — site pages (about, cv, blog, publications, etc.)
- `_books/` — book reviews

**Styling**: SCSS in `_sass/`, compiled to compressed CSS. Key files: `_base.scss`, `_layout.scss`, `_variables.scss`, `_themes.scss`. Theme colors defined in `_config.yml` under `repo_theme_light`/`repo_theme_dark`.

**JavaScript**: Vanilla JS in `assets/js/`. Key modules: `common.js`, `theme.js`, `masonry.js`, `search-setup.js`.

**Features controlled in _config.yml**: `enable_darkmode`, `enable_masonry`, `enable_math`, `enable_progressbar`, `enable_medium_zoom`, `search_enabled`, `navbar_fixed`.

## Deployment

Automatic via GitHub Actions (`.github/workflows/deploy.yml`) on push to `main`. Builds site and deploys to `gh-pages` branch for GitHub Pages.

## Customization Notes

- CV page reads from `resume.json` (priority) or `_data/cv.yml` (fallback)
- Publications use BibTeX with jekyll-scholar — edit `_bibliography/papers.bib`
- Profile image goes in `assets/img/` and is referenced in `_config.yml` or the about page
- Blog posts go in `_posts/` with filename format `YYYY-MM-DD-title.md`
- Third-party library versions and SRI hashes are pinned in `_config.yml` under `third_party_libraries`
