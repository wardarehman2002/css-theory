# CSS Theory Assignment

---

## Q1 — What is CSS and How Do You Add It to an HTML Page?

### What is CSS?

**CSS** stands for **Cascading Style Sheets**. It is a stylesheet language used to describe the visual presentation of HTML documents. Before CSS, all styling had to be done directly inside HTML using attributes like `color`, `font`, and `bgcolor`, which mixed structure with presentation. CSS solves this by **separating content (HTML) from design (CSS)**, making code cleaner, easier to maintain, and reusable across many pages.

---

### Three Methods of Adding CSS

#### 1. External CSS (Recommended)
A separate `.css` file is linked to the HTML using a `<link>` tag in the `<head>`. This is the **preferred method** in real projects because:
- One stylesheet can style hundreds of pages
- Changes are made in one place and reflected everywhere
- Browser can **cache** the file, improving load speed
- Keeps HTML clean and readable

```html
<!-- index.html -->
<head>
  <link rel="stylesheet" href="styles.css" />
</head>
<body>
  <h1>Hello World</h1>
</body>
```

```css
/* styles.css */
h1 {
  color: navy;
  font-size: 2rem;
}
```

---

#### 2. Internal CSS
CSS is written inside a `<style>` tag within the `<head>` of the HTML document. Useful for single-page projects or quick prototypes.

```html
<!DOCTYPE html>
<html>
  <head>
    <style>
      h1 {
        color: darkgreen;
        font-family: Georgia, serif;
      }
    </style>
  </head>
  <body>
    <h1>Hello World</h1>
  </body>
</html>
```

---

#### 3. Inline CSS
CSS is written directly on a specific element using the `style` attribute. Should be avoided in real projects — it mixes structure and style, cannot be reused, and is hard to maintain.

```html
<h1 style="color: crimson; font-size: 24px;">Hello World</h1>
```

---

### Why External CSS Is Preferred Over Inline CSS

| Feature              | External CSS         | Inline CSS           |
|----------------------|----------------------|----------------------|
| Reusability          |  Across all pages  |  One element only  |
| Maintainability      |  Edit one file     |  Edit every element|
| Separation of concerns |  Yes             |  No                |
| Browser caching      |  Yes               |  No                |
| Specificity issues   |  Manageable        |  Hard to override  |

---

## Q2 — Explain CSS Selectors with Examples

CSS selectors are patterns used to target HTML elements so styles can be applied to them. Different selectors have different **specificity** — a measure of how strong the rule is.

---

### Selector Types

#### 1. Element Selector
Targets all elements of a given HTML tag type.

```css
p {
  color: #333;
  line-height: 1.6;
}
```

---

#### 2. Class Selector
Targets all elements with a specific `class` attribute. Prefixed with a dot (`.`).
- **The same class can be used on multiple elements** — ideal for reusable styles.

```css
.card {
  background-color: white;
  border-radius: 8px;
  padding: 16px;
}
```

---

#### 3. ID Selector
Targets a **single unique element** with a specific `id` attribute. Prefixed with `#`.
- **An ID must be unique on a page** — you should never assign the same ID to more than one element.
- IDs have **higher specificity** than classes.

```css
#main-header {
  background-color: #1a1a2e;
  color: white;
}
```

---

#### 4. Group Selector
Applies the same styles to multiple selectors, separated by commas.

```css
h1,
h2,
h3 {
  font-family: "Georgia", serif;
  font-weight: 700;
}
```

---

#### 5. Descendant Selector
Targets an element that is **anywhere inside** another element (not necessarily a direct child).

```css
/* Targets ALL <a> tags inside .nav, regardless of nesting depth */
.nav a {
  text-decoration: none;
  color: #555;
}
```

---

#### 6. Child Selector (`>`)
Targets only **direct children** of an element — one level deep only.

```css
/* Only targets <li> elements that are DIRECT children of ul */
ul > li {
  list-style-type: disc;
  color: darkblue;
}
```

---

#### 7. Universal Selector
Targets **every element** on the page. Commonly used in CSS resets.

```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
```

---

### Class vs ID — When to Use Which?

| Feature             | Class (`.name`)               | ID (`#name`)                   |
|---------------------|-------------------------------|--------------------------------|
| Reusability         | Multiple elements           |   One element per page        |
| Specificity score   | 0-1-0                         | 0-1-0 → 1-0-0 (higher)        |
| JavaScript hook     | `querySelectorAll`            | `getElementById` (faster)      |
| Use case            | Repeated components, styles   | Unique page sections, anchors  |

