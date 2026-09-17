# Project context

## Purpose and audience

This is Vitaliy Kapustyanov's personal portfolio site. It presents him as a Design System Designer who brings structure to complex digital products. The primary audience is hiring managers, design leaders, product leaders, engineers, and potential collaborators evaluating his design-systems experience, systems thinking, and visual craft.

The site should communicate clarity, credibility, seniority, and an ability to turn fragmented interfaces, libraries, and workflows into coherent systems.

## Current page structure

The current site contains a portfolio home page, thirteen local case-study pages, and one local visual-archive page.

The home page contains:

1. Header with name and anchor navigation.
2. Intro/hero with positioning, value proposition, experience, and location.
3. Selected design-systems work with nine case-study previews.
4. Product Design Background with four earlier product-work previews.
5. Capabilities under “What I bring.”
6. Experience timeline/list.
7. Recommendations.
8. Additional links for mentoring, visual experiments, and a downloadable CV.
9. Contact call to action.
10. Footer.

Each case-study page contains a case hero, project metadata, editorial content sections with persistent side labels, local project imagery, a next-case link, and navigation back to the relevant work section. Case covers are used in homepage cards but are not repeated inside the case pages. Case headers show Back, the portfolio name, and Work; they do not expose or mention the underlying content source.

## Visual direction

- Monochrome, restrained interface.
- Warm paper-like background rather than pure white.
- Editorial and technical-document character.
- Consistent 1 px rules, open space, and strong typography instead of cards, shadows, or decorative UI.
- All structural dividers and borders use the shared `--line` color token; hierarchy should not depend on darker one-off rules.
- All case-card preview frames use a shared 3:2 aspect ratio with cover cropping for a consistent grid across design-system and product-design work.
- Case cards use one shared framed construction: a 1 px outer border, a bordered image/content boundary, a padded text area, and a bottom-aligned 64 px metadata area with a horizontal divider and space reserved for exactly two lines of thematic tags. Titles and descriptions stay top-aligned, allowing shorter content to create additional whitespace before the shared metadata baseline.
- Color is reserved for future case-study imagery and should not become general interface decoration without an explicit design decision.
- Persistent side labels describe the information type (for example CONTEXT, CHALLENGE, DECISION, EXECUTION, IMPACT) instead of repeating the adjacent editorial heading; on mobile they become horizontal section headers.
- The design should feel systematic and precise while remaining personal and readable.

## References

