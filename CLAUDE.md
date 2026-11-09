# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Yonaka (the README still says "Akatsuki CSS") is a dependency-free, Sass-authored CSS framework published to npm (`main: dist/yonaka.css`) and served via jsDelivr. There is no JS runtime and no test or lint setup; `src/index.js` is a placeholder and is gitignored.

## Commands

Use pnpm (`pnpm-lock.yaml` is the lockfile).

- `pnpm install` — install dev dependencies (sass, postcss, autoprefixer).
- `pnpm run build:css` — compile `src/sass/main.scss` to minified `dist/yonaka.css`, then run autoprefixer over it.
- `pnpm run watch:sass` — compile `src/sass/main.scss` to `src/styles/yonaka.temps.css` in watch mode. This is the dev loop.
- `pnpm exec sass --verbose src/sass/main.scss > /dev/null` — surface every Sass deprecation warning; the build should stay warning-free.

There are no tests. Verify changes by building and opening `index.html` or `src/pages/*.html` in a browser.

## Architecture

**Single entry point.** `src/sass/main.scss` pulls in every partial with `@use`, in a fixed order: `abstracts` → `base` → `components` → `layout` → `utils`. Output order is cascade order, so a new partial must be added to `main.scss` in the right section, or it is never compiled. Partials reference each other through module namespaces (`mixins.icon(...)`, `selectors.$text-elements`), so a partial that uses a mixin or variable must `@use` its source itself.

**Design tokens are CSS custom properties, not Sass variables.** The framework is customized at runtime by overriding `:root` variables (`--background`, `--primary`, `--accent`, `--base`, `--spacing`, `--roundness`, ...), as the README shows. Sass variables exist only for selector lists (`utils/_selectors.scss`, `$hero-variations`, `$exclude-from-layout`) and the mixins in `abstracts/_mixins.scss`. Prefer adding or reusing a `--token` over a Sass variable.

Token layers, from foundation to consumer:
- `abstracts/_templates.scss` holds the root controls (`--base`, `--spacing`, `--jump`) that generate the whole scale.
- `abstracts/_variables.scss` builds the measurement scale (`--sl` ... `--3xs` ...) from `--base`. It also `@use`s `_color-palette`, `_props` and `utils/_vars`.
- `abstracts/_color-palette.scss` defines the five theme colors twice, under `prefers-color-scheme: light` and `dark`. Each block also matches `[data-theme=light|dark]`, so a manual attribute can override the OS preference.
- `abstracts/_preferences.scss` sets `color-scheme: dark light` and the per-theme blend and effect variables.

**Compiled CSS is committed.** `dist/yonaka.css(.map)` (published) and `src/styles/yonaka.temps.css(.map)` (linked by `index.html` and `src/pages/*.html`) are tracked. Rebuild both after changing Sass (`build:css` and `watch:sass` or a one-off `sass src/sass/main.scss src/styles/yonaka.temps.css`) so the committed output matches the source.

**Demo pages.** `index.html` is the full component showcase, with `src/pages/family.html` and `playground.html` for specific utilities. They are the only visual check available.

## Gotchas

- `src/sass/_user/` (`index.scss`, `_spacing.scss`, `_colors..scss`) is not imported by `main.scss` and is effectively unused. `_colors..scss` has a double dot in its name.
- `utils/_measurements.scss` and `utils/_vars.scss` are not imported from `main.scss` either (`utils/vars` is commented out there; `_vars` still reaches the build through `abstracts/_variables.scss`).
- Docs exist in English (`README.md`, `GETTINGSTARTED.md`) and Portuguese (`INSTRUCOES(PT-BR).md`); update both when changing the public customization API.
