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
- **Layouts** (`layouts/`): `home.html` for the home page, plus one layout per section page (`about.html`, `boosters.html`, `performances.html`, `camps.html`, `tryouts.html`), selected via `layout:` in each page's frontmatter. Every page uses the two-column `.msd-layout` with the sidebar partial.
- **Partials** (`layouts/_partials/`): `sidebar.html` (links come from `[[params.sidebar]]` in `hugo.toml`), `photo.html` (renders an image from `static/`, or a labeled placeholder if the file doesn't exist yet), `performance.html`, `sponsor.html`, `page_header.html`.
- **Custom CSS**: `assets/css/extended/custom.css` — PaperMod's extension point. Team colors are the `--msd-red*` variables. Class prefix is `msd-`.

## Content

All content is single Markdown pages in `content/` with structured lists in YAML frontmatter:
- `_index.md` — home tagline and `gallery` photo list.
- `about.md` — `team_photo`, optional `leadership_photo` + `leadership_shoutout`, `coaches`; body is the team bio.
- `boosters.md` — `contacts`, `fundraisers` (past dates hidden), `sponsors` (name/level/logo/url).
- `performances.md` — `performances` (event/date/time/location/map/notes); past dates move to "Earlier This Season".
- `camps.md` — `photo`, `camps` (name/dates/ages/location/cost/details/register).
- `tryouts.md` — `signup` link, `key_dates` (past dates shown as last season's); body is tryout details.

**Never add student names or personal info — dancers are minors.** Empty lists hide their section.

Date-based upcoming/past splits are computed at build time, so they update on each deploy.

## Deployment

Netlify auto-deploys from the main branch. Build command: `hugo --minify`, publish directory: `public/`.
