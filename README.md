# virgola_brand_assets

Canonical source for Virgola brand assets shared across apps (virgola.co.nz,
seo_manager, ...): favicon/logo mark and the `theme.css` design tokens.

## Contents

- `icons/mark.svg` — the "V," logo mark (SVG source)
- `icons/favicon.ico` — multi-res favicon
- `icons/icon-512.png` — 512×512 raster icon (apple-touch-icon etc.)
- `theme.css` — shared color/font tokens + component classes (Tailwind `@theme`)

## Using this in an app

Add as a git submodule at `vendor/virgola-brand`:

```bash
git submodule add https://github.com/Virgola-Limited/virgola_brand_assets.git vendor/virgola-brand
```

Each consuming app has its own `bin/sync-brand-assets` (or `bin/sync_brand_assets`)
script that runs `git submodule update --init --remote` then copies the files
to that app's expected paths/filenames (naming conventions differ per app —
e.g. `favicon.svg` vs `icon.svg`). It's a manual dev-time tool, not a build
step: the copied files are committed as plain files in each app, so builds
and deploys never depend on git/network access to this submodule (handy since
CI/Docker build contexts often exclude `.git`, and third-party build platforms
don't always recurse submodules on checkout).

To pick up a brand update in a consuming app:

```bash
bin/sync-brand-assets   # or bin/sync_brand_assets — pulls latest + copies files
git add -A && git commit -m "chore: sync brand assets"
```

## Editing brand assets

Edit files here, commit, push. Then bump each consuming app as above.
