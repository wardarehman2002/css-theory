Q1. What is CSS and how do you add it to an HTML page?
What does CSS stand for?

CSS stands for Cascading Style Sheets.

What is the purpose of CSS?

CSS is used to style and design web pages. HTML creates the structure of a webpage, while CSS controls how the webpage looks, including colors, fonts, spacing, layouts, and animations.

What problem does CSS solve?

Without CSS, webpages would look plain and difficult to use. CSS separates design from content, making websites easier to maintain and update.

Three Ways to Add CSS
1. Inline CSS

Inline CSS is written directly inside an HTML element using the style attribute.

<p style="color: blue;">Hello World</p>
2. Internal CSS

Internal CSS is written inside a <style> tag in the HTML document.

<style>
p {
  color: blue;
}
</style>
3. External CSS

External CSS is written in a separate .css file and linked to the HTML page.

HTML:

<link rel="stylesheet" href="style.css">

CSS:

p {
  color: blue;
}
Which Method is Recommended?

External CSS is recommended in professional projects because:

Keeps HTML clean
Makes maintenance easier
Reuses styles across multiple pages
Improves scalability
Reduces duplicate code
Why is External CSS Preferred Over Inline CSS?
External CSS	Inline CSS
Reusable	Not reusable
Easy to maintain	Hard to maintain
Cleaner code	Clutters HTML
Better for large projects	Only suitable for small changes
Code Examples of All Three Methods
Inline CSS
<p style="color:red;">Inline CSS Example</p>
Internal CSS
<head>
<style>
p {
  color: blue;
}
</style>
</head>
External CSS
<link rel="stylesheet" href="style.css">
p {
  color: green;
}
Q2. Explain CSS Selectors with Examples

CSS selectors are used to target HTML elements and apply styles.

1. Element Selector

Targets all elements of a specific type.

p {
  color: blue;
}
2. Class Selector

Targets elements with a specific class.

.card {
  border: 1px solid black;
}

HTML:

<div class="card">Content</div>
3. ID Selector

Targets a single element with a unique ID.

#header {
  background-color: lightgray;
}

HTML:

<div id="header">Header</div>
4. Group Selector

Targets multiple elements together.

h1, h2, h3 {
  color: navy;
}
5. Descendant Selector

Targets elements inside another element at any level.

div p {
  color: green;
}

Example:

<div>
  <section>
    <p>Selected</p>
  </section>
</div>
6. Child Selector

Targets direct children only.

div > p {
  color: red;
}

Example:

<div>
  <p>Selected</p>
</div>
7. Universal Selector

Targets all elements.

* {
  margin: 0;
  padding: 0;
}
Class vs ID
Class	ID
Can be reused	Must be unique
Lower specificity	Higher specificity
Used for groups	Used for one element
Which Has Higher Specificity?

ID selector has higher specificity than a class selector.

Direct Child vs Any Descendant

Any descendant:

div p

Direct child:

div > p
Can You Use the Same Class on Multiple Elements?

Yes.

<p class="text">Paragraph 1</p>
<p class="text">Paragraph 2</p>
Can You Use the Same ID on Multiple Elements?

No. IDs should be unique.

Code Task (All Seven Selectors)
/* Element */
p {
  color: blue;
}

/* Class */
.card {
  padding: 10px;
}

/* ID */
#header {
  background: gray;
}

/* Group */
h1, h2, h3 {
  color: navy;
}

/* Descendant */
div p {
  color: green;
}

/* Child */
div > p {
  font-weight: bold;
}

/* Universal */
* {
  margin: 0;
}
Q3. What is the CSS Box Model?

Every HTML element is treated as a rectangular box.

The CSS Box Model consists of four layers:

Margin
 └── Border
      └── Padding
           └── Content
1. Content

The content area contains text, images, and other information.

Example:

width: 300px;
height: 200px;
Which Layer is the Innermost?

Content is the innermost layer.

2. Padding

Padding creates space between the content and the border.

Example:

padding: 20px;
Is Padding Inside or Outside the Border?

Padding is inside the border.

3. Border

The border surrounds the padding and content.

Example:

border: 2px solid black;
4. Margin

Margin creates space outside the border.

Example:

margin: 20px;
What Does margin: 0 auto Do?

It horizontally centers a block element.

