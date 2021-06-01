# Introduction

Created by: Mohamed Kamel Eddine TAIBI
Date created: Nov 26, 2020 2:22 PM
Last edited time: Nov 28, 2020 6:28 PM
Status: completed

# What is it?

- A full-fledged ***dynamic*** programming language
- Adds ***interactivity*** to a website
- Many tools are written on top of the core JavaScript language, such as:
    - ***Browser Application Programming interfaces*** (APIs) built into web browsers, used for:
        - ***creating HTML and setting CSS styles***
        - ***collecting and manipulating a video stream from a user's webcam***
        - ***generating 3D graphics and audio samples***
    - ***Third-party APIs***, which allow developers to incorporate functionality in sites from other content providers, such as Twitter and Facebook
    - ***Third-party frameworks*** and libraries that can be applied to HTML to accelerate the work of building websites and applications

Before closing `</body>` tag, enter this code to apply JS to the page:

```html
<script src="scripts/main.js"></script>
```

Putting the `<script>` element near the bottom of the HTML file is because the browser reads code from top to bottom.
If the JavaScript loads first and it is supposed to affect the HTML that hasn't loaded yet, there could be problems.

### Variables

```jsx
// Declaring variables
let v1;
var v2;
// Declaring a variable and assigning a value to it
let v3 = "Hello";
// Retrieving a variable's value
v3;
// Changing a variable's value
v3 = "Hi";
```

`var` is less recommended, use `let` instead

A semicolon is only required to separate statements on a single line

JavaScript is case sensitive

[Data types](Introduction%2079cf715f19ef41499351f986faa0e9da/Data%20types%204862109377f34f01956f911e3f91f2b2.csv)

### Operators

[Different operators](Introduction%2079cf715f19ef41499351f986faa0e9da/Different%20operators%209fb1bc51530d4d3ba1445947bc0a3940.csv)

Mixing data types can give unexpected results

### Conditionals

```jsx
let iceCream = 'chocolate';
if(iceCream === 'chocolate') {
  alert('Yay, I love chocolate ice cream!');    
} else {
  alert('Awwww, but chocolate is my favorite...');    
}
```

### Functions

```jsx
function multiply(num1,num2) {
  let result = num1 * num2;
  return result;
}
```

`return` statement returns the `result` variable out of the function so it's available to use outside. This is necessary because variables inside functions are not accessible outside the functions ***(variable scoping)***

### Events

***Events handlers***: code structures that listen for activity in the browser, and run code in response.

```jsx
document.querySelector('html').onclick = function() {};
```

The above code is equivalent to:

```jsx
let myHTML = document.querySelector('html');
myHTML.onclick = function() {};
```