The current site and its established visual system remain the primary design reference. [Uchechi Divine's portfolio](https://www.uchechidivine.com/#projects) is a secondary compositional reference: use it selectively when a page or case needs more variety, never as a replacement visual direction.

Compatible ideas to adapt include:

- alternating dense and spacious content sections to improve narrative pacing;
- varying image scale and grouping within the existing editorial grid;
- compact project summaries, outcome metrics, highlights, and related-case transitions;
- progressive disclosure when it keeps overview pages easy to scan;
- controlled asymmetry that still aligns to the site's established columns and measures.

Do not copy the reference's branding, palette, typography, decorative language, motion, or component construction. Any borrowed composition must be translated into this site's monochrome palette, IBM Plex typography, 1 px rule system, spacing grid, persistent side-label logic, and responsive behavior. A local experiment must not trigger an unrelated global redesign, and the reference must not dilute the current restrained editorial and technical-document character.

## Responsive targets

The primary review frames are:

- Desktop: 1440 px wide.
- Mobile: 390 px wide.

Current implementation ranges:

- Below 768 px: mobile layout.
- Editorial diagrams that require art direction use `<picture>` with dedicated mobile compositions below 768 px; desktop sources remain unchanged at 768 px and above.
- 768–1199 px: compact/tablet layout.
- 1200–1599 px: desktop layout.
- 1600 px and above: wide layout.

The layout is fluid inside these ranges. It should not be optimized for only two fixed screenshots. Preserve readable line lengths, hierarchy, spacing, and functional navigation at intermediate widths.

## Typography and layout principles

- IBM Plex Sans is the primary interface and editorial typeface.
- IBM Plex Mono is used for navigation, labels, dates, and technical accents. Case metadata is split into small uppercase mono labels and larger mixed-case IBM Plex Sans Medium values, using a wider 1100 px measure and a larger third column for Scope, Team, or Outcome values.
- Arial and system monospace are the offline fallbacks.
- Large headings use compact line-height and negative letter-spacing.
- Font sizes and spatial values follow a 4 px base grid. Very small functional values may use a 2 px step, while spatial values above 48 px use an 8 px step.
- Case-study body copy uses an approximately 800 px measure, while section headings, subheadings, and blockquotes use a closely related 860 px measure. This keeps text readable while maintaining a calm shared right edge.
- Desktop sections use a two-column grid: a narrow label column and a flexible content column.
- Editorial figures align to the main content column and never extend into the persistent side-label column; on mobile they use the full available width.
- Every case has a dedicated cover used by its homepage card. Cover assets remain separate from editorial figures and are not repeated inside the case-study page.
- Interface arrows and disclosure indicators use Material Symbols Sharp with fill 0, weight 300, grade 100, and optical size 32. Hover and keyboard focus underline only the link text, never the icon.
- Spacing and type sizes use fluid `clamp()` values where appropriate.
- Layout hierarchy should come from typography, spacing, alignment, and rules—not ornamental effects.
- Maintain semantic HTML, keyboard-accessible links, and sensible document hierarchy.

## Notion as the content source

Notion is the intended long-term source for portfolio content. The identifiers currently known to the project are stored in `notion-content-map.json`.

Never call the Notion API directly from browser JavaScript with a secret token. The intended production flow is:

`Notion → build-time sync → local structured content → static site`

Credentials must live in environment variables or another uncommitted secret store. They must never be added to HTML, client-side JavaScript, JSON content maps, or Git history.

The likely future structure may include:

- `content/site.json`
- `content/cases/*.json`
- `scripts/sync-notion.mjs`
- A build step that maps Notion blocks to site components.

This structure is a direction, not an implemented contract. Define the content schema deliberately before adding it.

## Current architecture

The project is intentionally small and dependency-free:

- `index.html` contains the portfolio home page.
- `cases/*.html` contains thirteen local case-study detail pages—nine design-system cases and four earlier product-design cases—plus the Visual experiments archive.
- `styles.css` contains shared design tokens, home-page layout, typography, components, and responsive rules.
- `case-study.css` extends the shared styles for long-form case-study layouts.
- `assets/cases/*` contains design-system case imagery transferred from Notion and referenced locally.
- `assets/product-work/*` contains cover images for the Product Design Background cards.
- `assets/visual-experiments/*` contains the illustration, drawing, graphic-design, and photography archive transferred from Notion.
- `notion-content-map.json` records Notion page/data-source identifiers without credentials.
- `CNAME` binds GitHub Pages to `kapustianov.com`; `sitemap.xml` and `robots.txt` expose the canonical public URLs to crawlers.
- `README.md` explains local use, responsive ranges, visual direction, and the proposed Notion integration.
- IBM Plex and an icon-name-subset of Material Symbols Sharp are loaded remotely from Google Fonts; the site otherwise opens directly from the filesystem and requires no local server or build tooling.

## What is already implemented

- Complete one-page portfolio layout.
- Responsive desktop, compact/tablet, and mobile behavior.
- Anchor navigation to Work, About, Experience, and Contact.
- Desktop sticky side labels and mobile section-header conversion.
- Hero positioning and professional metadata.
- Selected design-system work is presented as a responsive three-column desktop grid with six featured case studies, including four current Muse system cases; two additional case studies are available through progressive disclosure, while the research case remains available by direct link but is not featured on the homepage. Each card omits company-name eyebrows and includes one 14 px plain-text metadata line of short thematic tags describing the work, platforms, and methods without repeating quantitative case details.
- Product Design Background is presented as a responsive four-card grid sourced from the Earlier Product Work database in Notion, with a local long-form page for every project. Its cards use the same bottom-aligned thematic-tag pattern as the design-system work instead of dates or company metadata.
- Responsive long-form pages for Muse accessibility, multi-product Design System scaling, the Muse icon system, Muse semantic color architecture, the Cian icon system, Cian semantic color system, cross-platform contact system, design-system product analysis, scalable design ecosystem, veterinary ophthalmology tablet app, THRIVE Vet Care mobile app, CRM underwriting system, and fintech Android app.
- Full case content and supporting images transferred from Notion into semantic HTML and local assets.
- Capabilities, experience, four full-length recommendations sourced from Notion, mentoring, a local Visual experiments archive, a downloadable CV, contact, and footer content. Recommendations form a compact three-column desktop row of selected excerpts using 18–22 px regular text, with larger author names and roles; they stack vertically below 1200 px. A native disclosure below the row reveals the complete text, author, role, and working relationship for all four recommendations without JavaScript.
- CSS custom properties for the core palette, dimensions, and spacing.
- Notion source identifiers separated into a dedicated mapping file.

## Current placeholders

- Notion synchronization and a structured local content layer are not implemented; the current content was transferred manually.
- There is no build pipeline or client-side application framework. The static site is deployed through GitHub Pages with `kapustianov.com` as its canonical domain.

## Rules for further development

1. Read `AGENTS.md` and this file before doing any work.
2. Preserve the existing visual concept unless the user explicitly requests a redesign.
3. Treat 1440 px and 390 px as required review widths, while maintaining fluid behavior between them.
4. Keep the interface monochrome unless approved case imagery or an explicit visual change calls for color.
5. Preserve the side-label system and its mobile transformation unless explicitly directed otherwise.
6. Prefer semantic, accessible, dependency-free HTML and CSS for changes that do not require tooling.
7. Do not add a framework, package manager, build system, or third-party dependency without a concrete need.
8. Keep content, presentation, and external-source mapping separate.
9. Keep secrets out of the repository and out of browser-delivered code.
10. Clearly label placeholder content and do not present invented content as final.
11. Update this document when an approved decision changes the architecture, visual direction, content model, or project status.
12. Do not commit or push unless the user gives a separate, explicit instruction.