margin: 0 auto;
box-sizing Property
content-box (Default)

Width and height apply only to the content area.

box-sizing: content-box;

Example:

width: 300px;
padding: 20px;

Actual width becomes:

300 + 20 + 20 = 340px
border-box

Width includes content, padding, and border.

box-sizing: border-box;
With border-box, Does Width Include Padding?

Yes.

Padding and border are included inside the specified width.

Which One is Used in Professional Projects?

Most professional projects use:

box-sizing: border-box;

because it makes layouts easier to manage and calculate.

Code Task
.box {
  width: 300px;
  padding: 20px;
  border: 2px solid black;
  margin: 16px;
  box-sizing: border-box;
}
Q4. Explain CSS Colors. What are the different ways to define a color?

Colors are used in CSS to style text, backgrounds, borders, shadows, and other elements.

CSS provides several ways to define colors.

1. Named Colors

CSS has predefined color names.

h1 {
  color: orange;
}
Example
color: orange;
2. HEX Colors

HEX (Hexadecimal) colors start with # and contain six characters.

color: #F97316;
Format
#RRGGBB

Example:

color: #FF0000;
3. RGB Colors

RGB stands for Red, Green, Blue.

color: rgb(249, 115, 22);
Format
rgb(red, green, blue)

Each value ranges from 0–255.

4. RGBA Colors

RGBA is RGB with an Alpha channel.

color: rgba(249, 115, 22, 0.5);
What Does the "A" Stand For?

Alpha (transparency)

Values:

0   = fully transparent
1   = fully visible
5. HSL Colors

HSL stands for:

Hue
Saturation
Lightness
color: hsl(25, 95%, 53%);
Which Format Is Most Commonly Used?

Most developers commonly use:

HEX
RGB/RGBA

because they are widely supported and easy to work with.

Opacity vs RGBA
Opacity
opacity: 0.5;

Affects:

Element
Text
Images
Child elements

Everything becomes transparent.

RGBA
background: rgba(0, 0, 0, 0.5);

Only affects the color itself.

Child elements remain unchanged.

Does Opacity Affect Child Elements?

 Yes

Does RGBA Affect Child Elements?

 No

Code Task

Same Orange Color (#F97316) in All Formats

/* Named */
color: orange;

/* HEX */
color: #F97316;

/* RGB */
color: rgb(249, 115, 22);

/* RGBA */
color: rgba(249, 115, 22, 1);

/* HSL */
color: hsl(25, 95%, 53%);
Q5. What are CSS Units? Explain px, %, rem, em, vh, and vw.

CSS units are used to define sizes, spacing, widths, heights, and fonts.

1. px (Pixels)

Fixed-size unit.

font-size: 16px;
Use Case

Precise sizing of borders and icons.

2. % (Percentage)

Relative to the parent element.

width: 50%;
Use Case

Responsive layouts.

% Is Relative To?

 Parent Element

3. rem (Root Em)

Relative to the root (html) font size.

font-size: 2rem;
What Is 1rem Equal To By Default?
1rem = 16px

(Default browser size)

Use Case

Accessible typography.

4. em

Relative to the font size of the parent element.

font-size: 1.5em;
Use Case

Component-based spacing.

5. vh (Viewport Height)

Relative to viewport height.

height: 100vh;
What Does vh Stand For?

Viewport Height

Use Case

Full-screen hero sections.

6. vw (Viewport Width)

Relative to viewport width.

width: 50vw;
Use Case

Responsive sizing based on screen width.

Golden Rule for CSS Units
Font Sizes

Use:

rem

because it improves accessibility.

Widths

Use:

%

or

max-width

for responsive layouts.

Full-Screen Sections

Use:

100vh
Why Is rem Better Than px?

rem respects browser font settings and user accessibility preferences.

Users can zoom or increase text size more easily.

Code Task

Hero Section

.hero {
  height: 100vh;
  max-width: 75rem;
  margin: 0 auto;

  font-size: clamp(1.5rem, 4vw, 3rem);

  display: flex;
  justify-content: center;
  align-items: center;
}
Q6. What is CSS Specificity and how does the Cascade work?

When multiple CSS rules target the same element, the browser decides which rule wins.

This process is called:

Specificity
Cascade
Specificity

Specificity is a priority score assigned to selectors.

Higher specificity wins.

Specificity Scores
Selector	Score
Inline Style	1000
ID	100
Class	10
Element	1
Universal (*)	0
Which Has Higher Specificity?

Between:

.text

and

p

 Class selector wins.

What Specificity Score Does Inline Style Have?
1000

Highest normal specificity.

What Is the Cascade?

The cascade decides styles using:

1. Importance
!important
2. Specificity

Higher score wins.

3. Source Order

If specificity is equal, the last rule wins.

If Two Rules Have Equal Specificity?

The rule written later wins.

Example:

p {
  color: blue;
}

p {
  color: red;
}

Result:

color: red;
What Does !important Do?
color: red !important;

Overrides normal CSS rules.

Why Should It Be Avoided?
Hard to maintain
Causes debugging issues
Breaks normal cascade behavior
Code Task

HTML

<p id="intro" class="text">Hello</p>

CSS

p {
  color: blue;
}

.text {
  color: green;
}

#intro {
  color: red;
}
Which Color Wins?
#intro

