# Company Site — Agent Guide

## Purpose

The **Effective Flow** company website at `effective-flow.ch`. Audience: potential consulting clients and people interested in the company's software products.

**Tagline:** "Software and consulting for people who teach and explain."

## Tone

Professional but approachable. Avoid jargon. Focus on clarity and usefulness — this reflects the company's own values.

## Site Structure

```
sites/company/
├── assets/css/site.css       # Styles — also duplicated in sites/2reflect/
├── content/
│   ├── _index.md             # Home page body content
│   ├── contact.md            # Contact page
│   └── blog/
│       ├── _index.md         # Blog list page
│       └── *.md              # Individual blog posts
├── layouts/
│   ├── index.html            # Home page template
│   ├── _default/
│   │   ├── baseof.html       # Base template wrapping all pages
│   │   ├── list.html         # Blog list template
│   │   └── single.html       # Single page/post template
│   └── partials/
│       ├── header.html
│       └── footer.html
└── hugo.toml
```

## Content Authoring

### Blog Posts

New posts go in `content/blog/` as `.md` files with front matter:

```markdown
---
title: "Post Title"
date: 2026-03-05
draft: false
---

Post content here.
```

- Use `draft: true` while writing; set to `false` to publish
- Run with `hugo server -D` to preview drafts locally

### Pages

`_index.md` and `content/*.md` files use standard Hugo front matter. Page body content is rendered via the corresponding layout template.

## Hugo Config (`hugo.toml`)

Key parameters available in templates via `.Site.Params`:

| Parameter | Value |
|-----------|-------|
| `companyName` | `Effective Flow` |
| `description` | `Software and consulting for people who teach and explain.` |
| `productSiteUrl` | `https://2reflect.effective-flow.com` |

## Navigation

Defined in `hugo.toml` under `[menus]`. The "2Reflect" nav item links externally to the product site and is flagged with `params.external = true` — used by the header partial to render it as an external link.

## Deployment

- Deploys to Azure SWA: `victorious-island-06ef03503`
- Workflow: `.github/workflows/deploy-company.yml`
- Path filter: changes under `sites/company/` trigger this workflow
