# Ternary operator

- A ternary operator is an *n*-ary operation with n = 3.
- A ternary operation on a set *A* takes any given three elements of *A* and combines them to form a single element of *A.*
- `?:` is a ternary operator that's part of the syntax for basic conditional expressions in several programming languages.
- `?:` is commonly referred to as the *conditional operator, inline if (iif),* or *ternary if*.
- An expression `a ? b : c` evaluates to **`b`** if the value of `a` is true, and otherwise to `c`. We can read it like this: "*if a then b otherwise c".*
- In Kotlin, the conditional operator works as follows: if the expression to the left of `?:` is not null, the Elvis operator returns it, otherwise it returns the expression to the right.

    ```kotlin
    val name = node.getOptionalName() ?: "default name"
    ```

    The right-hand side expression is evaluated only if the left-side is null

    [Elvis operator](Ternary%20operator%20a23eb19ac7064efc99bebb18471b38e3/Elvis%20operator%2018ca99b3c8ed4771aa2d09eee7a1ba0f.md)