because ID specificity (100) is higher than:

Class (10)
Element (1)

Final color:

Red
Q7. Explain CSS Flexbox. How does it differ from block layout?

Flexbox (Flexible Box Layout) is a one-dimensional layout system used to arrange items in rows or columns.

Normally, block elements appear one below another. Flexbox gives us better control over alignment, spacing, and positioning.

What does display: flex do?

When display: flex is applied to a container, all direct child elements become flex items.

.container {
  display: flex;
}
flex-direction

Controls the direction of flex items.

Row (Default)
.container {
  display: flex;
  flex-direction: row;
}
Column
.container {
  display: flex;
  flex-direction: column;
}
justify-content

Aligns items along the main axis.

.container {
  display: flex;
  justify-content: center;
}

Common values:

flex-start
center
flex-end
space-between
space-around
space-evenly
align-items

Aligns items along the cross axis.

.container {
  display: flex;
  align-items: center;
}
Difference Between justify-content and align-items
Property	Controls
justify-content	Horizontal alignment (row layout)
align-items	Vertical alignment (row layout)
flex-wrap

Controls whether items stay on one line or move to a new line.

.container {
  display: flex;
  flex-wrap: wrap;
}
What does flex-wrap: wrap do?

It allows items to move onto the next line when there is not enough space.

gap

Adds space between flex items.

.container {
  gap: 20px;
}
flex: 1
.item {
  flex: 1;
}
What does flex: 1 do?

It allows items to grow equally and share available space.

How to Center an Element Horizontally and Vertically
.container {
  display: flex;
  justify-content: center;
  align-items: center;
}
Real-World Use Cases
Navigation Bar
Logo on left
Menu on right
Card Layout
Product cards
Feature sections
Code Task: Flexbox Navbar
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;

  padding: 16px 32px;
}

.nav-links {
  display: flex;
  gap: 20px;
}
Q8. What are CSS Pseudo-classes and Pseudo-elements?

Pseudo-classes and pseudo-elements allow styling based on state or virtual content.

Difference Between Them
Pseudo-class (:)

Styles an element based on its state.

Examples:

:hover
:focus
:nth-child()
:not()
Pseudo-element (::)

Styles part of an element or adds virtual content.

Examples:

::before
::after
::placeholder
:hover

Applies styles when the mouse is over an element.

button:hover {
  background: orange;
}
:focus

Applies styles when an input receives focus.

input:focus {
  border-color: blue;
}
:nth-child()

Targets elements based on position.

li:nth-child(2n) {
  background: lightgray;
}
:nth-child(2n) Selects Which Elements?

Selects:

2nd
4th
6th
8th
...

All even-numbered elements.

How to Style Every 3rd List Item?
li:nth-child(3n) {
  color: red;
}
:not()

Targets elements that do NOT match a selector.

p:not(.active) {
  color: gray;
}
::before

Adds virtual content before an element.

.featured::before {
  content: "★ ";
}
::after

Adds virtual content after an element.

.featured::after {
  content: " New";
}
::placeholder

Styles placeholder text.

input::placeholder {
  color: gray;
}
Does ::before Add a Real HTML Element?

 No

It creates virtual content only.

What Property Is Required?
content: "";

Without the content property, ::before and ::after will not appear.

Code Task
button:hover {
  background-color: orange;
}