> **Rule of thumb:** Use classes for styling; use IDs for unique anchors or JavaScript targeting.

**Which has higher specificity — class or ID?**
An **ID** has higher specificity (score: `1-0-0`) than a class (score: `0-1-0`).

---

## Q3 — What is the CSS Box Model?

Every HTML element is rendered as a rectangular box. The **CSS Box Model** describes the four layers that make up this box, from inside to outside:

```
+------------------------------+
|          MARGIN              |  ← Outermost: space outside the element
|  +------------------------+  |
|  |        BORDER          |  |  ← Decorative border around the padding
|  |  +------------------+  |  |
|  |  |     PADDING      |  |  |  ← Space between content and border
|  |  |  +------------+  |  |  |
|  |  |  |  CONTENT   |  |  |  |  ← Innermost: text, images, etc.
|  |  |  +------------+  |  |  |
|  |  +------------------+  |  |
|  +------------------------+  |
+------------------------------+
```

---

### The Four Layers

| Layer     | Description                                                                 |
|-----------|-----------------------------------------------------------------------------|
| **Content** | The innermost area where text, images, and child elements live. Controlled by `width` and `height`. |
| **Padding** | Space **inside** the border, between the content and the border. It is part of the element's background. |
| **Border** | A line that wraps around the padding and content. Can be styled with `border-width`, `border-style`, `border-color`. |
| **Margin** | Space **outside** the border. It separates the element from neighboring elements. Margins are always transparent. |

---

### `box-sizing: content-box` vs `box-sizing: border-box`

#### `content-box` (browser default)
`width` refers to the **content area only**. Padding and border are added **on top** of the declared width.

```css
/* Total rendered width = 300 + 20 + 20 + 2 + 2 = 344px */
.box {
  width: 300px;
  padding: 20px;
  border: 2px solid black;
  box-sizing: content-box;
}
```

#### `border-box` (industry standard )
`width` **includes** padding and border. The content area shrinks to accommodate them. This makes sizing predictable and is used in all professional projects.

```css
/* Total rendered width = exactly 300px */
.box {
  width: 300px;
  padding: 20px;
  border: 2px solid black;
  box-sizing: border-box;
}
```

---

### Code Task — `.box` Rule

```css
.box {
  width: 300px;
  padding: 20px;
  border: 2px solid #333;
  margin: 16px;
  box-sizing: border-box;
  /* Total visual width = 300px (padding + border are absorbed within) */
  /* Content area = 300 - 20 - 20 - 2 - 2 = 256px */
}
```

### `margin: 0 auto` Explained
When applied to a **block element with a defined width**, `margin: 0 auto` sets top/bottom margin to `0` and left/right margin to `auto`, which distributes equal space on both sides — **centering the element horizontally** within its container.

```css
.container {
  width: 800px;
  margin: 0 auto; /* Centers the container on the page */
}
```

---

## Q4 — Explain CSS Colors

CSS provides five formats to define colors:

---

### 1. Named Colors
English names for a set of ~140 predefined colors.

```css
color: orange;
background-color: tomato;
```

---

### 2. HEX (`#RRGGBB`)
A hexadecimal code representing Red, Green, Blue channels from `00` (none) to `FF` (full). **Most commonly used by developers** — clean, short, and widely supported.

```css
color: #F97316; /* Orange */
```

---

### 3. RGB (`rgb(r, g, b)`)
Defines color using Red, Green, Blue values from `0` to `255`.

```css
color: rgb(249, 115, 22); /* Orange */
```

---

### 4. RGBA (`rgba(r, g, b, a)`)
Same as RGB with an added **Alpha** (transparency) channel from `0` (fully transparent) to `1` (fully opaque). The 'A' stands for **Alpha**.

```css
color: rgba(249, 115, 22, 0.7); /* Orange at 70% opacity */
```

---

### 5. HSL (`hsl(hue, saturation%, lightness%)`)
Defines color using Hue (0–360 degrees on a color wheel), Saturation, and Lightness. Great for creating color themes and tints programmatically.

```css
color: hsl(24, 95%, 53%); /* Orange */
```

---

### Code Task — Orange in All Five Formats

