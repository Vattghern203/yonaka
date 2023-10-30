# Akatsuki CSS

Akatsuki CSS is a flexible and highly customizable CSS framework with a wide range of presets. It is designed to cater to developers of all skill levels, providing an intuitive way to style elements without the need for additional tools like PostCSS or JavaScript.

## Features

- Easily customizable elements
- Rich collection of presets
- No reliance on PostCSS or JavaScript for customization
- Dependency Free in the compiled version

## Getting Started

To get started with Akatsuki CSS, follow these steps:

1. [Download](https://www.npmjs.com/package/yonaka) on NPM, clone the repository or use the [Jsdelivr](https://www.jsdelivr.com/package/npm/yonaka).

2. Add the `akatsuki.css` file to your project by importing it on your global CSS file.
```css
@import "node_modules/akatsuki-css/akatsuki.css"
```

or in the HTML

```html
<link rel="stylesheet" href="node_modules/akatsuki-css/akatsuki.css" />
```

## Customizing

- You can overwrite the default values of the variables, by simpling rewriting it in the `:root` or `html` selector. The default specifity is equals to 0

- You can also customize a variable for a single tag with the inline css

    * Ex: ```html <div style="--spacing: var(--lg)">Dummy Text</div>```

### Global Scoped Variables

#### Overview

Some of the variables used in the project.

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
1. I create the sub variables for example, to a border(color, width and it's style)

```css
--border-color: var(--primary) // red;
--border-size: var(--md) // 16px;
--border-style: solid;
```

2. Then I create the 'shorthand' border variable

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

in progress

##### Customizing colors

To customize colors, I highly recommend using [realtimecolors](https://www.realtimecolors.com/?colors=e2f7f8-092425-41cbd2-061819-2db7be&fonts=Poppins-Poppins).

1. First go the site and use the dark mode option, then generate your desired palette(HEX colors recommended).
2. Click to export and toggle the option themes and copy the code.
3. Change it in the framework by overwritting it.

```css
:root {
  --text: #e2f7f8;
  --background: #092425;
  --primary: #41cbd2;
  --secondary: #061819;
  --accent: #2db7be;
}

@media (prefers-color-scheme: light) {
  :root {
    --text: #071c1d;
    --background: #daf5f6;
    --primary: #2db7be;
    --secondary: #e6f8f9;
    --accent: #41cbd2;
  }
}
```

with these colors, the framework will generate variants as: muted, foreground and etc...

```css
:where(:root) {
    // Color created with the palette
    
    --destructive: #772626;
    
    // Blend Colors
    
    --blend-text-color: #000;
    --blend-back-color: #FFF;
    --blend-highlight-color: #FFF;
    
    // Content / Text
    
    --content-text: color-mix(in oklab, var(--text), var(--blend-text-color) 20%);
    
    //--inverted-text: filter:invert(1)
    
    // Foregrounds
    
    --muted-text: color-mix(in oklab, var(--text), var(--blend-text-color) 35%);
    
    --foreground-text: color-mix(in oklab, var(--text), var(--blend-text-color) 35%);
    
    --foreground-primary: color-mix(in oklab, var(--primary), var(--blend-text-color) 35%);
    
    --foreground-background: color-mix(in oklab, var(--background), var(--blend-back-color) 15%);
    
    --foreground-secondary: color-mix(in oklab, var(--secondary), var(--blend-back-color) 30%);
    
    --foreground-accent: color-mix(in oklab, var(--accent), var(--blend-text-color) 35%);
    
    --foreground-destructive: color-mix(in oklab, var(--destructive), var(--blend-back-color) 15%);```
}