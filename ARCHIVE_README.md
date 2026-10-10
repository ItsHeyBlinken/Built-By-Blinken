# Archive: internal / working files (not deployed)

This branch preserves project working files that must **not** be served from the Coolify/nginx document root on `builtbyblinken.com`.

## Why this branch exists

Production pulls the GitHub default branch and serves the repository as static files via **nginx** (Coolify on a VPS). GitHub Pages is not used. Anything left on the deploy branch is publicly reachable (including `.md`, `package.json`, `.htaccess`, etc.).

## Contents (as of branch tip)

Working notes / PRDs / pricing drafts:

- `cursor_fix_pricing.md`
- `athlete_recruiting_profile_prd.md`
- `recruiting_profile_marketing_brief.md`
- `memory-bank/` (entire directory)

Archived product (unlinked from the public site; previously still served):

- `athlete-recruiting.html`
- `Recruiting-Template/`

Build / tooling / host leftovers (not site content):

- `package.json`, `package-lock.json`
- `tailwind.config.js`, `src/tailwind-input.css`
- `.htaccess` (Apache-only; inert on nginx and was downloadable)
- `.vscode/`
- `style1.css` (deprecated; unused by main pages)
- `CNAME` (GitHub Pages leftover)

## Restore a path onto a worktree

```bash
git checkout cursor/archive-internal-working-files-8ce9 -- memory-bank/
# or any other path listed above
```

Do not merge this branch into `main` unless you also change Coolify to publish only a subdirectory.