```css
/* #F97316 in all five CSS color formats */

.orange-named     { color: orange; }              /* closest named color */
.orange-hex       { color: #F97316; }
.orange-rgb       { color: rgb(249, 115, 22); }
.orange-rgba      { color: rgba(249, 115, 22, 1); }
.orange-hsl       { color: hsl(24, 95%, 53%); }
```

---

### `opacity: 0.5` vs `rgba(0, 0, 0, 0.5)`

| Property                    | What it affects                                              | Affects children? |
|-----------------------------|--------------------------------------------------------------|-------------------|
| `opacity: 0.5`              | The **entire element** including its children, text, borders |  **Yes** — inherited by all child elements |
| `rgba(0, 0, 0, 0.5)`        | Only the **specific color property** it is assigned to       |  **No** — children unaffected |

```css
/* BAD: the text inside .overlay also becomes transparent */
.overlay {
  background-color: black;
  opacity: 0.5;
}

/* GOOD: only the background is transparent, text stays opaque */
.overlay {
  background-color: rgba(0, 0, 0, 0.5);
}
```

---

## Q5 — What are CSS Units?

CSS units fall into two categories: **absolute** (fixed size) and **relative** (relative to something else).

---

### Unit Reference Table

| Unit  | Relative To                            | Best Use Case                          |
|-------|----------------------------------------|----------------------------------------|
| `px`  | Fixed screen pixel                     | Borders, shadows, fixed-size elements  |
| `%`   | Parent element's dimension             | Fluid widths, responsive layouts       |
| `rem` | Root element (`<html>`) font-size      | Font sizes, spacing (accessibility ) |
| `em`  | Nearest parent's font-size             | Component-relative spacing             |
| `vh`  | 1% of viewport height                 | Full-screen sections, hero areas       |
| `vw`  | 1% of viewport width                  | Full-width elements, fluid typography  |

---

### Detailed Explanations

#### `px` — Pixels
Absolute unit. `1px` is one CSS pixel (may be fractional on HiDPI screens). Predictable but not flexible.

```css
.divider {
  border-top: 1px solid #eee;
}
```

---

#### `%` — Percentage
Relative to the **parent element's** corresponding dimension (width or height).

```css
.column {
  width: 50%; /* Half the width of its parent */
}
```

---

#### `rem` — Root Em
Relative to the **`<html>` root font-size**, which defaults to `16px` in all browsers. `1rem = 16px` by default. Unlike `em`, it never compounds. **Preferred for font-size** because when a user changes their browser's default font size, rem-based text scales accordingly — improving **accessibility**.

```css
body {
  font-size: 1rem;   /* 16px */
}
h1 {
  font-size: 2.5rem; /* 40px */
}
```

---

#### `em` — Em
Relative to the **nearest parent's font-size**. Can compound if nested, which makes it tricky but useful for components that should scale with their context.

```css
.button {
  font-size: 1rem;
  padding: 0.75em 1.5em; /* Scales with the button's own font-size */
}
```

---

#### `vh` — Viewport Height
`1vh = 1% of the browser viewport height`. `vh` stands for **Viewport Height**.

```css
.hero {
  height: 100vh; /* Full screen height */
}
```

---

#### `vw` — Viewport Width
`1vw = 1% of the browser viewport width`. Great for fluid typography that scales with screen size.

```css
h1 {
  font-size: 5vw; /* Gets bigger on wide screens */
}
```

---

### Why `rem` is Better Than `px` for Font-Size (Accessibility)

If you set all font sizes in `px`, they are **fixed** regardless of the user's browser preference. Users who increase their default font size (visually impaired users, older users) get no benefit. With `rem`, all sizes are relative to the root, so changing the root size (or letting the user's browser preference apply) **scales the entire UI proportionally**.

---

### Code Task — Hero Section

```css
/* Hero section: full viewport height, scalable font, rem max-width */
.hero {
  height: 100vh;               /* Full viewport height (vh) */
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 2rem;               /* Rem for spacing */
  background-color: #0f172a;
}

.hero__content {
  max-width: 60rem;            /* Max width in rem (~960px) */
  width: 100%;
  text-align: center;
}

.hero__title {
  font-size: clamp(2rem, 5vw, 4rem); /* Fluid: vw scales with viewport, clamped with rem min/max */
  color: white;
  margin-bottom: 1rem;
}

.hero__subtitle {
  font-size: clamp(1rem, 2.5vw, 1.5rem);
  color: #94a3b8;
}
```

