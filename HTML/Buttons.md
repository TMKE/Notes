# Buttons

The `<button>` tag defines a clickable button.

```html
<button type="button">Click here</button>
```

We can define buttons using `<input>` element

```html
<form>
	<input type="button" value="Click here">
</form>
```

Inside a `<button>` element, you can put text or tags (like `<i>`, `<img>`, ...). This is not possible with a button created with the `<input>` element

[Attributes](Buttons%201cac04fbcd2b4b48920428e439a86954/Attributes%206f449b00c8c04833bf50db50db3e8167.csv)

The `<button>` tag also supports global and event attributes in HTML

There are some attributes specific to a button with `type="submit"` like: `formaction`, `formenctype`, `formmethod`, `formnovalidate`and `formtarget`

Always specify the type attribute for a `<button>` element, to tell browsers what type of button it is

### Aligning buttons to the center (using CSS)

```css
button {
	margin: auto;
	dispaly: block;
}
```