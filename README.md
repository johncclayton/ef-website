# Effective Flow Website

Hugo-based website for Effective Flow, focused on the 2Reflect product, with a starter blog and Azure Static Web Apps deployment workflows.

## Stack

- Hugo (extended)
- Azure Static Web Apps (Free plan)
- GitHub Actions

## Local Setup (Windows)

Install Hugo Extended with one of the following:

- `winget install Hugo.Hugo.Extended`
- `choco install hugo-extended -confirm`

Verify install:

- `hugo version`

Run locally:

- `hugo server -D`

The site is available at `http://localhost:1313`.

## Content Structure

- Product content: `content/2reflect/_index.md`
- Blog section: `content/blog/`
- Contact page: `content/contact.md`

## Branching and Deployment Strategy

- `main` -> production environment
- `staging` -> stable pre-production branch environment
- feature branches -> PR to `staging` for review
- promote by PR from `staging` to `main`

## GitHub Actions

- CI build check: `.github/workflows/ci.yml`
- Azure deploy workflow: `.github/workflows/azure-static-web-apps-jolly-water-0d22fdc03.yml`

The Azure workflow deploys for pushes to both `main` and `staging`, and creates PR preview environments.

## Azure Static Web Apps Setup Checklist

1. Create Azure Static Web App (Free plan) connected to this repo.
2. Set production branch to `main`.
3. Confirm workflow secret exists in GitHub:
   - `AZURE_STATIC_WEB_APPS_API_TOKEN_JOLLY_WATER_0D22FDC03`
4. Create and push `staging` branch.
5. Confirm `staging` environment URL appears after first `staging` push.
6. Add custom domain to production environment only.

## Free Plan Notes

- Supports your required `main` + `staging` + PR preview flow.
- Limits include:
  - 3 preview environments per app
  - 250 MB per environment (500 MB total storage)
  - 100 GB/month included bandwidth
  - no SLA