.featured::before {
  content: "H ";
}

input::placeholder {
  color: gray;
}
Q9. Explain CSS Transitions and Animations

CSS can create animations without JavaScript.

Transition vs Animation
Transition

Moves smoothly from one state to another.

Needs a trigger.

Example:

button:hover {
  background: orange;
}
Animation

Runs automatically using keyframes.

animation: fadeIn 1s ease;
Transition Shorthand
transition: property duration timing-function delay;

Example:

transition: all 0.3s ease 0s;
Timing Functions
ease

Starts slow, speeds up, slows down.

transition-timing-function: ease;
ease-in

Starts slowly.

transition-timing-function: ease-in;
ease-out

Ends slowly.

transition-timing-function: ease-out;
linear

Same speed throughout.

transition-timing-function: linear;
Common Transition Triggers
hover
focus
active
checked
Can You Have Multiple Transitions?

Yes.

transition:
  transform 0.3s ease,
  box-shadow 0.3s ease;
@keyframes

Defines animation stages.

@keyframes fadeIn {
  from {
    opacity: 0;
  }

  to {
    opacity: 1;
  }
}
Animation Shorthand
animation: fadeIn 1s ease 0s 1 forwards;
animation-fill-mode: forwards
animation-fill-mode: forwards;

Keeps the final animation state after completion.

animation-iteration-count: infinite
animation-iteration-count: infinite;

Repeats forever.

Why Is Transform Faster Than Width?

transform uses GPU acceleration and does not trigger layout recalculations.

Properties like:

width
margin
height

are slower because they force the browser to recalculate layouts.

Code Task
.card {
  padding: 20px;
  transition:
    transform 0.3s ease,
    box-shadow 0.3s ease;

  animation: fadeUp 0.8s ease forwards;
}

.card:hover {
  transform: translateY(-10px);

  box-shadow: 0 10px 20px rgba(0,0,0,0.2);
}

@keyframes fadeUp {
  from {
    opacity: 0;
    transform: translateY(20px);
  }

  to {
    opacity: 1;
    transform: translateY(0);
  }
}
Q10. Responsive Web Design, Media Queries, CSS Variables & Mobile-First

Responsive Web Design ensures websites work properly on all screen sizes.

Part A: Media Queries
What is a Media Query?

A media query applies CSS only when specific conditions are met.

Syntax:

@media (min-width: 768px) {
  /* CSS */
}
Standard Industry Breakpoints
Device	Width
Mobile	0–767px
Tablet	768px+
Laptop	1024px+
Desktop	1280px+
Part B: Mobile-First Approach

Mobile-first means designing for mobile screens first and then adding styles for larger screens.

Why Is Mobile-First Preferred?
Better performance
Better user experience
Easier scaling
Industry standard
Mobile-First Uses Which Media Query?

 min-width

Example:

@media (min-width: 768px) {
}
Desktop-First Uses
max-width
Part C: CSS Variables

CSS Variables are custom properties that store reusable values.

Define Variables
:root {
  --primary-color: #F97316;
  --spacing: 16px;
}
Use Variables
button {
  background: var(--primary-color);
}
var() with Fallback
color: var(--text-color, black);
Difference
var(--color)

Uses variable only.

var(--color, black)

Uses black if variable is missing.

Dark Mode
[data-theme='dark'] {
  --bg-color: #121212;
  --text-color: white;
}
What Does prefers-color-scheme: dark Do?

Automatically detects if the user prefers dark mode.

@media (prefers-color-scheme: dark) {
}
Can JavaScript Read and Change CSS Variables?

 Yes

JavaScript can access and modify CSS custom properties.

Code Task
:root {
  --primary-color: #F97316;
  --background-color: white;
  --text-color: black;

  --font-size-base: 1rem;

  --spacing-sm: 0.5rem;
  --spacing-md: 1rem;
  --spacing-lg: 2rem;
}

body {
  background: var(--background-color);
  color: var(--text-color);

  font-size: var(--font-size-base);
}

[data-theme='dark'] {
  --background-color: #121212;
  --text-color: #ffffff;
}

.card {
  padding: var(--spacing-md);
}

@media (min-width: 768px) {
  .container {
    max-width: 720px;
  }
}

@media (min-width: 1024px) {
  .container {
    max-width: 960px;
  }
}