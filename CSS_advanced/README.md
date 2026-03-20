# CSS Advanced — Learning Objectives

## 1. Selectors, Properties, and Values

A CSS rule is made of three parts:

- **Selector** — targets the HTML element(s) to style
- **Property** — the aspect you want to change
- **Value** — what you want to set that property to

```css
/* selector { property: value; } */
h1 { color: red; }
.card { font-size: 1.6rem; }
#header { background-color: #090909; }
```

**Types of selectors:**
- Tag: `p`, `h1`, `div`
- Class: `.card`, `.nav-item`
- ID: `#header`
- Attribute: `[data-section-theme="dark"]`, `[class^="col-"]`
- Pseudo-class: `a:hover`, `li:first-child`
- Pseudo-element: `p::before`, `h2::after`

---

## 2. The Difference Between Block and Inline Styling

| Type | Description | Default elements |
|------|-------------|-----------------|
| **Block** | Takes full width, starts on a new line | `div`, `p`, `h1–h6`, `section` |
| **Inline** | Takes only the space it needs, stays on the same line | `span`, `a`, `strong`, `em` |

```css
/* Force an element to be block */
.social-link { display: block; }

/* Force an element to be inline */
.nav-item { display: inline-block; }
```

---

## 3. How to Ensure Consistency Across All Browsers (CSS Reset)

Each browser applies its own default styles, which causes visual differences across Chrome, Firefox, Safari, etc.

**Two approaches:**

