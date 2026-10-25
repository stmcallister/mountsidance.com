# Mount Si Dance Team

Website for the Mount Si High School Dance Team, built with [Hugo](https://gohugo.io/) and the [PaperMod](https://github.com/adityatelange/hugo-PaperMod) theme. Deployed on Netlify at [mountsidance.com](https://mountsidance.com).

## Prerequisites

- [Hugo](https://gohugo.io/installation/) v0.158.0 or later (extended edition recommended)
- [Git](https://git-scm.com/)

## Setup

```bash
git clone <repo-url> mountsidance.com
cd mountsidance.com
git submodule update --init --recursive
```

The submodule step is required to pull in the PaperMod theme.

## Local Development

```bash
hugo server -D
```

Open `http://localhost:1313`. The site reloads as you edit.

## Updating Content

Every page is a Markdown file in `content/`. Lists (performances, sponsors, leaders, etc.) live in the frontmatter at the top of each file — copy an existing entry and edit it.

| Page | File | What to edit |
|------|------|--------------|
| Home | `content/_index.md` | `tagline`, `gallery` photos, welcome text |
| About Our Team | `content/about.md` | Team bio (body), optional `leadership_photo` + `leadership_shoutout`, `coaches` |
| Boosters & Sponsors | `content/boosters.md` | `contacts`, `fundraisers`, `sponsors` |
| Performances | `content/performances.md` | `performances` |
| Youth Camps | `content/camps.md` | `camps` |
| Tryouts | `content/tryouts.md` | `key_dates`, `signup` link, details (body) |

**No student names or personal info** — dancers are minors. Leadership shoutouts are a group message, not individual cards.

Empty lists (e.g. `sponsors: []`) hide their section; commented-out examples show the fields.

Dates use `YYYY-MM-DD`. Tryout dates that have passed are shown as "Last Season's Tryouts" until new dates are added. Past performances move to "Earlier This Season" and past fundraisers are hidden automatically on the next build.

## Photos

Add images under `static/images/` using the paths referenced in the frontmatter. Until a file exists, the site shows a striped placeholder labeled with the expected path.

| Photo | Path |
|-------|------|
| Home gallery (first is shown large) | `static/images/gallery/` (listed in `content/_index.md`) |
| Team photo | `static/images/team/team-photo.jpg` |
| Leadership photo (optional) | `static/images/team/leadership-photo.jpg` |
| Sponsor logos | `static/images/sponsors/` |
| Youth camp | `static/images/camps/youth-camp.jpg` |

To use different filenames, update the matching `src` / photo field in the content file.

The current photos came from the old Carrd site (mountsidanceteam.carrd.co) and are fairly low resolution (~450px tall). Swap in the originals when available.

## Sidebar & Menu

The sidebar links are configured under `[[params.sidebar]]` in `hugo.toml`, with the Instagram handle and contact email under `[params.contact]`. The top menu is under `[menu]`.

## Deployment

Netlify builds with `hugo --minify` and publishes `public/` (see `netlify.toml`).