---

## Q6 — What is CSS Specificity and How Does the Cascade Work?

### Specificity

**Specificity** is the scoring system the browser uses to decide which CSS rule wins when multiple rules target the same element. It is calculated as a 3-part score: **(A - B - C)**.

| Selector Type             | Score (A-B-C) | Example                    |
|---------------------------|---------------|----------------------------|
| Inline style              | `1-0-0-0`     | `style="color: red"`       |
| ID selector               | `1-0-0`       | `#intro`                   |
| Class / attribute / pseudo-class | `0-1-0` | `.text`, `[type]`, `:hover` |
| Element / pseudo-element  | `0-0-1`       | `p`, `h1`, `::before`      |
| Universal selector        | `0-0-0`       | `*`                        |

Scores are compared **left to right**. A rule with score `0-1-0` always beats `0-0-10` — you can't "overflow" from a lower tier to a higher one.

---

### The Cascade

The **cascade** is the algorithm that determines which styles apply when there are conflicts. It considers three factors in order:

1. **Origin & Importance** — Browser default styles < Author styles < `!important` author styles
2. **Specificity** — Higher score wins
3. **Source Order** — When specificity is equal, the **rule that appears last in the CSS** wins

---

### Inheritance

Some CSS properties (like `color`, `font-family`, `line-height`) are **inherited** by child elements from their parents. Others (like `margin`, `padding`, `border`) are **not** inherited by default.

```css
body {
  font-family: Georgia, serif; /* Inherited by all children */
  color: #333;                 /* Inherited by all children */
}
```

---

### `!important`

Appending `!important` to a declaration overrides normal specificity rules and forces the rule to win (unless another `!important` rule has higher specificity). **It should be avoided** because:
- It breaks the natural cascade and makes debugging extremely difficult
- It creates an "arms race" where more and more `!important` rules accumulate
- It signals a specificity problem that should be solved structurally

```css
/* Avoid this unless absolutely necessary */
p {
  color: blue !important;
}
```

---

### Code Task — Three Rules, One Element

```html
<p id="intro" class="text">Hello</p>
```

```css
/* Rule 1 — Element selector: specificity 0-0-1 */
p {
  color: blue;
}

/* Rule 2 — Class selector: specificity 0-1-0 (wins over Rule 1) */
.text {
  color: green;
}

/* Rule 3 — ID selector: specificity 1-0-0 (wins over both) */
#intro {
  color: red;
}
```

**Winner: `color: red`** from Rule 3.

**Why?** The ID selector `#intro` has the highest specificity score (`1-0-0`), beating the class selector `.text` (`0-1-0`) and the element selector `p` (`0-0-1`). The text "Hello" will appear **red**.

> If two rules had equal specificity, the one **later in the file** would win (source order).

---

## Q7 — Explain CSS Flexbox

### What is Flexbox?

**Flexbox** (Flexible Box Layout) is a **1-dimensional layout system** that arranges items in a row or column and distributes space between them intelligently. It was designed to solve layout problems that were painful with block/float-based layouts.

When you set `display: flex` on a container:
- The container becomes a **flex container**
- Its direct children become **flex items**
- Items align on the **main axis** (horizontal by default) and the **cross axis** (vertical by default)

---

### Key Properties

#### `flex-direction`
Sets the **main axis** direction.

```css
.container {
  flex-direction: row;           /* Default: left to right */
  flex-direction: row-reverse;   /* Right to left */
  flex-direction: column;        /* Top to bottom */
  flex-direction: column-reverse;
}
```

---

#### `justify-content`
Aligns items along the **main axis** (horizontal when `flex-direction: row`).

```css
.container {
  justify-content: flex-start;    /* Default */
  justify-content: flex-end;
  justify-content: center;
  justify-content: space-between; /* Equal gaps between items */
  justify-content: space-around;
  justify-content: space-evenly;
}
```

---

#### `align-items`
Aligns items along the **cross axis** (vertical when `flex-direction: row`).

```css
.container {
  align-items: stretch;    /* Default: stretch to fill */
  align-items: center;     /* Center vertically */
  align-items: flex-start;
  align-items: flex-end;
  align-items: baseline;
}
```

> **Key difference:** `justify-content` = main axis; `align-items` = cross axis.

---

