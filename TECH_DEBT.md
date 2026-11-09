# Technical debt

Findings from an audit of dead and unused code. Nothing here has been changed yet. Every item was verified as unreferenced (no `@use`/`@forward`, nothing in `package.json`, the workflow or `.claude/skills`). After each batch: `pnpm exec sass --verbose src/sass/main.scss > /dev/null` must stay warning-free, then rebuild both compiled CSS files.

## 1. Delete unused files
- [ ] `src/sass/_user/` (whole directory: `index.scss`, `_spacing.scss` are empty; `_colors..scss` copies the palette)
- [ ] `src/sass/utils/_measurements.scss` (unused `generate-width-classes`)
- [ ] `src/sass/components/_popup.scss` (`.popup {}`)
- [ ] `src/sass/themes/` (`_light.scss` is empty and the only file)
- [ ] `src/sass/base/_handle-classes.scss`, `src/sass/abstracts/_animations.scss` (comment-only)
- [ ] `src/sass/utils/_color-scheme.scss` and its `@use` at `main.scss:37` (outputs nothing)
- [ ] `src/sass/layout/_table.scss` and its `@use` at `main.scss:33` (only empty `table {}` / `th {}`)
- [ ] `src/index.js` (`git rm`) and the `.gitignore:3` line that lists it

## 2. Clean `main.scss`
- [ ] Remove `//@import "utils/vars"` (line 41; `_vars` already arrives through `abstracts/_variables.scss`)
- [ ] Remove `//@import "vendors/normalize"` and the `// VENDORS` header (there is no `vendors/` folder)

## 3. Unused custom properties (undocumented, safe to remove)
- [ ] `--theme`, `--spacing-between-sections`, `--jump` (`abstracts/_templates.scss`), plus the comment at `README.md:177` that lists them
- [ ] `--transition--props` (`_variables.scss:202`)
- [ ] `--plus-icon-code`, `--copy-icon-code`, `--registered-icon-code`, `--trademark-icon-code` (`_variables.scss:216-219`)
- [ ] `--footer-text`, `--highlight-text`, `--highlight-accent`, `--inner-round` (`_variables.scss`)
- [ ] `--_from-percentage`, `--_to-percentage` (`_color-palette.scss:32-33`)
- [ ] `--_switch-default-bg`, `--_switch-focus-outline` (`_switch.scss:9-10`)
- [ ] `--_font-family`, `--_font-weigth` (sic), `--_text-color` (`utils/_family.scss`)
- [ ] `--grid-min-cols` (`utils/_display.scss:38`), `--spacing-inline` (`base/_base.scss:7`)

Keep the tokens the README documents as public API: `--h-*`, `--w-*`, `--round-*`, `--font-*`, `--line-height-*`, `--gradient-*`, `--transition-*`, `--ar-*`, `--index-*`, `--border-*`, `--box-shadow*`, `--bp-*`, and so on.

## 4. Bugs found during the audit
- [ ] `abstracts/_templates.scss:35`: `--min-container-size` should be `--main-container-size`, so the `modern` template override never applies
- [ ] `components/_dropdown.scss:165`: `--_text-color` is declared but the next line reads `--text-color`
- [ ] `utils/_family.scss` `.parent.sizes` / `.parent.font`: `--spacing: var(--spacing)` and `--font-size: var(--font-size)` refer to themselves, so they are invalid at computed-value time
- [ ] `components/_general.scss` `a.scroll-to-top`: hard-coded `background-color: red` and the invalid property `behavior: smooth`. The class is unused, so fix it before adding it to any demo
- [ ] `layout/_nav.scss`: `.hamburguer-icon` is never used (also a misspelling)

## 5. Empty rule blocks
- [ ] Empty reduced-motion block in `abstracts/_preferences.scss:30-34`
- [ ] `:where(:root[data-template="roundy"]) {}` in `abstracts/_templates.scss:43`
- [ ] Empty `&:has(> input[type="checkbox"] + span:empty)` in `components/_input.scss:151-153`
- [ ] Ten empty nested `.parent` rules (`utils/_family.scss:78-125`) and `.parent.all-childs *:not(.bastard) {}` (`:146`). The flat working versions from `:151` on stay

## 6. Commented-out CSS
- [ ] About 28 single-line `//prop: value;` leftovers, for example `_base.scss:13,16`, `_general.scss:189,246`, `_modal.scss:79-80`, `_nav.scss:49,64`, `_main.scss:9,12`, `_switch.scss:17,129`, `_btn.scss:75`, `_media.scss:9`, `_hero.scss:118`, `_reset.scss:20`, `_typography.scss:109`, `_card.scss:31`, `_input.scss:102,160,218`, `_display.scss:110`
- [ ] Dead block comments: `layout/_hero.scss:43-44`, `components/_modal.scss` (~line 110), `utils/_display.scss:56-58`

## 7. `package.json`
- [ ] Keep only `sass`, `postcss`, `postcss-cli` and `autoprefixer` in `devDependencies`. The other 16 (`anymatch`, `binary-extensions`, `braces`, `chokidar`, `fill-range`, `glob-parent`, `immutable`, `is-binary-path`, `is-extglob`, `is-glob`, `is-number`, `normalize-path`, `picomatch`, `readdirp`, `source-map-js`, `to-regex-range`) are transitive. `immutable@^4` even installs a second copy next to the one `sass` needs
- [ ] Run `pnpm install` to refresh `pnpm-lock.yaml` (this also triggers the build-css workflow)

## 8. Assets
- [ ] `src/aseets/img/yonaka.jpg` is 5184x2916 and 1.27 MB, and it ships in the npm package. Resize and compress it (the showcase uses it as a 8vmin logo and a chip avatar). No image tool was available when the audit ran
- [ ] The icons in `src/aseets/icon/` are referenced nowhere (the Sass uses inline data-URI SVGs). They ship in npm and could be linked through jsDelivr, so deleting them is a judgment call
- [ ] The `aseets` typo is kept on purpose to avoid breaking paths

## 9. Not yet demoed in `index.html`
Defined in Sass but without a showcase example: hero variants (`.hero`, `.hero-shade`, `.hero-blur`, `.hero-fade`), `.floating-nav`, `.separator`, `.dotted-grid`, `.custom-gradient`, `.text-align-*`, the `.heritage-*` / `data-heritage` utilities, `data-template="modern|classic|roundy"`, and a table. Also still open: a copyable code snippet under each demo and a template switcher next to the theme toggle.

## 10. Docs to update once the cleanup lands
- [ ] `CLAUDE.md`: the "Gotchas" list, the `_templates` / `_preferences` bullets and the `src/index.js` mention
- [ ] `README.md:177`
