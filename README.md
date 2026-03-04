# Effective Flow Websites

This repo contains two Hugo sites deployed to separate Azure Static Web Apps.

## Sites

| Site | Directory | Domain | Azure SWA | Secret |
|------|-----------|--------|-----------|--------|
| Company | `sites/company/` | effective-flow.ch | victorious-island-06ef03503 | `AZURE_STATIC_WEB_APPS_API_TOKEN_VICTORIOUS_ISLAND_06EF03503` |
| 2Reflect | `sites/2reflect/` | 2reflect.effective-flow.com | agreeable-stone-0fdc8de03 | `AZURE_STATIC_WEB_APPS_API_TOKEN_AGREEABLE_STONE_0FDC8DE03` |

## Stack

- Hugo (extended) 0.150.0
- Azure Static Web Apps (Free plan)
- GitHub Actions

## Local Setup (Windows)

Install Hugo Extended:

- `winget install Hugo.Hugo.Extended`

Run either site locally:

```
cd sites/company
hugo server -D
```

```
cd sites/2reflect
hugo server -D
```

Sites are available at `http://localhost:1313`.

## Content Structure

### Company site (`sites/company/`)
- Home page: company intro and consulting
- Blog: `content/blog/`
- Contact: `content/contact.md`

### 2Reflect product site (`sites/2reflect/`)
- Landing page: product hero, features, CTAs
- Privacy policy: `content/privacy-policy.md`

## Branching and Deployment Strategy

- `main` -> production environment (both SWAs)
- `staging` -> staging environment (both SWAs)
- feature branches -> PR to `staging` for review
- promote by PR from `staging` to `main`

## GitHub Actions

- CI build check: `.github/workflows/ci.yml` (builds both sites)
- Company deploy: `.github/workflows/deploy-company.yml`
- 2Reflect deploy: `.github/workflows/deploy-2reflect.yml`

Deploy workflows use path filters so only the affected site is rebuilt and deployed when its files change.