#### `flex-wrap`
By default, all flex items try to fit on one line. `flex-wrap: wrap` allows items to **wrap to the next line** when they run out of space.

```css
.container {
  flex-wrap: wrap; /* Items drop to next row when needed */
}
```

---

#### `gap`
Sets the spacing between flex items (row and column gap combined).

```css
.container {
  gap: 16px;           /* Same gap between rows and columns */
  gap: 12px 24px;      /* row-gap column-gap */
}
```

---

#### `flex: 1`
Applied to a flex **item**, it means: take up all available remaining space, equally distributed among all items with `flex: 1`. It is shorthand for `flex: 1 1 0` (grow, shrink, basis).

```css
.sidebar { flex: 0 0 250px; } /* Fixed sidebar */
.main    { flex: 1; }         /* Main takes remaining space */
```

---

### Centering Both Horizontally and Vertically

```css
.centered-container {
  display: flex;
  justify-content: center; /* Horizontal center */
  align-items: center;     /* Vertical center */
  height: 100vh;
}
```

---

### Real-World Use Cases

1. **Navigation bars** — logo left, links right, vertically centered
2. **Card grids** — rows of cards with equal spacing that wrap on smaller screens

---

### Code Task — Flexbox Navbar

```css
/* Navbar: logo left, nav links right, vertically centred, with gap */

.navbar {
  display: flex;
  justify-content: space-between; /* Logo left, links right */
  align-items: center;            /* Vertically centred */
  padding: 0 2rem;
  height: 64px;
  background-color: #1e293b;
}

.navbar__logo {
  font-size: 1.25rem;
  font-weight: 700;
  color: #f8fafc;
  text-decoration: none;
}

.navbar__links {
  display: flex;
  align-items: center;
  gap: 2rem;           /* Space between individual links */
  list-style: none;
  margin: 0;
  padding: 0;
}

.navbar__links a {
  color: #cbd5e1;
  text-decoration: none;
  font-size: 0.95rem;
  transition: color 0.2s ease;
}

.navbar__links a:hover {
  color: #f97316;
}
```

```html
<!-- Corresponding HTML structure -->
<nav class="navbar">
  <a href="/" class="navbar__logo">BrandName</a>
  <ul class="navbar__links">
    <li><a href="/about">About</a></li>
    <li><a href="/work">Work</a></li>
    <li><a href="/contact">Contact</a></li>
  </ul>
</nav>
```

---

## Q8 — What are CSS Pseudo-classes and Pseudo-elements?

### The Difference

| Feature         | Pseudo-class (`:`)                              | Pseudo-element (`::`)                              |
|-----------------|-------------------------------------------------|----------------------------------------------------|
| Syntax          | Single colon: `:hover`                          | Double colon: `::before`                           |
| Purpose         | Style based on **state or position**            | Style a **specific part** of an element            |
| Adds to DOM?    | No                                              | No — creates a **virtual element** (not real HTML) |
| Example         | `:hover`, `:focus`, `:nth-child()`              | `::before`, `::after`, `::placeholder`             |

> `::before` and `::after` do **not** add real HTML elements. They are rendered by the browser but do not appear in the DOM. They **require the `content` property** to render — without it, they are invisible (even `content: ""` is needed for decorative uses).

---

### Pseudo-classes

#### `:hover`
Applies when the mouse is over an element.

```css
.button:hover {
  background-color: #f97316;
  cursor: pointer;
}
```

---

#### `:focus`
Applies when an element is focused (e.g., via keyboard tab or click on input).

```css
input:focus {
  outline: 2px solid #3b82f6;
  border-color: #3b82f6;
}
```

---

#### `:nth-child()`
Selects elements based on their position among siblings. `:nth-child(2n)` selects **every even-numbered** element (2nd, 4th, 6th...).

```css
/* Zebra stripe a table */
tr:nth-child(even) {
  background-color: #f8fafc;
}

/* Style every 3rd list item */
li:nth-child(3n) {
  color: #f97316;
  font-weight: bold;
}
```

---

#### `:not()`
Selects elements that do **not** match the given selector.

```css
/* Style all buttons except the primary one */
.button:not(.button--primary) {
  background-color: transparent;
  border: 1px solid #ccc;
}
```

---

### Pseudo-elements

#### `::before` and `::after`
Insert virtual content before or after an element's actual content. The `content` property is required.

