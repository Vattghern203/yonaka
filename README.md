# Yonaka

[English](README.md) | [Português](README.pt-BR.md)

Yonaka is a flexible and highly customizable CSS framework with a wide range of presets. It is designed to cater to developers of all skill levels, providing an intuitive way to style elements without the need for additional tools like PostCSS or JavaScript.

## Features

- Easily customizable elements
- Rich collection of presets
- No reliance on PostCSS or JavaScript for customization
- Dependency free

## Contents

- [Getting Started](#getting-started)
- [Customizing](#customizing)
- [Components](#components)
- [Utilities](#utilities)
- [Theming](#theming)
- [Development](#development)
- [Browser support](#browser-support)
- [License](#license)

## Getting Started

To get started with Yonaka, follow these steps:

### Installation

#### jsDelivr

1. Go to the [jsDelivr](https://www.jsdelivr.com/package/npm/yonaka) website
2. Copy the HTML tag or just the URL
3. Add it to your code

* HTML
  ```html
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/yonaka/dist/yonaka.css" /> <!--jsDelivr here, on top of the personal CSS-->
    <link rel="stylesheet" href="src/styles/personal.css" /> <!--Personal CSS below here-->
    <title>Cool Example 😎</title>
  </head>
  ```

* CSS

  ```css
  @import url("https://cdn.jsdelivr.net/npm/yonaka/dist/yonaka.css");

  /*Overwrite Stuff Here*/

  :root {
    --background: tomato;
  }
  ```

#### NPM

1. Run this in your terminal: ```npm i yonaka```
* If you want to see what you will download go to [NPM](https://www.npmjs.com/package/yonaka)

2. Import Yonaka in your code (same as the jsDelivr option)

* HTML

  ```html
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link rel="stylesheet" href="node_modules/yonaka/dist/yonaka.css" /> <!--Yonaka here, on top of the personal CSS-->
    <link rel="stylesheet" href="src/styles/personal.css" /> <!--Personal CSS below here-->
    <title>Cool Example 2 😎</title>
  </head>
  ```

* CSS

  ```css
  @import url("node_modules/yonaka/dist/yonaka.css");

  /*Overwrite Stuff Here*/

  :root {
    --background: rebeccapurple;
  }
  ```

**Note:** remember to follow the cascade if you want to rewrite some styling.

### Requirements

Your HTML only need to follow this structure:

```html
<body>
  <header>
    <nav></nav>
  </header>

  <!--If you want to have a hero section, put it between the header and the main tag-->

  <section class="hero"></section>

  <main></main>

  <footer></footer>
</body>
```

### Default Usage

You can use the framework as a normal HTML, but it enforces semantic usage, some examples:

1. Use sections inside the main tag to create blocks of content.

```html
<body>
  <header></header>

  <section class="hero"></section>

  <main>
    <section>
      <h2>Title</h2>

      <p>Lorem</p>
    </section>

    <section>
      <h2>Title 2</h2>

      <p>Lorem 2</p>
    </section>
  </main>

  <footer></footer>
</body>
```

2. Use displays to hold content when needed.
  - `.wrapper` for no styling
  - `.row` for a flex row
  - `.col` for a flex column

[Editable Template](https://codepen.io/Vattghern203/pen/abXxQzV)

## Customizing

Since it's designed to be flexible and accessible by any level of knowledge, there's several ways to make the framework looks as you please.

### Design System Variables

Basically all the styles are dependent of each other. Ex: the base variable, creates the measurements, that creates the spacings and etc... So one change in this flow, changes everything else.

#### Global Scoped

Some of the variables used in the project can be accessed by any element in the markup, allowing them to be rewrite for specific needs. 

```css
:where(:root, html) {
    /* GLOBAL SCOPED VARS */

    --base: 1.6rem; /* The root of the whole scale: every measurement is derived from it */
    --roundness: var(--sm); /* The border-radius of everything */
    --spacing: .8rem; /* The spacing between elements (body resets it to var(--md)) */
    --spacing-y: calc(var(--spacing) / 2);
    --spacing-x: calc(var(--spacing) * 2);
    --width: auto; /* The width of an element */
    --height: auto; /* The height of an element */

    --main-container-size: 80dvw;
    --min-layout-size: 20rem;

    /* Declared but not used by any style yet: --jump, --theme, --spacing-between-sections */

    /* SPACING VARS --------------------------------- */

    --sl: calc(var(--base) / 10);
    --3xs: calc(var(--base) / 8);
    --xxs: calc(var(--base) / 6);
    --xs: calc(var(--base) / 4);
    --sm: calc(var(--base) / 2);
    --md: var(--base); /* the default */
    --lg: calc(var(--base) * 2);
    --xl: calc(var(--base) * 4);
    --xxl: calc(var(--base) * 6);
    --3xl: calc(var(--base) * 8);
    --hg: calc(var(--base) * 10);

    /* COLOR PALETTE (Default, dark) --------------------------------- */

    --text: #d9e5f7;
    --background: #03070d;
    --primary: #173c73;
    --secondary: #081426;
    --accent: #296cd1;
    --destructive: #772626;

    /* BORDERS, OUTLINES, BOX-SHADOWS */

    --border: var(--border-sm);
    --outline: var(--outline-md);
    --box-shadow: var(--box-shadow-sm);

    /* Blend Colors */

    --blend-text-color: #000; /* Color that blend with texts */
    --blend-back-color: #FFF; /* Color that blend with bg colors */
    --blend-highlight-color: #FFF; /* Color the enhance visibility */

    /* Color Mix */

    --color-mix-method: var(--color-method-in-oklab);

    --muted-blend-intensity: 45%;
    --foreground-blend-intensity: 15%;

    /* BREAKPOINTS (reference values only: custom properties can't be used inside @media) */

    --bp-sm: 40em;
    --bp-md: 48em;
    --bp-lg: 64em;
    --bp-hg: 80em;

    /* TYPOGRAPHY --------------------------------- */

    --font-sans-serif: 'Inter', system-ui, 'Roboto', Poppins, Montserrat, 'Open Sans', Lato, Nunito, sans-serif;
    --font-weight: 400;
    --font-size: var(--md);
    --line-height: var(--line-height-relaxed); /* 1.625 */
}
```

The default theme colors live in [Theming](#theming).

#### Private Scope

There are variables that only have effect on the element itself and on its children.

You can use global scoped vars and change them.

```css
:where(:root, html) {
  --_bg: var(--background);

  --_border: var(--border); /* Using the default border from global scope */
  --border-style: dotted;
}
```

### Overwrite

- You can overwrite the default values of the variables, by simply rewriting it in the `:root` or `html` selectors. The tokens and the base styles are wrapped in `:where()`, so their specificity is 0 and any selector of yours wins. Some component selectors (`details`, `article`, `.gallery`, `header`...) are not wrapped, so they may need a more specific selector;

- Also you can customize a variable for a single tag with the inline css;

    * Ex: ```<div style="--spacing: var(--lg)">Dummy Text</div>```

- Or you can use the inheritance on the parent selector;

**Note:** the utility variables (borders, outlines, shadows, z-index, transitions, effects and aspect ratios, listed below) are declared on every element (`*`). Overriding them on `:root` doesn't reach the descendants, so set them on the target element, or with a `*` selector:

```css
:root, * {
  --border-style: dotted;
}
```

**Note:** I personally recommend creating your own stylesheet and import it below the Yonaka one in your HTML.




#### Usage and Pattern

The framework uses variables for almost everything, allowing the user to customize a big portion of the Yonaka default styling, simulating a mini design system.

I've create a pattern that works like this. 
1. I create the sub variables for example, to a border (color and style) _Experimental_

```css
--border-color: var(--accent);
--border-style: solid;
```

2. Then I created the sized 'shorthand' border variables (width, style and color, in this order), and a base one that components use

```css
--border-sm: .1rem var(--border-style) var(--border-color);
--border-md: .2rem var(--border-style) var(--border-color);

--border: var(--border-sm);
```

3. After this I can create variations by changing the value of any of the above variables in the HTML element or even in the global CSS.

```html
<section style="--border-style: dotted">
    <p>Lorem</p>
</section>
```

#### List of customizable utility variables

* some examples (_Experimental_) 👨‍🔬
* In light mode `--effect-bright-level` is meant to be `85%`, but the per-element default above currently wins below `html`.

```css
:where(:root, html, *, *::after, *::before) {

    /* OUTLINE --------------------------------------------------- */
    --offset-min: 0rem; // Minimal value possible
    --offset-sm: 1rem; 
    --offset-md: 1.25rem;
    --offset-lg: 1.50rem;
    --offset-hg: 1.75rem;

    /* Offset Base */
    --outline-offset: var(--offset-md, 1.25rem);

    /* Offset Customization */
    --outline-color: var(--accent);
    --outline-style: solid;


    --outline-sm: .1rem var(--outline-style) var(--outline-color);
    --outline-md: .2rem var(--outline-style) var(--outline-color);
    --outline-lg: .4rem var(--outline-style) var(--outline-color);

    /* Base */
    --outline: var(--outline-md);

    /* BORDER ------------------------------------------------------ */
    --border-color: var(--accent);
    --border-style: solid;

    --border-sm: .1rem var(--border-style) var(--border-color);
    --border-md: .2rem var(--border-style) var(--border-color);
    --border-lg: .4rem var(--border-style) var(--border-color);
    --border-hg: .6rem var(--border-style) var(--border-color);

    /* Base */
    --border: var(--border-sm);

    /* BOX SHADOW -------------------------------------------------- */
    /* Small variant */
    --box-shadow-xs: 0 .1rem .2rem rgba(0, 0, 0, 0.08);

    /* Regular shadow (same as the provided --box-shadow-sm) */
    --box-shadow-sm: 0 .2rem .4rem rgba(0, 0, 0, 0.1);

    /* Larger variant */
    --box-shadow-lg: 0 .4rem .8rem rgba(0, 0, 0, 0.1);

    /* Extra large variant */
    --box-shadow-xl: 0 .8rem 1.6rem rgba(0, 0, 0, 0.15);

    /* Double extra large variant */
    --box-shadow-2xl: 0 1rem 2rem rgba(0, 0, 0, 0.2);

    /* Base -------------------------- */
    --box-shadow: var(--box-shadow-sm, 0 .2rem .4rem rgba(0, 0, 0, 0.1));

    /* Z-INDEX ----------------------------------------------------- */
    --index-nav: 900;
    --index-popup: 999;
    --index-backtap: -1;
    --index-back: 20;
    --index-hidden-back: -20;

    --z-index: var(--index-back, 20);

    /* EFFECTS ----------------------------------------------------- */
    --effect-bright-level: var(--_effect-level, 150%);
    --effect-bright: brightness(var(--effect-bright-level));

    /* TRANSITIONS ------------------------------------------------- */
    --transition-props-colors: 
        background-color,
        border-color,
        color,
        fill,
        outline-color,
        text-decoration-color;
    
    --transition-props-motion: 
        transform,
        rotate,
        scale,
        zoom;
        
    --transition-props-sizes:
        height,
        max-height, 
        max-width,
        min-height,
        min-width,
        width;

    --transition-props-filter: filter, backdrop-filter;

    --transition-props-effect: opacity, box-shadow;

    --transition-props-all: all;

    --transition-props: unset;

    /* EASE CURVES -------------------------------------------- */
    --transition-ease: ease;
    --transition-ease-in: ease-in;
    --transition-linear: linear;
    --transition-ease-in-out: ease-in-out;
    
    /* Custom Easing (Cubic Bezier) */
    --transition-middle-break: cubic-bezier(0, .82, 1, .21);
    --transition-out-back: cubic-bezier(0.68, -0.6, 0.32, 1.6);
    --transition-out-circle: cubic-bezier(0.85, 0, 0.15, 1);
    --transition-friction: cubic-bezier(0, 1.46 ,1 ,-0.29);

    /* My own creation 👨‍🔬 */
    --transition-delay-in: cubic-bezier(.13, 0, 1, .13);
    --transition-jump-the-gun: cubic-bezier(.1, .65, .65, .9);
    --transition-samurai-cut: cubic-bezier(0, 1.51, 1, 1.88);
    --transition-time-reversal: cubic-bezier(0.71, 1.7, 0.76, -0.49);

    --transition-time-ssl: 2s; // Super Slow
    --transition-time-sl: .8s; // Slow
    --transition-time-md: .4s; // Medium
    --transition-time-ft: .2s; // Fast


    /* TRANSITION DELAY ------------------------------------------ */
    --transition-delay-short: .1s; /* Short delay */
    --transition-delay-normal: .3s; /* Normal delay */
    --transition-delay-long: .6s; /* Long delay */
}
```

##### Customizing colors

To customize colors, I highly recommend using [realtimecolors](https://www.realtimecolors.com/?colors=e2f7f8-092425-41cbd2-061819-2db7be&fonts=Poppins-Poppins).

1. First go the site, then generate your desired palette(HEX colors recommended).
2. Click to export and toggle the options themes and @media, copy the code.
3. Change it in the framework by overwritting it.

```css
@media (prefers-color-scheme: light) {
  :root {
    --text: #0e0e10;
    --background: #eeedf3;
    --primary: #382c58;
    --secondary: #9681cf;
    --accent: #5631b9;
  }
}
@media (prefers-color-scheme: dark) {
  :root {
    --text: #efeff1;
    --background: #0e0d13;
    --primary: #b2a6d2;
    --secondary: #45307f;
    --accent: #6a45cd;
  }
}
```

with these colors, the framework will generate variants as: muted, foreground and etc...

```css
:where(:root) {
    --muted-text: color-mix(var(--color-mix-method), var(--text), var(--blend-text-color) var(--muted-blend-intensity));

    --muted-accent: color-mix(var(--color-mix-method), var(--accent), var(--background) var(--muted-blend-intensity));

    --muted-primary: color-mix(var(--color-mix-method), var(--primary), var(--background) var(--muted-blend-intensity));

    --muted-secondary: color-mix(var(--color-mix-method), var(--secondary), var(--background) var(--muted-blend-intensity));

    --muted-destructive: color-mix(var(--color-mix-method), var(--destructive), var(--background) var(--muted-blend-intensity));

    --muted-background: color-mix(var(--color-mix-method), var(--background), var(--blend-text-color) var(--muted-blend-intensity));

    --foreground-text: color-mix(var(--color-mix-method), var(--text), var(--blend-highlight-color) var(--foreground-blend-intensity));

    --foreground-primary: color-mix(var(--color-mix-method), var(--primary), var(--text) var(--foreground-blend-intensity));

    --foreground-background: color-mix(var(--color-mix-method), var(--background), var(--text) var(--foreground-blend-intensity));

    --foreground-secondary: color-mix(var(--color-mix-method), var(--secondary), var(--text) var(--foreground-blend-intensity));

    --foreground-accent: color-mix(var(--color-mix-method), var(--accent), var(--text) var(--foreground-blend-intensity));

    --foreground-destructive: color-mix(var(--color-mix-method), var(--destructive), var(--text) var(--foreground-blend-intensity));
}
```

**Note:** If you don't liked the result you can change its behavior. 
- For blend intensity overwrite those variables ```--foreground-blend-intensity``` and ```--muted-blend-intensity```. Use percentages from 0% to 100%.

- For color interpolation methods, change the ```--color-mix-method``` for: 
 
    ```css
    /* Rectangular Space */

    --color-method-in-oklab: in oklab; /* default */
    --color-method-srgb: in srgb;

    /* Polar Space */

    --color-method-oklch: in oklch;
    --color-method-hsl: in hsl;
    ```

    * Ex: 
    ```css
    :root, html {
        --color-mix-method: var(--color-method-oklch);
    }
    ```

## Components

Yonaka has a decent amount of components as: switches, headers, navs, buttons, accordions, dropdowns and cards.

To create them, the user must follow some "rules", because the css is very specific to avoid conflict with others selectors.

**Note:** Follow the structure of the HTML or just copy it.

### Inputs

File inputs must be inside a label: the input is hidden and the label is the visible target. Color inputs also get the label layout. The other types (date, radio, checkbox, range, search, textarea...) are styled directly on the element.

### Card

```html
<article>
  <img
    src="https://images.unsplash.com/photo-1545569341-9eb8b30979d9?q=80&w=1170&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D"
    alt="a japanese landscape" loading="lazy">
  <h3>image card</h3>
  <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Iusto quas blanditiis.</p>
</article>
```

### Buttons

```html
<button class="cta">Call to Action</button>
<button class="secondary">Secondary</button>
<button class="ghost">Ghost</button>
<button class="disabled">Disabled</button>
<button class="destructive">Destructive</button>
```

### Switch

```html
<label for="input__switch">

    Default Switch

    <input type="checkbox" id="input__switch" role="switch" />
</label>
```

- class variants: ```.squished, .squared```

To use the switch component, wrap the checkbox in a label and set the role attribute equals to "switch". The `for`/`id` pair isn't needed for the styling, but keep it for accessibility.

### Accordion

```html
<details>
    <summary>Accordion</summary>

    <p>Accordion Text</p>
</details>
```

If you want the accordion to start as open, just add the open attribute to the `<details>` tag.
* Ex: 
    ```html
    <details open>
        <summary>Accordion Open</summary>
        <p>Accordion Text</p>
    </details>
    ```

### Select

```html
<select>
    <option value="" selected>Select</option>
    <option value="">option 1</option>
    <option value="">option 2</option>
    <option value="">option 3</option>
    <option value="">option 4</option>
</select>
```

I recommend using the first value as a placeholder, for this just add the selected attribute to it and write a info text to lead the user on what it does.

### Dropdown

```html
<details role="listbox">
    <summary>Dropdown</summary>

    <ul>
        <li><a href="#">item 1</a></li>
        <li><a href="#">item 2</a></li>
        <li><a href="#">item 3</a></li>
        <li><a href="#">item 4</a></li>
    </ul>
</details>
```

Same as the Accordion, use the open attribute to make it be opened at start. `role="list"` works too, with the same styles.

### Header with Nav

```html
<header class="header-sticky">
    <a href="#" role="img" aria-label="">
      <img src="https://1000logos.net/wp-content/uploads/2021/12/Akatsuki-Logo.png" alt="logo" class="logo" /> <!--the logo should have the logo class-->
    </a>

    <nav role="navigation">
      <ul>
        <li>
          <a href="#">components</a>
        </li>
        <li>
          <a href="#">examples</a>
        </li>
        <li>
          <a href="#about">about</a>
        </li>
      </ul>
    </nav>
</header>
```

- class variants: ```.header-sticky```

In this case the nav and the header are together, but you can use them separately.

### Accordion Gallery

```html
<div class="gallery">

  <figure>
    <img loading="lazy" src="https://picsum.photos/seed/japan/600/400" alt="Japan">
    <figcaption>Japan</figcaption>

  </figure>
  <figure>
    <img loading="lazy" src="https://picsum.photos/seed/china/600/400" alt="China">
    <figcaption>China</figcaption>
  </figure>

  <figure>
    <img loading="lazy" src="https://picsum.photos/seed/korea/600/400" alt="Korea">
    <figcaption>Korea</figcaption>
  </figure>

  <figure>
    <img loading="lazy" src="https://picsum.photos/seed/taiwan/600/400" alt="Taiwan">
    <figcaption>Taiwan</figcaption>
  </figure>
        
</div>
```

### Scroll Gallery(Pinterest Style)

```html
<div class="scroll-gallery">
      <!-- Existing cities -->
      <img loading="lazy" src="https://picsum.photos/seed/tokyo/600/400" alt="Tokyo">
      <img loading="lazy" src="https://picsum.photos/seed/kyoto/600/400" alt="Kyoto">
      <img loading="lazy" src="https://picsum.photos/seed/osaka/600/400" alt="Osaka">
      <img loading="lazy" src="https://picsum.photos/seed/nara/600/400" alt="Nara">
      <img loading="lazy" src="https://picsum.photos/seed/sapporo/600/400" alt="Sapporo">
      <img loading="lazy" src="https://picsum.photos/seed/hiroshima/600/400" alt="Hiroshima">
      <img loading="lazy" src="https://picsum.photos/seed/yokohama/600/400" alt="Yokohama">
      <img loading="lazy" src="https://picsum.photos/seed/fukuoka/600/400" alt="Fukuoka">
      <img loading="lazy" src="https://picsum.photos/seed/nagoya/600/400" alt="Nagoya">
      <img loading="lazy" src="https://picsum.photos/seed/kobe/600/400" alt="Kobe">
      <img loading="lazy" src="https://picsum.photos/seed/sendai/600/400" alt="Sendai">
      <img loading="lazy" src="https://picsum.photos/seed/kawasaki/600/400" alt="Kawasaki">
      <img loading="lazy" src="https://picsum.photos/seed/saitama/600/400" alt="Saitama">
      <img loading="lazy" src="https://picsum.photos/seed/okayama/600/400" alt="Okayama">
</div> 
```


You can add many more images. Lazy loading is recommended.

### Hero

```html
<div class="hero-{blur, shade or gradient}">
    <h1>Yonaka</h1>
    <p>the best framework in the world</p>

    <section>
      <button class="cta">Get Started</button>
      <button class="ghost">Go Out</button>
    </section>
</div>
```

Variables:

```css
.hero {
    --_bg-img-url: url(https://images.unsplash.com/photo-1528353518104-dbd48bee7bc4?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1332&q=80);
    --_bg-img-size: cover;
    --_bg-img-repeat: no-repeat;
    --_bg-img-pos: center;
}
```

A `div` or a `section` with the class wraps everything (`.hero` alone or one of the variants). You can pass the --_bg-img-url to change the background as you please in the inline css or in another stylesheet above in the cascade.

The hero also has `--_hero-content-pos` to place its content.

### Modal

```html
<dialog id="dialog_modal">
    <header>OPA</header>

    <p>lorem</p>

    <footer>OMG</footer>
</dialog>

  <button class="secondary" onclick="dialog_modal.showModal()">
    Modal Here
  </button>
```

The ID must match the onclick function

* tip: Avoid using kebab-case 💀

## Utilities

| Group | Classes | Notes |
| --- | --- | --- |
| Display | `.wrapper`, `.row`, `.col` | `.row` and `.col` accept `--flex-spacing` |
| Flex | `.flex-cluster`, `.flex-cluster-grow` | wrapping clusters |
| Grid | `.grid-dynamic`, `.grid-fixed` | `--grid-item-width`, `--grid-cols`, `--grid-rows`, `--grid-justify-items` |
| Scroll | `.reel` | horizontal scroller, `--grid-auto-cols` |
| Bento | `.bento`, `.small-bento`, `.big-bento`, `.dotted-grid` | |
| Text | `.text-align-{center,left,right,justify,end,start}`, `.muted`, `.foreground`, `.limited-text` | `.limited-text` clamps lines via `--_line-number` |
| Family | `.parent`, `.heritage-all`, `.heritage-appearence`, `.heritage-typography`, `.heritage-spacing`, `.heritage-colors` | or `data-heritage="all\|aspect\|typography\|spacing\|colors"` |
| Family selectors | `.direct-childs`, `.first-child-only`, `.last-child-only`, `.odd-children`, `.even-children`, `.all-first-childs`, `.all-last-childs`, `.bastard` | `.bastard` opts an element out. See `src/pages/family.html` |

More components: `span.chip` (with `data-excludable="true"`), `progress`, `.carousel`, `hr` / `.separator`, a custom scrollbar, `article.hero-card`, `a[role="button"]`, `input[type="search"]`, `textarea`, `.floating-nav` (with `data-orientation="right"`) and a hamburger side nav (`label[role="navigation"]` followed by an `aside`). The checkbox-based modal (`label[role="button"]` + `article[role="dialog"]`) works without JavaScript; `.modal-close` closes it. See `index.html` for the markup of each one.

Extra tokens: `--h-*` / `--w-*` (`full`, `half`, `third`, `quarter`, `screen`...), `--round-{sm,md,lg,full,peal}`, `--font-{serif,mono,special,handwrite,slab-serif}`, `--line-height-{tight...loose}`, `--gradient-*`, `.custom-gradient`, `--padding-block` and `--padding-inline`.

## Theming

The colors follow the OS preference (`prefers-color-scheme`). To force a theme, set `data-theme="light"` or `data-theme="dark"` on `<html>` (or on any element):

```html
<html data-theme="dark">
```

The framework also ships templates that change the scale: `<html data-template="modern">` (`--base: 2rem`) and `data-template="classic"` (`--base: 1rem`).

Default colors:

```css
@media (prefers-color-scheme: light) {
  :where(:root, html) {
    --text: #081426;
    --background: #f3f6fc;
    --primary: #8cb1e8;
    --secondary: #d9e5f7;
    --accent: #2e71d6;
  }
}

@media (prefers-color-scheme: dark) {
  :where(:root, html) {
    --text: #d9e5f7;
    --background: #03070d;
    --primary: #173c73;
    --secondary: #081426;
    --accent: #296cd1;
  }
}
```

## Development

```bash
pnpm install
pnpm exec sass src/sass/main.scss dist/yonaka.css --style=compressed   # same as build:css, then autoprefixer
pnpm run watch:sass                                                     # compiles to src/styles/yonaka.temps.css
```

The demo pages are `index.html` and `src/pages/*.html`. They link `src/styles/yonaka.temps.css` with a root-absolute path, so serve the repo root (e.g. `python3 -m http.server`) instead of opening the files directly.

## Browser support

Yonaka relies on modern CSS: `color-mix()`, `:has()`, `:where()`, `@property` and the `dvh` / `dvw` units. Use an evergreen browser.

## License

[MIT](LICENSE.md)

___

[playground](https://codepen.io/Vattghern203/pen/XWOpQgw?editors=1100)