- **CSS Reset** — removes all browser defaults completely (Eric Meyer's reset)
- **Normalize.css** — keeps useful defaults but makes them consistent across browsers ✅ (preferred)

```css
/* Import normalize.css at the top of your stylesheet */
@import url('https://necolas.github.io/normalize.css/8.0.1/normalize.css');
```

---

## 4. How to Setup CSS Variables

CSS variables (custom properties) are defined in `:root` and reused throughout the stylesheet.

```css
/* Define variables */
:root {
    --color-primary: #d73953;
    --font-size-medium: 1.6rem;
    --font-weight-bold: 700;
}

/* Use variables */
.section-title {
    color: var(--color-primary);
    font-size: var(--font-size-medium);
    font-weight: var(--font-weight-bold);
}
```

**Advantages:**
- Change a value once → updates everywhere
- Can be overridden in a specific context (e.g. dark theme)

```css
/* Override for dark sections */
[data-section-theme="dark"] {
    --color-primary: #ffffff;
}
```

---

## 5. The Differences Between Inline, Embedded and External CSS

| Type | Where | Example | Use case |
|------|-------|---------|----------|
| **Inline** | Inside an HTML tag | `<p style="color: red;">` | Quick fixes, not recommended |
| **Embedded** | Inside `<style>` in `<head>` | `<style> p { color: red; } </style>` | Single page styles |
| **External** | Separate `.css` file linked in `<head>` | `<link rel="stylesheet" href="style.css">` | Best practice ✅ |

External CSS is preferred because it separates concerns, is reusable across pages, and is easier to maintain.

---

## 6. How Grid Systems Work (With Floats)

A float-based grid divides a row into columns using percentages and `float: left`.

```css
/* Base column rule using attribute selector */
[class^="col-"] {
    float: left;
    padding: 0.5rem;
}

/* Column widths */
.col-1-3 { width: 33.33%; }  /* 1/3 of the row */
.col-1-2 { width: 50%; }     /* 1/2 of the row */

/* Clearfix to contain floated children */
.row::after {
    content: "";
    display: table;
    clear: both;
}
```

```html
<div class="row">
    <div class="col-1-3">Column 1</div>
    <div class="col-1-3">Column 2</div>
    <div class="col-1-3">Column 3</div>
</div>
```

---

## 7. The Difference Between Icon Webfonts and SVG Icons

| | Webfonts (e.g. Font Awesome) | SVG Icons |
|---|---|---|
| **Format** | Font file (`.woff`, `.ttf`) | XML-based vector |
| **Styling** | CSS `color`, `font-size` | CSS `fill`, `width`, `height` |
| **Accessibility** | Harder | Easier (can add `<title>`) |
| **Performance** | One HTTP request for all icons | One per icon (unless sprited) |
| **Scalability** | ✅ Vector | ✅ Vector |
| **Multi-color** | ❌ Single color only | ✅ Multi-color supported |

```css
/* Styling an SVG icon */
.social-link svg {
    fill: var(--text-color);
    width: 25px;
    height: 25px;
}
```

---

## 8. The Difference Between Pseudo-Classes and Pseudo-Elements

### Pseudo-classes (`:`)
Target an element in a **specific state**.

```css
a:hover   { text-decoration: underline; }
a:visited { font-style: italic; }
a:active  { background-color: var(--color-light-grey); }
li:first-child { color: red; }
```

### Pseudo-elements (`::`)
Target a **specific part** of an element, or insert virtual content.

```css
p::first-line  { font-weight: bold; }
h2::before     { content: "→ "; }
.nav-link::after { content: ""; position: absolute; }
```

**Key rule:** pseudo-classes use `:`, pseudo-elements use `::`.

---

## 9. How to Make Background Gradients

CSS gradients are created with `background` or `background-image`.

### Linear Gradient
```css
/* Direction + color stops */
.hero {
    background: linear-gradient(to right, #d73953, #090909);
}

/* With angle */
.section {
    background: linear-gradient(135deg, #ffffff 0%, #f3f3f3 100%);
}
```

### Radial Gradient
```css
.card {
    background: radial-gradient(circle, #d73953, #090909);
}
```

### With Transparency
```css
/* Overlay effect */
.overlay {
    background: linear-gradient(rgba(0,0,0,0), rgba(0,0,0,0.7));
}
```

---

## 10. How to Animate Elements in CSS

CSS animations use `@keyframes` combined with the `animation` property.

```css
/* Define the animation */
@keyframes fadeIn {
    from { opacity: 0; transform: translateY(20px); }
    to   { opacity: 1; transform: translateY(0); }
}

/* Apply it */
.card {
    animation: fadeIn 0.5s ease-in-out;
}
```

**Animation properties:**
```css
.element {
    animation-name: fadeIn;
    animation-duration: 0.5s;
    animation-timing-function: ease-in-out;
    animation-delay: 0.2s;
    animation-iteration-count: infinite; /* or a number */
    animation-direction: alternate;

    /* Shorthand */
    animation: fadeIn 0.5s ease-in-out 0.2s infinite alternate;
}
```

**Transitions** (simpler, for hover effects):
```css
.button {
    transition: background-color 0.3s ease;
}
.button:hover {
    background-color: var(--color-primary);
}
```

---

## 11. How to Transform (2D, 3D) Elements

The `transform` property moves, scales, rotates, or skews elements.

### 2D Transforms
```css
.card:hover {
    transform: translateX(10px);    /* Move horizontally */
    transform: translateY(-5px);    /* Move vertically */
    transform: scale(1.05);         /* Zoom in slightly */
    transform: rotate(45deg);       /* Rotate */
    transform: skewX(10deg);        /* Skew */

    /* Combine multiple transforms */
    transform: translateY(-5px) scale(1.05);
}
```

### 3D Transforms
```css
.card {
    transform: perspective(500px) rotateY(30deg);  /* 3D rotation */
    transform: translateZ(50px);                    /* Move on Z axis */
    transform-style: preserve-3d;                  /* Keep 3D for children */
}
```

---

## 12. What Vendor Prefixes Are

Vendor prefixes are prefixes added by browsers to support experimental or non-standard CSS features before they become official.

| Prefix | Browser |
|--------|---------|
| `-webkit-` | Chrome, Safari, Edge |
| `-moz-` | Firefox |
| `-ms-` | Internet Explorer |
| `-o-` | Opera (old) |

```css
/* Example: animation with vendor prefixes */
.element {
    -webkit-animation: fadeIn 0.5s ease;
    -moz-animation: fadeIn 0.5s ease;
    animation: fadeIn 0.5s ease; /* Standard — always last */
}

/* Example: transform with vendor prefixes */
.element {
    -webkit-transform: rotate(45deg);
    -moz-transform: rotate(45deg);
    transform: rotate(45deg); /* Standard — always last */
}
```

> Today, most modern browsers support standard CSS properties without prefixes. Tools like **Autoprefixer** can automatically add vendor prefixes when needed.