```css
.featured::before {
  content: "H ";       /* content property is required */
  color: #f97316;
  font-weight: bold;
}
```

---

#### `::placeholder`
Styles the placeholder text of an `<input>` or `<textarea>`.

```css
input::placeholder {
  color: #94a3b8;
  font-style: italic;
}
```

---

### Code Task — Hover, `::before`, and Placeholder

```css
/* 1. Button turns orange on hover */
.btn {
  background-color: #1e293b;
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  transition: background-color 0.25s ease;
}

.btn:hover {
  background-color: #f97316;
}

/* 2. Add "H " before every .featured list item using ::before */
ul li.featured::before {
  content: "H ";        /* content property is REQUIRED */
  color: #f97316;
  font-weight: 700;
}

/* 3. Style placeholder text grey in an input */
input::placeholder {
  color: #9ca3af;
  font-style: italic;
}
```

---

## Q9 — Explain CSS Transitions and Animations

### Transitions vs Animations

| Feature         | Transitions                                     | Animations (`@keyframes`)                          |
|-----------------|-------------------------------------------------|----------------------------------------------------|
| Trigger needed? |  Yes — requires a state change (`:hover`, `:focus`, class toggle via JS) |  No — can run automatically on page load |
| Control         | Start → End (2 states only)                     | Full keyframe control (unlimited states)           |
| Looping         | Not natively                                    |  Yes — `animation-iteration-count: infinite`     |
| Use case        | Hover effects, focus states, toggles            | Loading spinners, entrance animations, loaders     |

---

### Transitions

The `transition` shorthand: `property | duration | timing-function | delay`

```css
.button {
  transition: background-color 0.3s ease 0s;
  /* OR multiple properties: */
  transition: background-color 0.3s ease, transform 0.2s ease-out;
}
```

#### Timing Functions

| Function    | Description                                                        |
|-------------|-------------------------------------------------------------------|
| `ease`      | Starts slow, speeds up, ends slow. The default — feels natural.   |
| `ease-in`   | Starts slow, ends fast. Good for elements leaving the screen.     |
| `ease-out`  | Starts fast, ends slow. Good for elements entering the screen.    |
| `linear`    | Constant speed throughout. Good for spinners, progress bars.      |

---

### `@keyframes` and Animations

```css
@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.card {
  animation: fadeInUp 0.6s ease-out forwards;
  /* animation: name | duration | timing | fill-mode */
}
```

#### `animation-fill-mode: forwards`
After the animation completes, the element **stays in the final keyframe state** rather than snapping back to its original styles.

#### `animation-iteration-count: infinite`
Makes the animation **loop forever**, never stopping. Useful for loading spinners or pulsing effects.

---

### Why Prefer `transform` and `opacity` for Animations?

Animating properties like `width`, `margin`, or `top` causes the browser to **recalculate layout (reflow)** and **repaint** the entire page on every frame — extremely expensive on the GPU/CPU.

`transform` and `opacity` are **composited on the GPU** and do not trigger layout recalculation. This means they run at a smooth **60fps** even on lower-end devices.

| Property        | Triggers layout reflow? | Performance   |
|-----------------|------------------------|---------------|
| `transform`     |  No                   |  Fast (GPU) |
| `opacity`       |  No                   |  Fast (GPU) |
| `width`/`height`|  Yes                  |  Slow       |
| `margin`/`top`  |  Yes                  |  Slow       |

---

### Code Task — Hover Lift + Fade-In Animation

```css
/* Fade-in from below on page load */
@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(40px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.card {
  background: white;
  border-radius: 12px;
  padding: 24px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);

  /* Entrance animation */
  animation: fadeInUp 0.6s ease-out forwards;

  /* Smooth transition for hover effect */
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

/* Lift up and deepen shadow on hover */
.card:hover {
  transform: translateY(-8px);
  box-shadow: 0 16px 40px rgba(0, 0, 0, 0.15);
}
```

> **Common triggers for transitions:** `:hover`, `:focus`, `:active`, `:checked`, or JavaScript adding/removing a CSS class.

> **Multiple transitions:** Yes — separate them with commas: `transition: transform 0.3s ease, opacity 0.2s ease;`

---

## Q10 — Responsive Web Design: Media Queries, CSS Variables, and Mobile-First

---

### Part A — Media Queries

A **media query** is a CSS rule that applies styles **only when a certain condition is met** — most commonly a screen size range. They are the foundation of responsive design.

