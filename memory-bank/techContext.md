# Tech context

## Runtime

- None (static files only).

## Tooling

| Tool | Version / note |
|------|----------------|
| Node | Used locally (and optionally on CI/Coolify) for Tailwind CLI |
| `tailwindcss` | `^3.4.x` (devDependency) |
| npm scripts | `build:css`, `watch:css` |

## File map (core)

| Path | Purpose |
|------|---------|
| `index.html`, `templates.html`, `pricing.html` | Main marketing pages (deploy branch) |
| `style.css` | Home + shared patterns; `style1.css` templates; `pricing.css` pricing |
| `src/tailwind-input.css` | `@tailwind` directives for CLI |
| `tailwind-built.css` | Generated; commit for static hosts without build |
| `tailwind.config.js` | Theme extension + `content` globs |

## Standalone athlete scaffold

- Sibling path: `../Athlete-Recruiting-Profile-Template/` (outside this repository).
- Source stack: Vite 8 conventions, React, TypeScript, Tailwind CSS v4 via `@tailwindcss/vite`.
- Vite 8 Node requirement documented as Node 20.19+ or 22.12+.
- Source-only as of 2026-07-14: no dependency install, lockfile resolution, test execution, production build, Git initialization, Coolify configuration, or deployment was performed.

## External services

- Font Awesome 6.x (cdnjs).
- Google Analytics (gtag).

## Deployment notes

- **Pipeline:** GitHub repo → **Coolify** on the VPS fetches and serves static files via **nginx**. GitHub Pages is **not** part of the stack.
- **Tailwind:** commit `tailwind-built.css` on the deploy branch. Tooling (`package.json`, `tailwind.config.js`, `src/`) lives on `cursor/archive-internal-working-files-8ce9` so it is not publicly served.
- **Internal files:** do not place Memory Bank, PRDs, or archived demos on the Coolify-tracked branch; use the archive branch (see `ARCHIVE_README.md`).
