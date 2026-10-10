# Active context

**Highest-priority Memory Bank file for “what matters now.”** If other files disagree, prefer **activeContext** → **progress** → the rest.

## Current stack (frontend)

- Static HTML + hand-authored CSS.
- **Tailwind CSS v3** compiled to `tailwind-built.css` (not the CDN in production).
- Build: `npm run build:css` from repo root; input `src/tailwind-input.css`, output `tailwind-built.css`.
- `tailwind.config.js` (on this archive branch) scans main HTML pages for class names; restore from archive before rebuilding CSS on the deploy branch.
- **Display serif:** Fraunces (Google Fonts) used for hero / section headings via the `.font-display` utility (extended in `tailwind.config.js` `fontFamily.display`); Inter remains the default body / sans family.

## Agency design system (added 2026-05-05)

A shared set of tokens and patterns lives in `style.css` so all four main pages share the same visual language:

- `.eyebrow` / `.eyebrow-center` — small-caps tracked label with leading bar, used above every section title.
- `.font-display` — Fraunces serif heading class (also exposed as a Tailwind utility).
- `.section-index` — oversized faint digit (used optionally for "01 / 02 / 03" feel).
- `.bg-gradient-soft` — radial-gradient backdrop for hero / feature panels.
- `.industry-pill` — pill-row component for industries served on the homepage.
- `.stat-block` / `.stat-number` / `.stat-label` — agency-style stats bar.
- `.btn-cta` (solid) and `.btn-ghost` (outlined) — primary agency CTAs (used alongside the existing `.btn-primary` in `pricing.css`).
- `.differentiator-card` / `.differentiator-icon` — "why work with us" cards.
- `.process-timeline` / `.process-step` — process row with desktop connector line.
- `.work-card` family — featured-templates / portfolio cards on homepage.
- `.hero-stack` + `.hero-stack-card.{card-back,card-mid,card-front}` — CSS-only layered template stack for the homepage hero.
- `.compare-table` family — pricing comparison table (lives in `#website-design` section on `pricing.html`).
- `.filter-btn` (with `.filter-count`) and `.template-card-chip` — segmented filter bar + always-visible category chip on `templates.html`.

`templates.html` uses `style.css` as its primary stylesheet. Deprecated `style1.css` lives only on the archive branch.

## Deployment

- **GitHub:** repository is the **source of truth** for files (push commits here).
- **Coolify (VPS):** pulls from the GitHub repo and serves the site — **not GitHub Pages.** Flow: push to GitHub → Coolify fetches/builds or deploys as configured. Live responses are **nginx** (so root `.htaccess` is not applied and was publicly downloadable until removed).
- **Deploy hygiene:** Coolify serves the repo document root. Internal notes, Memory Bank, PRDs, npm/Tailwind tooling, and archived athlete demo files must stay on `cursor/archive-internal-working-files-8ce9` (or another non-deployed ref), not on the branch Coolify tracks.
- Deploys verified with **no Tailwind CDN console warnings** in the browser.
- Tailwind rebuild: restore `package.json`, `tailwind.config.js`, and `src/tailwind-input.css` from the archive branch into a local worktree, run `npm run build:css`, commit `tailwind-built.css` on the deploy branch.

## Athlete recruiting — archived off deploy branch (2026-10-10)

- Not part of the public agency offer. Do not link it from Home, Templates, or Pricing.
- Files live only on branch `cursor/archive-internal-working-files-8ce9` (`athlete-recruiting.html`, `Recruiting-Template/`), not on the Coolify-deployed branch.
- Sibling scaffold `../Athlete-Recruiting-Profile-Template/` remains outside this repo and is unused.

## Conventions worth preserving

- Semantic headings: e.g. `h1` with ids (`home-heading`, `templates-heading`, `pricing-heading`) for `aria-labelledby` where used.
- Hero `h1`s use `.font-display` (Fraunces) at large sizes; section `h2`s use `.font-display` with an `.eyebrow` label above them.
- Custom theme colors and fonts live in `tailwind.config.js` (`primary`, `secondary`, `accent`, `highlight`, `muted`, `light`, Inter for `sans`, Fraunces for `display`).
- Link order: page-specific CSS first (`style.css` and any page-specific like `pricing.css`), then `tailwind-built.css`, then Font Awesome CDN.

## Open / watch

- Athlete page CSS leftovers may still exist in `style.css` on the deploy branch; the HTML was moved to the archive branch.
- **`pricing.html` (2026-09-10 pivot):** Primary and only offer is **Website Starter — $250 one-time setup + $50/month**. The monthly fee covers hosting, SSL, maintenance, technical support, and small content updates (hours, phone, service copy, a few images). New pages, features, redesigns, e-commerce, and ongoing SEO campaigns are quoted separately. Launch / Growth / Signature, Site Care, activation bundles, commerce packages, and Athlete profiles were removed from the public site. Primary CTA is **Let's Build Your Site** → `mailto:services@bytesbyblinken.com`. Keep visible copy and JSON-LD aligned when this offer changes.
- After HTML edits that add or change Tailwind classes, run **`npm run build:css`** and commit `tailwind-built.css` if not using a CI build step. The 2026-07-14 athlete launch intentionally deferred this manual build, so generated CSS still needs regeneration before release.
- Adding new top-level HTML pages that use Tailwind requires adding them to `content` in `tailwind.config.js` and rebuilding.
- Homepage `Recent work` section links to **3 specific live demos** under `Site Templates/`: `Pixel Perfect`, `5 Real Estate`, and `4 Landscaping` (GreenThumb). Retail/e-commerce templates (Vinyl Vault, ShopSmart) are archived in `Site Templates/` but not shown on Templates or Home. That section is `text-left` so it is not centered by the global `main { text-align: center }` rule in `style.css`.
- `.font-display` includes `word-spacing: 0.18em` and `.eyebrow` includes `word-spacing: 0.35em` so Fraunces / tracked labels keep visible gaps between words.
- **Testimonials with named clients are NOT in use** on the homepage. The block has been replaced with a generic "How clients experience us" / social-proof block. Do not re-introduce invented client names; if real testimonials become available, add them with proper attribution and re-enable the block intentionally.
