# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Website for the Mount Si High School Dance Team — a Hugo static site using the PaperMod theme, deployed on Netlify. Same infrastructure as the devrelpatterns.com project.

## Development Commands

```bash
hugo server -D          # local dev server at http://localhost:1313
hugo --minify           # production build into public/
```

Hugo version: 0.158.0 (specified in `netlify.toml`; PaperMod requires 0.158.0+).

## Architecture

- **Theme**: PaperMod, installed as a git submodule in `themes/PaperMod`. Do not edit theme files directly — use layout overrides instead.
- **Layouts** (`layouts/`): `home.html` for the home page, plus one layout per section page (`about.html`, `boosters.html`, `performances.html`, `camps.html`, `tryouts.html`, `photos.html`), selected via `layout:` in each page's frontmatter. Every page wraps its content in `.msd-layout`; navigation is the PaperMod header menu (`[menu.main]` in `hugo.toml`).
- **Partials** (`layouts/_partials/`): `photo.html` (renders an image from `static/`, or a labeled placeholder if the file doesn't exist yet), `schedule.html`, `sponsor.html`, `page_header.html`.
- **Header override**: `layouts/_partials/header.html` is a copy of PaperMod's header whose only change is a star (instead of a moon) for the theme toggle. If the theme's header changes upstream, re-copy it and reapply that one change.
- **Home section cards**: the icon cards under the home intro come from `[[params.sections]]` in `hugo.toml`. Contact links (Instagram, coach email) live in `params.footer.text`.
- **Custom CSS**: `assets/css/extended/custom.css` — PaperMod's extension point. Palette: school-gray backgrounds with rose (`--msd-red`), blush, and gold accents; fonts are Playfair Display (headings) and Jost (body). No emojis or script fonts. Class prefix is `msd-`.

## Content

All content is single Markdown pages in `content/` with structured lists in YAML frontmatter:
- `_index.md` — home tagline and `feature_camp` (when true, the home page shows the camp flyer from `camps.md` first; edit the flyer only in `camps.md`).
- `about.md` — `team_photo`, optional `leadership_photo` + `leadership_shoutout`, `coaches`; body is the team bio.
- `boosters.md` — `contacts` (booster board, adults), `fundraisers` (past dates hidden), `sponsor_tiers` (level + sponsors with name/logo/url, highest tier first; a logo shows only once its file exists in `static/images/sponsors/`).
- `performances.md` — `performances` and `competitions` (event/date/end_date/time/location/map/notes); each renders as a season schedule table (`schedule.html`) with past rows muted and the next one marked.
- `camps.md` — `photo`, `camps` (name/dates/ages/location/cost/details/register).
- `photos.md` — `gallery` photo list (files in `static/images/gallery/`; the first photo is shown large).
- `tryouts.md` — `signup` link, `key_dates` (past dates shown as last season's); body is tryout details.

**Never add student names or personal info — dancers are minors.** Empty lists hide their section.

Date-based upcoming/past splits are computed at build time, so they update on each deploy.

## Deployment

Netlify auto-deploys from the main branch. Build command: `hugo --minify`, publish directory: `public/`.
