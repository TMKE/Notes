# Introduction

# What is it?

- CSS stands for ***Cascading Style Sheets***
- It's used for ***describing the presentation*** of a ***document written in markup language*** such as HTML

To apply CSS to HTML, paste the following line in the head:

```html
<link href="styles/style.css" rel="stylesheet">
```

The browser is used to display documents visually. It is sometimes called a ***user agent*** *(a computer program that represents a person inside a computer system)*. It's the main type of user agent we think of when talking about CSS, however, it's not the only one. There are others - such as those which convert HTML and CSS documents into PDFs to be printed.

### Anatomy of a CSS ruleset

The whole structure is called a ruleset

- Selector: The HTML element to be styled
- Declaration: A single rule. It specifies which of the element's properties you want to style
- Property: The way in which you can style an HTML element
- Property value: This chooses one out of many possible appearances for a given property
- `{}` wrap the ruleset
- `:` separate the property from its value or values
- `;` separate each declaration from the next one

If a property is unknown, or if a value is not valid for a given property, the declaration is processed as invalid. *It is completely ignored by the browser's CSS engine*.

US spelling is the standard where there is language variation or uncertainty. For example, `colour` will not work.

### Selecting multiple elements

You can apply a single ruleset to multiple elements. Separate multiple selectors by commas:

```css
p, li, h1 {
  color: red;
}
```

### Selecting element nested inside an other one

```css
li em {
	color: rebeccapurple;
}
```

### Adjacent sibling combinator

```css
h1 + p {
	font-size: 200%;
}
```

### Styling things based on state

```css
a:link {
	color: pink;
}

a:visited {
	color: green;
}

a:hover {
	text-decoration: none;
}
```

### Combining selectors and combinators

```css
/* selects any <span> that is inside a <p>, which is inside an <article>  */
article p span { ... }

/* selects any <p> that comes directly after a <ul>, which comes directly after an <h1>  */
h1 + ul + p { ... }
```

### Different types of selectors

[Selectors](Introduction%2061deb63f8845425c8693b0151a5c56b8/Selectors%20f8c557a98a0c4441bdd7a0025c356a8f.csv)

### Functions

There are some values that take the form of a function.

```html
<div class="outer">
	<div class="box">The inner box is 90% - 30px.</div>
</div>
```

```css
.outer {
  border: 5px solid black;
}

.box {
  padding: 10px;
  width: calc(90% - 30px);
  background-color: rebeccapurple;
  color: white;
}
```

This renders as:

# CSS modules

CSS is broken down into modules. For example, Backgrounds and Borders module contains different properties and features.

It is easier to find information if you are aware that a certain property is likely to be found among other similar things and are therefore probably in the same specification.

***Example***: It makes logical sense for the `background-color` and `border-color` properties to be defined in Backgrounds and Borders module

### CSS specifications

All web standards technologies *(HTML, CSS, JavaScript, etc.)* are defined in giant documents called ***specifications*** *(or simply "specs")*, which are published by standards organizations (such as the W3C, WHATWG, ECMA, or Khronos) and define precisely how those technologies are supposed to behave.

New CSS features are developed, or specified, by the CSS Working Group, which is a group within the W3C, made of representatives of browser vendors and invited experts.

# Browser support

It's unusual for all browsers to implement a feature at the same time, and so there is usually a gap where you can use some part of CSS in some browsers and not in others. For this reason, being able to check implementation status is useful.

# @rules

CSS @rules (at-rules) provide instruction for what CSS should perform or how it should behave.

```css
@import 'style2.css';
```

`@media` is used to create media queries. They use conditional logic for applying CSS styling.

```css
body {
  background-color: pink;
}

@media (min-width: 30em) {
  body {
    background-color: blue;
  }
}
```

`@media` can be used to increase the font size on larger screens or windows for better readability.

# Shorthands

Shorthand properties set several values in a single line.

```css
padding: 10px 15px 15px 5px;
```

This is the equivalent of these four lines of code:

```css
padding-top: 10px;
padding-right: 15px;
padding-bottom: 15px;
padding-left: 5px;
```

This one line:

```css
background: red url(bg-graphic.png) 10px 10px repeat-x fixed;
```

is equivalent to these five lines:

```css
background-color: red;
background-image: url(bg-graphic.png);
background-position: 10px 10px;
background-repeat: repeat-x;
background-attachment: fixed;
```

# Comments

Add comments to your code.

# Fonts and text

In the `<head>` element in the HTML document:

```html
<link href="https://fonts.googleapis.com/css?family=Open+Sans" rel="stylesheet">
```

```css
html {
  font-size: 10px; /* px means "pixels" */
  font-family: "Open Sans", sans-serif; /* this should be the rest of the output you got from Google fonts */
}

h1 {
  font-size: 60px;
  text-align: center;
}

p, li {
  font-size: 16px;    
  line-height: 2;
  letter-spacing: 1px;
}
```

# Box model

Each box (element) taking up space on your page has properties like:

- `padding`, the space around the content
- `border`, the solid line that is just outside the padding
- `margin`, the space around the outside of the border

```css
html {
	/* changing the page color */
  background-color: #00539F;
}

body {
	/* forces the body to always be 600 pixels wide */
  width: 600px;
  margin: 0 auto;
  background-color: #FF9500;
  padding: 0 20px 20px 20px;
  border: 5px solid black;
}

h1 {
  margin: 0;
  padding: 20px 0;    
  color: #00539F;
  text-shadow: 3px 3px 1px black;
}

img {
  display: block;
  margin: 0 auto;
}
```

When you set two values on a property like `margin` or `padding`, the first value affects the element's top and bottom side; the second value affects the left and right side

When you set four values, the order is: top, right, bottom, left

`text-shadow` applies a shadow to the text content of the element; the first pixel value sets the horizontal offset, the second pixel value sets the vertical offset, the third pixel value sets the blur radius, and the forth value sets the base color of the  shadow

The `<body>` is a ***block*** element, meaning it takes up space on the page.
A block element can have margin and other spacing values applied to it

Images are ***inline*** elements, it's not possible to apply margin or spacing values to them (we must give the image block-level behavior using `display: block;`)

Further reading:

[Block-level & Inline Elements](https://www.notion.so/Block-level-Inline-Elements-8aa4b4c026db44e9ab52b4ca2ef530b5)