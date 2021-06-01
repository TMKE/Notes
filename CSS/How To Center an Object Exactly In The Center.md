# How To Center an Object Exactly In The Center

Give the element the class of `.centered` and then style that class:

```css
.centered {
	position: fixed;
	top: 50%;
	left: 50%;
	transform: translate(-50%, -50%);
}
```

The `translate` value for `transform` is based off the size of the element, so that will center nicely. If we don't use it, the element will not be centered correctly.
