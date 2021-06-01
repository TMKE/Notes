# Switch Statement

Created by: Mohamed Kamel Eddine TAIBI
Date created: Nov 27, 2020 6:46 PM
Last edited time: Nov 27, 2020 7:55 PM
Status: completed

Use the `switch` statement to select one of many code blocks to be executed

```jsx
switch(expression) {
  case x:
    // code block
    break;
  case y:
    // code block
    break;
  default:
    // code block
}
```

### How it works?

1. The switch expression is evaluated once
2. The value is compared with the values of each case
3. If there's a match, the associated block is executed
4. If there's no match, the default block is executed

When the interpreter reaches a `break` keyword, it breaks out of the switch block

It's not necessary to break the last case because the block ends there anyway

If you omit the `break` statement, the next case will be executed even if the evaluation does not match the case

The `default` case doesn't have to be the last case in a switch block. If it's not the last then remember to end the default case with `break`

### Common code blocks

You can use the same code for different switch cases

```jsx
switch (new Date().getDay()) {
  case 3:
  case 4:
    text = "Soon it is Weekend";
    break;
  case 5:
  case 6:
    text = "It is Weekend";
    break;
  default:
    text = "Looking forward to the Weekend";
}
```

Switch cases use strict comparison `===`.
The values must be of the same type.