# Akatsuki CSS

Akatsuki CSS is a flexible and highly customizable CSS framework with a wide range of presets. It is designed to cater to developers of all skill levels, providing an intuitive way to style elements without the need for additional tools like PostCSS or JavaScript.

## Features

- Easily customizable elements
- Rich collection of presets
- No reliance on PostCSS or JavaScript for customization
- Dependency free

## Getting Started

To get started with Akatsuki-CSS, follow these steps:

1. [Download](https://www.npmjs.com/package/yonaka) on NPM, clone the repository or use the [Jsdelivr](https://www.jsdelivr.com/package/npm/yonaka).

2. Add the `akatsuki.css` file to your project by importing it on your global CSS file.
```css
@import "node_modules/akatsuki-css/akatsuki.css"
```

or in the HTML

```html
<link rel="stylesheet" href="node_modules/akatsuki-css/akatsuki.css" />
```

**Note:** remember to follow the cascade if you want to rewrite some styling.

## Customizing

- You can overwrite the default values of the variables, by simpling rewriting it in the `:root` or `html` selectors. The default specifity for almost all styles is equals to 0;

- Also you can customize a variable for a single tag with the inline css;

    * Ex: ```<div style="--spacing: var(--lg)">Dummy Text</div>```

- Or you can use the inheritance on the parent selector;

**Note=** I personally recommend creating your own stylesheet and import it below the Akatsuki one in your HTML.


### Global Scoped Variables

#### Overview

Some of the variables used in the project can be accessed by any element in the markup, allowing them to be rewrite for specific needs. 

```css
:where(:root) {
    // GLOBAL SCOPED VARS

    --roundness: auto; // The border-radius to everything
    --spacing: .8rem; // the spacing between elements
    --spacing-y: auto;
    --spacing-x: auto;
    --jump: .4rem; // the jump value between elements
    --theme: dark; // the actual theme in the page
    --width: auto; // the witdth of an element
    --height: auto; // the height of an element

    // SPACING VARS ---------------------------------

    --xxs: .2rem;  //  0.5 Extra Extra Small
    --xs: .4rem;   //  1.0 Extra Small
    --sm: .8rem;   //  2.0 Small
    --md: 1.6rem;  //  4.0 Medium
    --lg: 3.2rem;  //  6.0 Large
    --xl: 6.4rem;  //  8.0 Extra Large
    --hg: 12.8rem; //  10.0 Huge

    // COLOR PALETTE ---------------------------------

    --text: #d9e5f7;
    --background: #03070d;
    --primary: #173c73;
    --secondary: #081426;
    --accent: #296cd1;

    // Color created with the palette

    --destructive: #772626;

    // Blend Colors

    --blend-text-color: #000;
    --blend-back-color: #FFF;
    --blend-highlight-color: #FFF;

    
    // BREAKPOINTS ---------------------------------

    --bp-sm: 40em;
    --bp-md: 48em;
    --bp-lg: 64em;
    --bp-hg: 80em;

    // TYPOGRAPHY ---------------------------------

    --font-family: system-ui, 'Inter', 'Roboto';
    --font-weight: 400;
    --font-size: 1.6rem;
    --line-height: 1.15;

}

// LIGHT THEME

[data-theme="light"] {
    --text: #081426;
    --background: #f3f6fc;
    --primary: #8cb1e8;
    --secondary: #d9e5f7;
    --accent: #2e71d6;

    --blend-text-color: #FFF;
    --blend-back-color: #000;
    --blend-highlight-color: #000;
}
```

#### Usage and Pattern

The framework uses variables for almost everithing, allowing the user to customize a big portion of the Akatsuki-CSS default styling, simulating a mini design system.

I've create a pattern that works like this. 
1. I create the sub variables for example, to a border(color, width and it's style) _Experimental_

```css
--border-color: var(--primary) // red;
--border-size: var(--md) // 16px;
--border-style: solid;
```

2. Then I created the 'shorthand' border variable

```css
--border: var(--border-color) var(--border-size) var(--border-style);
```

3. After this I can create variations by changing the value of any of the above variables in the HTML element or even in the global CSS.

```html
<section style="--border-style: dotted">
    <p>Lorem</p>
</section>
```

#### List of customizable variables

_in progress_

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
    // Rectangular Space

    --color-method-in-oklab: in oklab; -> default
    --color-method-srgb: in srgb;

    // Polar Space

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

Akatsuki has a decent amount of components as: switches, headers, navs, buttons, accordions, drropdowns and cards.

To create them, the user must follow some "rules", because the css is very specific to avoid conflict with others selectors.

**Note:** Follow the structure of the HTML or just copy it.

### Switch

```html
<label for="input__switch">

    Default Switch

    <input type="checkbox" id="input__switch" role="switch" aria-checked="false" />
</label>
```

- class variants: ```.squished, .squared```

To use the switch component, you need to use the for from the label pointing to the input id and use the role attribute equals to "switch"

### Accordion

```html
<details>
    <summary>Accordion</summary>

    <p>Accordion Text</p>
</details>
```

If you want the accordion to start as open, just add the open attribute to the summary tag.
* Ex: 
    ```html
    <summary open>Summary Open</summary>
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
<details role="listbox" >
    <summary>Dropdown</summary>

    <ul>
        <li><a href="#">item 1</a></li>
        <li><a href="#">item 2</a></li>
        <li><a href="#">item 3</a></li>
        <li><a href="#">item 4</a></li>
    </ul>
</details>
```

Same as the Accordion, use the open attribute to make it be opened at start.

### Header with Nav

```html
<header class="header-sticky">
    <a href="#" role="img" aria-label="">
      <img src="https://1000logos.net/wp-content/uploads/2021/12/Akatsuki-Logo.png" alt="logo" class="logo" /> <!--the logo must have the logo class-->
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

- class variants: ```.sticky```

In this case the nav and the header are together, but you can use them separately.

### Hero

```html
<div class="hero">
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
    --bg-img-url: url(https://images.unsplash.com/photo-1528353518104-dbd48bee7bc4?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1332&q=80);
    --bg-img-size: cover;
    --bg-img-repeat: no-repeat;
    --bg-img-pos: center;
}
```

A div with the clas wraps everything, you can pass the --bg-img-url to change the background as you please in the inline css or in another stylesheet above in the cascade.

___

[playground](https://codepen.io/Vattghern203/pen/XWOpQgw?editors=1100)
