# Introduction

### What's is it?

- HTML stands for *(HyperText Markup Language)*
    - ***HyperText***: links that connect web pages to one another
    - ***Markup***: annotate text, images and other contents for display in a Web browser. It includes special "elements" such as `<head>`, `<title>`, ... used to enclose, or wrap, different parts of the content to make it appear or act in a certain way
    - "`<`" and "`>`" (tags) set off an element from other text in a document. The name of an element inside a tag is case insensitive
- HTML defines the structure of web content

### Anatomy of an HTML element

Different parts of an HTML element

- *Opening tag: states where the element begins*
- *Closing tag: states where the elements ends*

### Attributes

Attributes contain extra information about the element

An attribute should always have:

1. the attribute ***name*** followed by an equal sign
2. the attribute ***value*** wrapped by opening and closing quotation marks

**`class`** is the attribute **name** and `**editor-note**` is the attribute **value**

The **`class`** attribute allows you to give the element a non-unique identifier that can be used to target it *(and any other elements with the same **`class`** value)* with style information and other things

### Nesting elements

**Nesting**: putting elements inside other elements

```html
<p>My cat is <strong>very</strong> grumpy.</p>
```

The elements have to open and close correctly so that they are clearly inside or outside one another

### Empty elements

They have no content, like the `**<img>**` element:

```html
<img src="images/firefox-icon.png" alt="My test image">
```

There is no closing `**</img>**` tag and no inner content because an image element doesn't wrap content to affect it

`**src**` (source) attribute contains the path to the image file, `**alt**` (alternative) attribute give descriptive text for users who cannot see the image *(they are visually impaired, so they use screen readers, or the path in `**src**` is incorrect)*

### Anatomy of an HTML document

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>My test page</title>
  </head>
  <body>
    <img src="images/firefox-icon.png" alt="My test image">
  </body>
</html>
```

- **`<!DOCTYPE html>`**: needed to make sure your document behaves correctly
- **`<html></html>`**: (root element) wraps all the content on the entire page
- **`<head></head>`**: contains keywords, page descriptions that you want to appear in search results, CSS, character set declarations, and more
- **`<meta charset="utf-8">`**: UTF-8 is the character set which includes most characters from the vast majority of written languages
- **`<title></title>`**: sets the title that appears in the browser tab
- **`<body></body>`**: contains the content showed in the page

### Marking up text

- Headings
    - There are 6 heading levels,`**<h1>**`-`**<h6>**`
    - They are used for accessibility and SEO
- Paragraphs `**<p>**`
- Lists
    1. **Unordered lists**: wrapped in `**<ul>**`
    2. **Ordered lists**: wrapped in `**<ol>**`
    3. Each item inside the lists is put inside an `**<li>**` *(list item)* element

### Links

- Using `**<a>**` *(anchor)*
- Using the attribute `**href**` *(hypertext reference)* and filling its value with the web address