# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Yonaka (formerly "Akatsuki CSS"; the old name may linger in demo pages) is a dependency-free, Sass-authored CSS framework published to npm (`main: dist/yonaka.css`) and served via jsDelivr. There is no JS runtime and no test or lint setup; `src/index.js` is a placeholder (`console.log`) that is tracked in git despite being in `.gitignore`.

## Commands

Use pnpm (`pnpm-lock.yaml` is the lockfile). `package-lock.json` is stale and the `version:*` scripts still call npm; ignore both. `pnpm run` may try to reinstall and fail on an ignored build script (`@parcel/watcher`); if so, call the binaries directly (`node_modules/.bin/sass`, `node_modules/.bin/postcss`).

- `pnpm install` — install dev dependencies (sass, postcss, autoprefixer).
- `pnpm run build:css` — compile `src/sass/main.scss` to minified `dist/yonaka.css`, then run autoprefixer over it.
- `pnpm run watch:sass` — compile `src/sass/main.scss` to `src/styles/yonaka.temps.css` in watch mode. This is the dev loop.
- `pnpm exec sass --verbose src/sass/main.scss > /dev/null` — surface every Sass deprecation warning. Today it prints 29 known ones (28 `@import` deprecations plus the global `invert()` in `base/_reset.scss`); don't add new ones.

There are no tests. Verify changes by building and opening `index.html` or `src/pages/*.html` in a browser. Serve the repo root (e.g. `python3 -m http.server`), because `family.html` links the CSS with a root-absolute path. The demos use no JS except one `showModal()` `onclick` in the modal demo.

## Architecture

**Single entry point.** `src/sass/main.scss` pulls in every partial with `@import` (a migration to `@use` is pending), in a fixed order: `abstracts` → `base` → `components` → `layout` → `utils`. Output order is cascade order, so a new partial must be added to `main.scss` in the right section, or it is never compiled. Because of `@import`, everything shares one global scope: partials call `icon(...)` and use `$text-elements` without a namespace, relying on `abstracts/mixins` being imported first. Some partials still have a leftover `@use "../abstracts/mixins"` that does nothing. Adding `@use "components/name"` to `main.scss` fails (`@use` must come before other rules).

**Design tokens are CSS custom properties, not Sass variables.** The framework is customized at runtime by overriding `:root` variables (`--background`, `--primary`, `--accent`, `--base`, `--spacing`, `--roundness`, ...), as the README shows. Sass variables exist mainly for selector lists and loops (`utils/_selectors.scss`, `$hero-variations`, `$exclude-from-layout`, `$dropdown`, `$text-aligns`) and the mixins in `abstracts/_mixins.scss`. Prefer adding or reusing a `--token` over a Sass variable.

Token layers, from foundation to consumer:
- `abstracts/_templates.scss` holds the root controls (`--base`, `--spacing`) that generate the whole scale. `--jump`, `--theme` and `--spacing-between-sections` are declared but nothing reads them.
- `abstracts/_variables.scss` builds the measurement scale (`--sl` ... `--3xs` ...) from `--base`. It also `@use`s `_color-palette`, `_props`, `_templates` and `utils/_vars`.
- `abstracts/_color-palette.scss` defines the five theme colors for `prefers-color-scheme: light` and `dark`, then again under `:where([data-theme=light|dark])` declared after the media queries, so a manual attribute overrides the OS preference.
- `abstracts/_preferences.scss` sets `color-scheme: dark light` and light-theme overrides for the blend and effect variables (there is no dark block; dark uses the defaults in `_variables.scss`). Its reduced-motion block is empty.

**Compiled CSS is committed.** `dist/yonaka.css(.map)` (published) and `src/styles/yonaka.temps.css(.map)` (linked by `index.html` and `src/pages/*.html`) are tracked. Rebuild both after changing Sass (`build:css` and `watch:sass` or a one-off `sass src/sass/main.scss src/styles/yonaka.temps.css`) so the committed output matches the source.

**Demo pages.** `index.html` is the full component showcase, with `src/pages/family.html` and `playground.html` for specific utilities. They are the only visual check available.

## Gotchas

- `src/sass/_user/` (`index.scss`, `_spacing.scss`, `_colors..scss`) is not imported by `main.scss` and is effectively unused. `_colors..scss` has a double dot in its name.
- `utils/_measurements.scss` and `utils/_vars.scss` are not imported from `main.scss` either (`utils/vars` is commented out there; `_vars` still reaches the build through `abstracts/_variables.scss`).
- Utility vars (`utils/_vars.scss`: borders, outlines, shadows, z-index, transitions, aspect ratios) are declared on `:where(:root, html, *, ...)`, so overriding them on `:root` doesn't reach descendants.
- Empty or never-imported partials: `components/_popup.scss`, `themes/_light.scss`, `base/_handle-classes.scss`, `abstracts/_animations.scss`. `utils/_color-scheme.scss` is imported but only holds a comment.
- `src/aseets/` (sic) holds the icons and the demo image and ships in the npm package; the typo is kept to avoid breaking paths.
- Docs: `README.md` is the full documentation; `README.pt-BR.md` is a short Portuguese quick-start (intro and install only). Update `README.md` when changing the public customization API, and `README.pt-BR.md` only if install or setup changes.