**Syntax:**
```css
@media (min-width: 768px) {
  /* Styles for screens 768px and wider */
}
```

#### Standard Industry Breakpoints

| Breakpoint   | Width          | Target Devices            |
|--------------|----------------|---------------------------|
| Mobile       | `< 768px`      | Phones (default styles)   |
| Tablet       | `≥ 768px`      | Tablets, large phones     |
| Laptop       | `≥ 1024px`     | Laptops, small desktops   |
| Desktop      | `≥ 1280px`     | Large monitors            |

---

### Part B — Mobile-First Approach

**Mobile-first** means you write your **base styles for mobile screens first**, then use `min-width` media queries to layer in styles for larger screens.

This is the industry standard because:
- Mobile traffic accounts for the majority of web usage globally
- It forces prioritization of content (no room for clutter on small screens)
- Browsers load CSS top-to-bottom — mobile styles are always loaded; desktop enhancements only load when needed
- It generally produces **lighter, faster pages**

#### Mobile-First vs Desktop-First

```css
/* MOBILE-FIRST  (use min-width) */
.grid { grid-template-columns: 1fr; }           /* Mobile: single column */
@media (min-width: 768px)  { .grid { grid-template-columns: 1fr 1fr; } }
@media (min-width: 1024px) { .grid { grid-template-columns: repeat(3, 1fr); } }

/* DESKTOP-FIRST  (use max-width — avoid) */
.grid { grid-template-columns: repeat(3, 1fr); } /* Desktop: three columns */
@media (max-width: 1024px) { .grid { grid-template-columns: 1fr 1fr; } }
@media (max-width: 768px)  { .grid { grid-template-columns: 1fr; } }
```

---

### Part C — CSS Variables (Custom Properties)

CSS custom properties (variables) let you **store values in one place** and reuse them throughout your stylesheet. They are defined with `--` prefix inside a selector (typically `:root` for global scope) and accessed with `var()`.

```css
:root {
  --color-primary: #f97316;
  --font-size-base: 1rem;
}

h1 {
  color: var(--color-primary);
  font-size: calc(var(--font-size-base) * 2.5);
}
```

#### `var(--color)` vs `var(--color, fallback)`

- `var(--color)` — uses the variable; if undefined, the property is **invalid**
- `var(--color, #333)` — uses the variable; if undefined, falls back to `#333`

```css
color: var(--text-color, #1a1a1a); /* Falls back to #1a1a1a if --text-color is not defined */
```

#### Can JavaScript read and change CSS variables?

**Yes.** JavaScript can read and write CSS variables at runtime:

```javascript
// Read
const value = getComputedStyle(document.documentElement).getPropertyValue('--color-primary');

// Write
document.documentElement.style.setProperty('--color-primary', '#3b82f6');
```

---

### `@media (prefers-color-scheme: dark)`

This media query detects the **user's OS-level dark mode preference** and automatically applies your dark theme without requiring any user interaction.

```css
@media (prefers-color-scheme: dark) {
  :root {
    --color-bg: #0f172a;
    --color-text: #f1f5f9;
  }
}
```

---

### Code Task — Design System with Dark Mode & Responsive Layout

