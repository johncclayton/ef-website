# 2Reflect Site — Agent Guide

## Purpose

The **2Reflect** product landing page at `2reflect.effective-flow.com`. Audience: teachers and presenters looking for a Windows tool to annotate over any shared screen.

**Tagline:** "Teach like it's real on any shared screen"

## Tone

Product marketing — benefit-led, concise, action-oriented. Speak directly to the user's teaching/presenting pain points. Avoid technical implementation details.

## Site Structure

```
sites/2reflect/
├── assets/css/site.css       # Styles — also duplicated in sites/company/
├── content/
│   ├── _index.md             # Landing page front matter / content
│   └── privacy-policy.md     # Privacy policy (required for Windows Store)
├── layouts/
│   ├── index.html            # Main landing page template (hero, features, CTAs)
│   ├── _default/
│   │   ├── baseof.html       # Base template wrapping all pages
│   │   ├── list.html
│   │   └── single.html       # Used for privacy policy page
│   └── partials/
│       ├── header.html
│       └── footer.html
└── hugo.toml
```

## Layout vs Content

This is primarily a **template-driven** site. The landing page content (hero text, feature descriptions, CTAs) lives in `layouts/index.html`, not in `content/_index.md`. When updating landing page copy, edit the layout template directly.

The `content/privacy-policy.md` is a standard content file rendered via `single.html`.

## Hugo Config (`hugo.toml`)

Key parameters available in templates via `.Site.Params`:

| Parameter | Value |
|-----------|-------|
| `productName` | `2Reflect` |
| `productTagline` | `Teach like it's real on any shared screen` |
| `windowsStoreUrl` | `https://www.microsoft.com/store/apps/windows` |
| `companySiteUrl` | `https://effective-flow.ch` |

**Do not change `windowsStoreUrl`** without first verifying the correct store listing URL.

## Privacy Policy

`content/privacy-policy.md` exists to satisfy Windows Store requirements. Any changes must remain accurate and compliant — treat it with care and do not remove it.

## Navigation

The "Effective Flow" nav item links externally to the company site and is flagged with `params.external = true`. Do not remove this cross-link.

## Deployment

- Deploys to Azure SWA: `agreeable-stone-0fdc8de03`
- Workflow: `.github/workflows/deploy-2reflect.yml`
- Path filter: changes under `sites/2reflect/` trigger this workflow
