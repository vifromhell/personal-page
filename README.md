# Vitaliy portfolio prototype

A static, responsive portfolio prototype based on the current Notion page structure.

## Open locally

Double-click `index.html`. It works directly from a folder; no local server is required.

Google Fonts are loaded from the internet:
- IBM Plex Sans
- IBM Plex Mono

If you are offline, the page falls back to Arial / system monospace.

## Responsive model

Primary design frames:
- Desktop: 1440 px
- Mobile: 390 px

Implementation ranges:
- `< 768`: mobile
- `768–1199`: compact/tablet
- `1200–1599`: desktop
- `1600+`: wide

The layout is fluid inside these ranges rather than being tied to specific devices.

## Visual direction

- Monochrome UI
- Warm paper-like background
- Color reserved for future case-study images
- Editorial / technical-document structure
- Persistent side labels on desktop
- Side labels become section headers on mobile
- Thin rules and restrained UI rather than cards/shadows

## Notion integration: next step

Do **not** call Notion directly from browser JavaScript with an API token.

Recommended production architecture:

Notion → build-time sync script → local JSON/content → static site

This keeps the Notion token private and means the public site has no runtime dependency on Notion.

A later version can add:
- `content/site.json`
- `content/cases/*.json`
- `scripts/sync-notion.mjs`
- a build step that maps Notion blocks into site components

The current prototype intentionally keeps content in HTML so the visual system can be reviewed before we commit to a content schema.