```css
/* =============================================
   DESIGN SYSTEM — :root custom properties
   ============================================= */

:root {
  /* Colors */
  --color-bg:         #ffffff;
  --color-surface:    #f8fafc;
  --color-border:     #e2e8f0;
  --color-text:       #1e293b;
  --color-text-muted: #64748b;
  --color-primary:    #f97316;
  --color-primary-hover: #ea6c0a;

  /* Typography */
  --font-size-xs:   0.75rem;   /* 12px */
  --font-size-sm:   0.875rem;  /* 14px */
  --font-size-base: 1rem;      /* 16px */
  --font-size-lg:   1.125rem;  /* 18px */
  --font-size-xl:   1.25rem;   /* 20px */
  --font-size-2xl:  1.5rem;    /* 24px */
  --font-size-3xl:  2rem;      /* 32px */
  --font-size-4xl:  2.5rem;    /* 40px */

  /* Spacing */
  --space-1:  0.25rem;   /* 4px */
  --space-2:  0.5rem;    /* 8px */
  --space-3:  0.75rem;   /* 12px */
  --space-4:  1rem;      /* 16px */
  --space-6:  1.5rem;    /* 24px */
  --space-8:  2rem;      /* 32px */
  --space-12: 3rem;      /* 48px */
  --space-16: 4rem;      /* 64px */

  /* Border Radius */
  --radius-sm: 4px;
  --radius-md: 8px;
  --radius-lg: 16px;

  /* Shadows */
  --shadow-sm: 0 1px 3px rgba(0, 0, 0, 0.08);
  --shadow-md: 0 4px 12px rgba(0, 0, 0, 0.12);
  --shadow-lg: 0 16px 40px rgba(0, 0, 0, 0.16);
}


/* =============================================
   DARK MODE — via data attribute
   (can be toggled by JS: document.documentElement.dataset.theme = 'dark')
   ============================================= */

[data-theme="dark"] {
  --color-bg:         #0f172a;
  --color-surface:    #1e293b;
  --color-border:     #334155;
  --color-text:       #f1f5f9;
  --color-text-muted: #94a3b8;
  --color-primary:    #fb923c;
  --color-primary-hover: #f97316;

  --shadow-sm: 0 1px 3px rgba(0, 0, 0, 0.4);
  --shadow-md: 0 4px 12px rgba(0, 0, 0, 0.5);
  --shadow-lg: 0 16px 40px rgba(0, 0, 0, 0.6);
}

/* Also support OS-level dark mode preference automatically */
@media (prefers-color-scheme: dark) {
  :root:not([data-theme="light"]) {
    --color-bg:         #0f172a;
    --color-surface:    #1e293b;
    --color-border:     #334155;
    --color-text:       #f1f5f9;
    --color-text-muted: #94a3b8;
    --color-primary:    #fb923c;
  }
}


/* =============================================
   BASE STYLES — Mobile first (no media query = mobile)
   ============================================= */

*,
*::before,
*::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  background-color: var(--color-bg);
  color: var(--color-text);
  font-size: var(--font-size-base);
  font-family: Georgia, "Times New Roman", serif;
  line-height: 1.6;
  transition: background-color 0.3s ease, color 0.3s ease;
}

.container {
  width: 100%;
  padding-inline: var(--space-4); /* Mobile: 16px side padding */
}

.grid {
  display: grid;
  grid-template-columns: 1fr;     /* Mobile: single column */
  gap: var(--space-4);
}

h1 { font-size: var(--font-size-2xl); }
h2 { font-size: var(--font-size-xl); }
h3 { font-size: var(--font-size-lg); }

.card {
  background: var(--color-surface);
  border: 1px solid var(--color-border);
  border-radius: var(--radius-md);
  padding: var(--space-4);
  box-shadow: var(--shadow-sm);
}

.btn-primary {
  background-color: var(--color-primary);
  color: white;
  padding: var(--space-3) var(--space-6);
  border: none;
  border-radius: var(--radius-md);
  font-size: var(--font-size-base);
  cursor: pointer;
  transition: background-color 0.2s ease;
}

.btn-primary:hover {
  background-color: var(--color-primary-hover);
}


/* =============================================
   TABLET — min-width: 768px
   ============================================= */

@media (min-width: 768px) {
  .container {
    padding-inline: var(--space-8); /* More breathing room */
    max-width: 768px;
    margin-inline: auto;
  }

  .grid {
    grid-template-columns: 1fr 1fr; /* Two columns on tablet */
    gap: var(--space-6);
  }

  h1 { font-size: var(--font-size-3xl); }
  h2 { font-size: var(--font-size-2xl); }

  .card {
    padding: var(--space-6);
    box-shadow: var(--shadow-md);
  }
}


/* =============================================
   DESKTOP — min-width: 1024px
   ============================================= */

@media (min-width: 1024px) {
  .container {
    max-width: 1100px;
    padding-inline: var(--space-12);
  }

  .grid {
    grid-template-columns: repeat(3, 1fr); /* Three columns on desktop */
    gap: var(--space-8);
  }

  h1 { font-size: var(--font-size-4xl); }
  h2 { font-size: var(--font-size-3xl); }
  h3 { font-size: var(--font-size-2xl); }

  .card {
    padding: var(--space-8);
    border-radius: var(--radius-lg);
    box-shadow: var(--shadow-lg);
    transition: transform 0.3s ease, box-shadow 0.3s ease;
  }

  .card:hover {
    transform: translateY(-4px);
    box-shadow: var(--shadow-lg);
  }
}
```