# Bug Report & QA Testing

**Date:** 2026-04-21 (final)
**Site:** https://ghcharleslau.github.io
**Tested on:** Docker dev server (localhost:8080) + Chrome DevTools

---

## Test Summary

| Page | Status | Notes |
|------|--------|-------|
| Home (`/`) | PASS | Name, bio, real presentation, 9 publications, 6 socials |
| Blog (`/blog/`) | PASS | Empty (no posts), no template placeholders |
| Publications (`/publications/`) | PASS | 11 papers grouped by year (2024/2023/2022), DOI/HTML buttons |
| Projects (`/projects/`) | PASS | Empty (no projects), no template placeholders |
| CV (`/cv/`) | PASS | Education, awards, skills all present |
| News (`/news/`) | PASS | News items render |
| Dark mode (all pages) | PASS | Emerald `#00d4aa` consistent, dark bg `#1c1c1d`, navbar glass blur works |
| Mobile (375x812) | PASS | Hamburger menu, no overflow |

## Feature Tests

| Feature | Status | Details |
|---------|--------|---------|
| Navbar brand "Shaoqiang (Charles) Liu" | PASS | All pages |
| Nav items capitalized | PASS | Home, Blog, Publications, Projects, CV |
| Glass morphism navbar | PASS | `blur(12px)`, `rgba(255,255,255,0.72)` light / `rgba(28,28,29,0.75)` dark |
| Dark mode toggle | PASS | Both modes verified |
| Social icons (6 total) | PASS | Email, Instagram, X, Xiaohongshu, GitHub, ORCID |
| Social icon size | PASS | Reduced from 64px to 35.2px |
| Social section spacing | PASS | 40px margin-top from content above |
| Footer | PASS | Inline, no background, no border, grey 12px text |
| Profile image | PASS | Shadow, no border, 24px margin-left from text |
| Section dividers | PASS | `1px solid` border-bottom on all h2 headings |
| Inter font | PASS | Confirmed on body |
| Emerald color scheme | PASS | `#00d4aa` in both light and dark modes |
| "Selected Publications" capitalization | PASS | |
| Presentation content | PASS | IAMCR 2025 entry with real data |
| No template placeholder text | PASS | No "Einstein", "Lorem", "cool projects" anywhere |

## Issues Found & Fixed (All Resolved)

1. **"selected publications" not capitalized** — Fixed in `_layouts/about.liquid`
2. **Template description on Projects** — "A growing collection of your cool projects" -> "Academic and research projects."
3. **Template description on Publications** — Updated to "Academic publications in reversed chronological order."
4. **X/Twitter URL double @** — Stripped `@` prefix in `socials.yml`
5. **Xiaohongshu icon incorrect** — Replaced with official Simple Icons SVG path data
6. **Home page too crowded** — Added section spacing, h2 dividers, profile-text gap, social section gap
7. **Social icons too large** — Reduced from 64px to 35.2px
8. **Presentation placeholders** — Replaced with real IAMCR 2025 entry

## Remaining Action Items (User TODO)

- Upload profile photo `myphoto_2025.jpg` to `assets/img/` (currently using placeholder)
- Add more presentations as they occur
- Add blog posts to `_posts/` when ready
- Add projects to `_projects/` when ready
- Add Google Scholar ID in `socials.yml` when available
