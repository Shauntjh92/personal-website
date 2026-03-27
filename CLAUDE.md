# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static personal portfolio website for **Shaun Toh** (Data Scientist / Analytics Engineer), hosted on **Cloudflare Pages** via GitHub auto-deploy. The site replicates the visual design of the [Hideo WordPress theme](https://andersnoren.se/themes/hideo/) as a pure static HTML/CSS site — no framework, no build step.

## Deployment

- **GitHub repo:** `https://github.com/Shauntjh92/personal-website`
- **Hosting:** Cloudflare Pages, connected to the GitHub repo (auto-deploys on push to `main`)
- **Deploy command:** none (static HTML, output directory = `/`)
- **Live URL:** `personal-website.pages.dev`

To deploy any change:
```bash
git add index.html
git commit -m "describe change"
git push
```
Cloudflare picks it up automatically within ~1 minute.

## File Structure

```
Personal_website/
├── index.html                          ← the entire site (single file)
├── Profile-pic-Halfbody.jpg            ← profile photo (referenced in index.html)
├── Resume-Toh Jia Hui Shaun_180126_DS.pdf  ← CV (linked as download in index.html)
├── hideo/                              ← original Hideo theme (fonts + assets only used)
│   └── assets/
│       └── fonts/
│           ├── instrument-serif/       ← heading font (woff2)
│           └── open-sauce-two/        ← body font (woff2)
└── .gitignore                          ← excludes .DS_Store and *.zip
```

The `hideo/` folder is not a functioning WordPress theme here — it is kept solely because `index.html` references its font files via relative paths (e.g. `hideo/assets/fonts/instrument-serif/instrument-serif-400.woff2`).

## Design System (from Hideo theme.json)

All styling lives inside a `<style>` block in `index.html`. CSS variables:

| Variable | Light value | Dark value | Usage |
|---|---|---|---|
| `--color-10` | `#ECE7E1` | `#1a1a22` | Page background |
| `--color-100` | `#15151C` | `#ECE7E1` | Primary text |
| `--color-30` | `#D4CFC8` | `#2e2e3a` | Borders, card hover |
| `--color-70` | `#75736E` | `#8a8880` | Secondary/dim text |
| `--color-0` | `#FFFFFF` | `#0f0f16` | White |
| `--body-margin` | `clamp(24px, 4.166vw, 32px)` | — | Universal padding |
| `--font-heading` | Instrument Serif | — | All `h1`/`h2`/`h3` |
| `--font-body` | Open Sauce Two | — | All body text |

Dark mode is applied via `[data-theme="dark"]` on `<html>`. Toggle persists to `localStorage` under the key `theme`.

Font sizes:
- H1: `clamp(72px, 10vw, 128px)`
- H2: `clamp(56px, 8vw, 96px)`
- Body: `clamp(16px, 1vw, 18px)`
- Bio text (`--fs-large`): `clamp(15px, 1vw, 17px)`

## Layout

**Desktop:** 256px sticky sidebar (left) + flexible main content (right)
- Sidebar: `position: sticky; top: 0; height: 100vh; border-right: 1px solid #D4CFC8`
- Desktop header bar: job title (left) + GitHub icon + dark mode toggle (right), `border-bottom: 1px solid #D4CFC8` — name was removed

**Mobile (≤768px):** Sticky top bar with name (left) + GitHub icon + dark mode toggle + hamburger (right) → full-screen nav overlay

## Page Sections

| Section | ID | Notes |
|---|---|---|
| About | `#about` | Bio, profile photo, CV download + LinkedIn buttons; heading is "About" (no name) |
| Projects | `#projects` | Cards grid; two projects: Wifey App, Analyst AI Dashboard |
| Skills | `#skills` | Pill-tag groups by category |
| Footer | — | LinkedIn link only (copyright removed) |

## Owner Content

- **Name:** Shaun Toh
- **Title:** Data Scientist / Analytics Engineer
- **LinkedIn:** `https://www.linkedin.com/in/shauntjh-s629952r/`
- **GitHub:** `https://github.com/Shauntjh92`
- **CV file:** `Resume-Toh Jia Hui Shaun_180126_DS.pdf`
- **Profile photo:** `Profile-pic-Halfbody.jpg`

### Projects
| Name | URL | Description |
|---|---|---|
| Wifey App | `https://github.com/Shauntjh92/Wifey-app` | Singapore mall store finder — FastAPI + PostgreSQL + React |
| Analyst AI Dashboard | `https://github.com/Shauntjh92/Analyst_AI_Dashboard` | A simple analyst AI who can help give high level insights |

### Skills
- **Programming:** Python, PySpark
- **Data Management:** Microsoft SQL Server, MySQL, Presto
- **Project Management:** Azure DevOps, JIRA, Confluence
- **Data Visualization:** Tableau, Power BI
- **Certifications:** MSc. Intelligent Systems, Specialist Diploma in Artificial Intelligence

## Common Edits

**Add a new project:** Add another `<a class="project-card" ...>` block inside `.projects-grid` in `index.html`.

**Update CV:** Replace `Resume-Toh Jia Hui Shaun_180126_DS.pdf` with a new file, then update both `href` references in `index.html` (URL-encode spaces as `%20`).

**Change bio text:** Edit the `<p>` tags inside `.about-text` in `index.html`.

**Adjust font sizes:** Edit CSS variables in the `:root` block at the top of the `<style>` tag.

**Toggle dark mode colours:** Edit the `[data-theme="dark"]` block directly below `:root` in the `<style>` tag.

**Add header action icons:** Add `.icon-btn` elements inside `.header-actions` (desktop) and `.mobile-header-right` (mobile).
