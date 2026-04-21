# Website Maintenance Guide

Personal academic website of Shaoqiang (Charles) Liu, built with [Jekyll](https://jekyllrb.com/) and the [al-folio](https://github.com/alshedivat/al-folio) theme (v0.14.7).

---

## Quick Start

### Local Development (Docker)

```bash
docker compose pull        # Pull latest image
docker compose up          # Start dev server at http://localhost:8080
docker compose down        # Stop server
docker compose restart     # Restart after config/code changes
```

### Local Development (Ruby)

```bash
bundle install
bundle exec jekyll serve   # Dev server at http://localhost:4000
bundle exec jekyll build   # Production build to _site/
```

> **Note:** After modifying SCSS files (`_sass/`), you must restart the Docker container for changes to compile. HTML/Markdown/Liquid changes are auto-detected via `--watch`.

---

## Site Structure

```
├── _config.yml              # Global config (navbar, fonts, features, colors)
├── _pages/
│   ├── about.md             # Home page (permalink: /)
│   ├── blog.md              # Blog listing
│   ├── publications.md      # Full publications page
│   ├── projects.md          # Portfolio projects
│   ├── cv.md                # CV page
│   └── news.md              # News/announcements archive
├── _posts/                  # Blog posts (filename: YYYY-MM-DD-title.md)
├── _projects/               # Project cards (markdown)
├── _news/                   # News items (markdown)
├── _bibliography/
│   └── papers.bib           # Publications (BibTeX, used by jekyll-scholar)
├── _data/
│   ├── socials.yml          # Social media links & usernames
│   └── cv.yml               # CV data (YAML fallback)
├── assets/
│   ├── json/resume.json     # CV data (JSON, primary source)
│   ├── img/                 # Images (profile, thumbnails)
│   └── pdf/                 # PDF files (CV download)
├── _includes/               # Reusable Liquid components
│   ├── header.liquid        # Navbar
│   ├── footer.liquid        # Footer
│   ├── social.liquid        # Social icon renderer
│   └── ...
├── _layouts/                # Page layouts (about, default, cv, page)
├── _sass/                   # SCSS stylesheets
│   ├── _variables.scss      # Color variables
│   ├── _themes.scss         # Light/dark theme definitions
│   ├── _base.scss           # Base styles + custom enhancements
│   └── _layout.scss         # Layout styles
└── .github/workflows/
    └── deploy.yml           # Auto-deploy to GitHub Pages on push to main
```

---

## Common Tasks

### Update Social Media Links

Edit `_data/socials.yml`. Supported keys:

| Key | Description | Example |
|-----|-------------|---------|
| `email` | Email address | `user@example.com` |
| `github_username` | GitHub handle | `GHCharlesLau` |
| `instagram_id` | Instagram handle | `username` |
| `x_username` | X/Twitter handle (without @) | `Charles_Anan` |
| `xiaohongshu_id` | Xiaohongshu user ID | `2745147159` |
| `scholar_userid` | Google Scholar ID | `your_scholar_id` |
| `linkedin_username` | LinkedIn handle | `username` |
| `orcid_id` | ORCID ID | `0000-0000-0000-0000` |
| `rss_icon` | Show RSS feed icon | `true` / `false` |

### Add a New Publication

1. Open `_bibliography/papers.bib`
2. Add a new `@article` entry:

```bibtex
@article{author2024title,
  abbr={SHORT},
  title={Your Paper Title},
  author={Last, First and Last, First and Liu, S.},
  journal={Journal Name},
  volume={1},
  number={1},
  pages={1--10},
  year={2024},
  doi={10.xxxx/xxxxx},
  html={https://doi.org/10.xxxx/xxxxx},
  selected={true}    # Show on Home page
}
```

3. If you want it shown on the Home page, set `selected={true}`.

### Add a Blog Post

Create a new file in `_posts/` with the naming format `YYYY-MM-DD-title.md`:

```markdown
---
layout: post
title: "Your Post Title"
date: 2025-01-15
categories: [research, methods]
tags: [computational, social-media]
description: A brief description of your post.
---

Your content here...
```

### Update CV Data

Two sources, in order of priority:

1. **`assets/json/resume.json`** — JSON Resume format (primary)
2. **`_data/cv.yml`** — YAML fallback

Edit either file. Key sections: `education`, `awards`, `publications`, `skills`, `languages`.

### Update Profile Photo

1. Place your photo in `assets/img/` (e.g., `myphoto.jpg`)
2. Edit `_pages/about.md`, update the `profile.image` field:

```yaml
profile:
  image: myphoto.jpg
```

Supported formats: `.jpg`, `.jpeg`, `.png`. WebP versions are auto-generated.

### Upload CV PDF for Download

1. Place your CV PDF in `assets/pdf/` (e.g., `cv.pdf`)
2. Uncomment and update in `_data/socials.yml`:

```yaml
cv_pdf: /assets/pdf/cv.pdf
```

### Add a Conference Presentation

Edit `_pages/about.md`, find the "Presentations" section, and add entries:

```markdown
- **"Your Presentation Title"** — *Conference Name*, Year, Location.
```

---

## Customization

### Color Scheme

The site uses an emerald/mint accent color. Key files:

- `_sass/_variables.scss` — Defines `$emerald-color: #00d4aa` and variants
- `_sass/_themes.scss` — Maps variables to CSS custom properties for light/dark mode

To change the accent color, update `$emerald-color` in `_variables.scss` and the `--global-theme-color` references in `_themes.scss`.

### Font

Currently using **Inter**. To change, edit `google_fonts` in `_config.yml` and the `font-family` in `_sass/_base.scss`.

### Dark Mode

Controlled by `enable_darkmode: true` in `_config.yml`. The toggle button appears in the navbar. Dark mode colors are defined in `html[data-theme="dark"]` block of `_themes.scss`.

### Navbar Features

| Setting | File | Description |
|---------|------|-------------|
| `navbar_fixed: true` | `_config.yml` | Sticky navbar at top |
| `enable_navbar_social: false` | `_config.yml` | Social icons in navbar (currently off; socials shown at page bottom instead) |
| `search_enabled: true` | `_config.yml` | Ctrl+K search |
| `enable_darkmode: true` | `_config.yml` | Light/dark toggle |
| `enable_progressbar: false` | `_config.yml` | Scroll progress bar (currently off) |

### Footer

The footer is inline (not fixed) and displays in grey small text at the end of the Home page. Controlled by `footer_fixed: false` in `_config.yml`. Edit `footer_text` in `_config.yml` to change footer content.

---

## Deployment

The site auto-deploys to GitHub Pages when you push to the `main` branch via the GitHub Actions workflow at `.github/workflows/deploy.yml`.

```bash
git add .
git commit -m "Your commit message"
git push origin main
```

Your site will be live at `https://ghcharleslau.github.io` within a few minutes.

---

## Troubleshooting

| Issue | Solution |
|-------|----------|
| SCSS changes not showing | Restart Docker: `docker compose restart` |
| Page not updating | Hard refresh browser: Ctrl+Shift+R |
| YAML parse error | Check for unquoted colons in values (e.g., use `"BNU, Instructor: Dr. Li"`) |
| Image not loading | Ensure file is in `assets/img/` and filename matches the reference |
| BibTeX not rendering | Check `.bib` syntax; ensure `selected={true}` for Home page display |
| X/Twitter link broken | Remove `@` prefix from `x_username` in `socials.yml` |
| Docker won't start | Ensure Docker Desktop is running; try `docker compose down && docker compose up` |
