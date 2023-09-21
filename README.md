# Yonaka Framework

Yonaka is a versatile CSS framework designed to provide a mini design system that can be easily customized within your HTML files. It leverages the power of CSS variables to allow seamless changes to the design. By altering the values of these variables, you can achieve a wide range of design possibilities.

## How it Works

- Utilizes semantic HTML for better understanding and accessibility.
- Provides an extensive set of utility classes for quick and effective styling.

## Example Usage

To get started, include the framework in your project and start utilizing the provided CSS variables and utility classes. Here's a basic example of how to use it:

```html
<!-- Include the framework CSS -->
<link rel="stylesheet" href="path/to/your/framework.css">

<!-- Your HTML content here, utilizing the framework -->
<!-- For example: -->
<div class="row">
    <div class="col">
        <h1 style="--text-color: var(--accent);">Hello, World!</h1>
        <p style="--text-color: var(--text);">This is a sample paragraph.</p>
    </div>
</div>
```

## Customization

To customize the design, simply adjust the CSS variables within your HTML or in an external stylesheet.

```css
:root {
    --bg: #ffffff; /* Change the background color */
    --text-color: #000000; /* Change the text color */
    /* Add more custom variables as needed */
}
```

You can also change variable values inline in the HTML using the `style` attribute:

```html
<div class="row">
    <div class="col">
        <h1 style="--text-color: var(--secondary);">Hello, World!</h1>
        <p style="--text-color: var(--muted-text);">This is a sample paragraph.</p>
    </div>
</div>
```