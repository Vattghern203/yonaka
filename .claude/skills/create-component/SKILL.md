---
name: create-component
description: Create or modify a Yonaka component or utility - accessible markup patterns (ARIA, native elements), CSS-only behavior, and Sass that follows the repo's current conventions. Use when adding or changing anything under src/sass/components, layout or utils.
---

# Creating components in Yonaka

Yonaka is a dependency-free, CSS-only framework. A component is a Sass partial plus a demo in `index.html`. No JavaScript (the only exception is the one `showModal()` call that the `<dialog>` demo needs).

## 1. Pick the markup first (semantics and ARIA)

Style native elements and ARIA attributes, not invented classes. Existing components target `details`, `dialog`, `input[type="checkbox"][role="switch"]`, `label[role="button"]`, `select` and so on.

- Prefer a native element that already has the behavior: `<details>`/`<summary>` (accordion), `<dialog>` (modal), `<input type=checkbox role=switch>` (switch), `<progress>`, `<select>`.
- Add `role` and `aria-*` only where HTML doesn't already express it, and select on them (`[role="switch"]` is the pattern in use today; `[aria-busy]`, `[aria-expanded]`, `[aria-current]`, `[aria-invalid]` and `[aria-disabled]` are encouraged for new components, no existing code uses them yet).
- Keep state in attributes and pseudo-classes, so styling and accessibility stay in sync: `:checked`, `[open]`, `:disabled`, `:focus-visible`, `:user-invalid` (new, not used yet), `[aria-*]`.
- If the markup needs a hidden control for a CSS-only toggle (checkbox hack, `label[role="button"]:has(> input:checked)`), hide it with a visually-hidden technique that keeps it focusable, not `display: none`, and keep a visible `:focus-visible` style on the label. Existing code still uses `display: none` in `components/_modal.scss`, `layout/_nav.scss` and `components/_general.scss`; don't copy that.
- Honor `prefers-reduced-motion` for any transition or animation (the block in `abstracts/_preferences.scss` is empty, so put the rules there), and never convey state by color alone.

## 2. CSS-only behavior

Use the platform: `:has()`, `:is()`/`:where()`, `:checked`, `:target`, `details[open]`, `dialog::backdrop`, `::marker`, `@starting-style`, `popover`/anchor positioning where support is acceptable. Prefer `:where()` for low-specificity defaults so users can override with plain CSS, which is how the README tells people to customize.

## 3. Tokens, not literals

Customization happens at runtime through CSS custom properties.

- Read the global tokens: colors (`--text`, `--background`, `--primary`, `--secondary`, `--accent`), the scale (`--xs`, `--sm`, `--md`, `--lg`, ... generated from `--base` in `abstracts/_variables.scss`), `--spacing`, `--roundness`, `--outline-*`, `--transition-*`.
- Expose component knobs as private custom properties declared at the top of the component with a leading underscore, then consume them. Prefix them with the component name (`--_switch-w`, `--_switch-color`); some older partials use generic names (`--_bg`, `--_border`), which are fine inside a scoped selector but not preferred. Give them defaults from global tokens (`var(--md)`), not hard-coded values.
- Don't add a Sass variable for something users may want to change; add a `--token`. Sass variables are only for selector lists and mixin arguments.
- Colors come from the palette tokens so light and dark themes (`prefers-color-scheme` and `[data-theme]`) work automatically. Avoid raw hex/rgb unless it's theme-independent.
- Prefer logical properties (`padding-inline`, `margin-block`, `inset-inline-start`) and relative units (`rem`/`em`; the root is 62.5%).

## 4. Sass conventions

- Never use `@import`. Every partial starts with `@use` for what it needs, e.g. `@use "../abstracts/mixins";`, and calls members with the namespace: `@include mixins.icon(var(--expand-icon));`, `selectors.$text-elements`.
- Built-ins live in modules: `@use "sass:math"`, `sass:list`, `sass:map`, `sass:color`. No global `append`, `map-get`, `darken`, `invert`, or `rgba($color, $alpha)`; use plain CSS (`rgb(0 0 0 / .6)`, `color-mix()`, relative colors) when possible.
- Use `math.div()`, not `/`, for division.
- Nest with `&` for states and pseudo-elements, but keep nesting shallow (about 3 levels) to avoid specificity creep.
- Reuse the mixins in `abstracts/_mixins.scss` (`icon`, `icon-background`, `centered-flex`, ...) before writing new ones.

## 5. Wire it up, showcase it, document it

A component is not done until all of these exist:

1. Create `src/sass/components/_name.scss` (or `layout/`, `utils/`).
2. Add `@use "components/name";` to `src/sass/main.scss` in the matching section, alphabetically; otherwise it is never compiled.
3. **Showcase in `index.html`.** Add a demo in the relevant section (components in `#components__section`, forms in `#forms`, and so on), using the exact markup from step 1 with its ARIA attributes. Show every variant and state (default, `open`/`checked`, disabled, invalid) so the page works as the visual test.
4. **Update the docs.** Add or update a section under `## Components` in `README.md` with the markup snippet, the variants, and the `--_private` variables users can override, following the neighboring sections' format. `README.pt-BR.md` is only an install quick-start, so touch it only if the change affects setup. A component or variable that changes the public customization API must be reflected in `README.md` in the same PR.
5. Check: `pnpm exec sass --verbose src/sass/main.scss > /dev/null` must print no warnings.
6. Rebuild the committed outputs: `pnpm run build:css`, and `pnpm exec sass src/sass/main.scss src/styles/yonaka.temps.css`.
7. Open `index.html` and check keyboard operation (Tab, Space/Enter, Esc for dialogs), the visible focus ring, and both light and dark schemes.
