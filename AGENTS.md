# Effective Flow — Monorepo Agent Guide

## Overview

This is a Hugo monorepo containing two independent static websites for the Effective Flow company. Both sites are deployed to separate Azure Static Web Apps instances via GitHub Actions.

## Sites

| Site | Directory | Domain |
|------|-----------|--------|
| Company | `sites/company/` | effective-flow.ch |
| 2Reflect product | `sites/2reflect/` | 2reflect.effective-flow.com |

See `sites/company/AGENTS.md` and `sites/2reflect/AGENTS.md` for site-specific guidance.

## Stack

- **Hugo Extended 0.150.0** — no Node.js, no npm, no package.json
- **Azure Static Web Apps** (Free plan) — one instance per site
- **GitHub Actions** — CI and deploy workflows in `.github/workflows/`

## Local Development

Each site is run independently from its own directory:

```
cd sites/company
hugo server -D
```

```
cd sites/2reflect
hugo server -D
```

Both are available at `http://localhost:1313`. There is no root-level build command.

## Shared CSS

`assets/css/site.css` is **duplicated** in both sites — there is no shared symlink or import. If CSS changes are needed, update **both** files:

- `sites/company/assets/css/site.css`
- `sites/2reflect/assets/css/site.css`

## Branching and Deployment

- `main` → production (both sites)
- `staging` → staging environment (both sites)
- Feature branches → PR to `staging` → PR to `main`

Deploy workflows use **path filters** so only the affected site is rebuilt when its files change. Do not merge changes across site directories unnecessarily.

## GitHub Actions Workflows

| File | Purpose |
|------|---------|
| `.github/workflows/ci.yml` | Builds both sites on every PR |
| `.github/workflows/deploy-company.yml` | Deploys company site |
| `.github/workflows/deploy-2reflect.yml` | Deploys 2Reflect site |

The `azure-static-web-apps-*.yml` file is **Azure-generated** — do not edit it manually.

## Hugo Conventions

- No Hugo theme is used — all layouts are fully custom in each site's `layouts/` directory
- Templates follow standard Hugo layout lookup: `baseof.html` → `single.html` / `list.html` / `index.html`
- Partials are in `layouts/partials/` — `header.html` and `footer.html` wrap all pages
- Site parameters (title, URLs, taglines) are defined in each site's `hugo.toml`
