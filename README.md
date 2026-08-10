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
e.g. `favicon.svg` vs `icon.svg`). Run it locally after pulling, and it also
runs automatically as part of the app's build (npm `prebuild` hook / Dockerfile
`RUN` step) so deploys never depend on the host platform's git-submodule
support.

To pick up a brand update in a consuming app:

```bash
git submodule update --remote vendor/virgola-brand
bin/sync-brand-assets   # or bin/sync_brand_assets
git add -A && git commit -m "chore: sync brand assets"
```

## Editing brand assets

Edit files here, commit, push. Then bump each consuming app as above.
