# Block-level & Inline Elements

For the purpose of styling, elements are divided into two categories: ***block-level*** elements and ***inline*** elements.

In summary, a `<span>` element is used as an inline element and a `<div>` element as a block level element.

- ***Inline element***: does not cause a line break and does not take up the entire space of the parent (*container*), only occupying the space as needed within the space defined by the main element. *It's usually used within other HTML elements*. *Examples*: `<a>` (*anchor*), `<em>` (*emphasis*), `<img>`,`<span>`, `<code>`, `<cite>`, `<button>`, `<input>` etc.
- ***Block-level element***: always starts on a new line and takes up the entire space of the parent (*container*). A block-level element can take up *one line* or *multiple lines* and has a line break before and after the element. *Examples*: `<h1>` to `<h6>`, `<blockquote>`, `<pre>` (*pre-formatted text*), `<div>`, `<p>`, `<article>`, `<section>`, `<figure>` etc.

The `<div>` element is usually used as a *container for other HTML elements* and to separate them from the rest. The `<div>` element is an un-styled tag (it does not change the look of an HTML element).

The `<span>` element can be used as a *container for HTML text*. But essentially, it is used to style a certain text within a larger text element. The `<span>` element does not automatically style an HTML element.

`<div>` & `<span>` do not require attributes

Block-level elements may contain other block-level or inline element. Inline elements cannot contain block-level elements