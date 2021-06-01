# How to get elements inside a <div>

Created by: Mohamed Kamel Eddine TAIBI
Date created: Nov 28, 2020 6:53 PM
Last edited time: Nov 28, 2020 7:00 PM
Status: completed

Let's take `<button>` elements as an example.

```html
<div class="keys">
    <button id="a"></button>
    <button id="b"></button>
</div>
```

We can get CSS selector for any element using developer tools. Right click the element in the developer tools window, then copy CSS selector. In our example:

```jsx
let buttonA = document.querySelector('.keys > button:nth-child(1)');
let buttonB = document.querySelector('.keys > button:nth-child(2)');
```