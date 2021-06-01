# Resume

## Introduction

- Kotlin is a modern language with:
    - robust (firm, solid, or sturdy) code
        - distinguishing between nullable and non-nullable data types, which help catch more errors at compile time
        - strongly typed, which means, a variable will not be automatically converted from one type to another (weakly typed is the opposite)
        - statically typed, which means the compiler figures out the type of each variable at compile time (dynamically typed is the opposite)
        - type inference
        - lambdas
        - coroutines
        - properties
        - etc.
    - mature platform (since 2011)
    - concise (short), readable code
    - Interoperable with Java
- `java -version` & `javac -version` to verify JDK installation
- REPL (Read-Eval-Print Loop) is Kotlin's interactive shell

## Basics

- Kotlin has two types of variables:
    - `val`: used for unchangeable values
    - `var`: used for changeable values

    Kotlin code style prefers immutable data when possible

- Kotlin compiler infers the type based off of the type of the assigned value
- Numbers:
    - 6 types: `Int`, `Byte`, `Short`, `Long`, `Double`, and `Float`.
    - Kotlin doesn't impicitly convert between number types (source of errors).
    - Conversion functions: `toByte()`, `toInt()`, etc.
    - Kotlin allows placing underscores in numbers.
- Strings and chars:
    - `"`: for strings
    - `'`: for single characters
    - `+`: concatenation
    - `$`: variable interpolation (create string template)

        Use curly braces `{}` for expressions.

- Conditionals:
    - Implicitly, each conditional branch returns the result of the expression of its final line.
    - There's no traditional ternary operator in Kotlin (i.e. `a ? b : c`)
    - If the expression to the left of `?:` (Elvis operator) is not null, the operator returns it, otherwise it returns the expression to the right. e.g. `val l: Int = b?.length ?: -1`.
    - `throw` & `return` are expressions, so they can also be used on the right hand side of the elvis operator.
    - We use `when` expression when the complexity of the conditional statement grows.
- Null safety:
    - Kotlin variables can't hold null values by default.
    - `?` as a suffix specifies a variable as being nullable. e.g. `val name: String? = null`.
    - If you attempt to invoke a method on a null value, your program crashes (handle the `NullPointerException`).
    - Safe-call operator `?`:
        - Useful in chains.

        ```kotlin
        bob?.department?.head?.name
        ```

        ```kotlin
        println(name?.toUpperCase())
        ```

        - To perform an operation only for non-null values, use the safe call operator together with `let`:

        ```kotlin
        val listWithNulls: List<String?> = listOf("Kotlin", null)
        for (item in listWithNulls) {
            item?.let { println(it) } // prints Kotlin and ignores null
        }
        ```

    - Not-null assertion operator `!!`:
        - Converts any value to a non-null type and throws an exception (NPE) if the value is null.
        - Not ideal but needed when dealing with legacy Java code.

        ```kotlin
        val l = name!!.length
        ```

    - Smart casting:
        - Works for null checks, type checks, or any condition that satisfies a contract.
        - Does not work when the compiler cannot guarantee that the variable cannot change between the check and the usage (the variable is mutable).

        ```kotlin
        if (name != null) {
            // No need to write languageName?.toUpperCase()
            println(name.toUpperCase())
        }
        ```

    - We can filter non-null elements from a collection of nullable type by using `filterNotNull()`.

        ```kotlin
        val nullableList: List<Int?> = listOf(1, 2, null, 4)
        val intList: List<Int> = nullableList.filterNotNull()
        ```

- Type checks:
    - `is` & `!is` are used to check if an object conforms to a given type at runtime.
    - Casts happen automatically:
        - if a negative check leads to a return.
        - `is`-checks.
        - right-hand side of `&&` and `||`.
    - Unsafe cast operator `as`:
        - It's unsafe (because it throws `ClassCastException` if the cast is not possible).

        `null` cannot be cast to `String` as this type is not nullable.

        ```kotlin
        val x: String? = y as String?
        ```

    - Safe cast operator `as?`:
        - Returns `null` on failure.

        ```kotlin
        val x: String? = y as? String
        ```

- Iterations: `..`, `downTo`, `step`, and `repeat`.
- Jump expressions:
    - `break`:
        - Terminate the nearest loop.
        - Used with if-else condition.
        - We can terminate a specific loop using labels.

            ```kotlin
            boucle@ for (i in 1..5) {
            		for (j in 4..9) {
            				if (i == 2) break@boucle
            		}
            }
            ```

    - `continue`:
        - Skip the remaining code at specified condition.
        - We can also use labels here.
- Tail recursion
    - Normal recursion with a large number of calls throws `java.lang.StackOverflowError`.
    - Tail recursion performs calculations first, then make the recursive call.
    - Use `tailrec` before the declaration of recursive functions.

## Functions

- Single-expression (compact) functions (no `{}`, but `=`).

    ```kotlin
    fun sum(a: Int, b: Int) = a + b
    ```

- `main()` function:
    - Returns `Kotlin.Unit`.
    - As of Kotlin 1.3, the `main()` function doesn't use any parameters.
- Everything in Kotlin returns a value, except loops.
- Functions with block body must always specify return types explicitly, unless it's intended for them to return `Unit`.
- Calling member functions:

    ```kotlin
    Stream().read() // create instance of class Stream and call read()
    ```

- A default argument can be a value or another function.
- A function used as a default value is evaluated at runtime.
- Default arguments should be put at the end.

We can't use named arguments with Java functions. Bytecode does not preserve names of function parameters.

- When overriding a method with default parameter values, the values must be omitted from the signature.
- Lambdas:
    - Objects.
    - Identified by their input and output.
    - Can be passed as data.
    - The parameters go on the left of what is called a function arrow `->`. The code to execute goes to the right of `->`.
    - We can keep a reference to a lambda.
    - The return value of a lambda is the result of the final expression.
    - We can use the `::` operator when passing the function reference as an argument.
- Higher-order functions:
    - Use or return other functions.
    - Any parameter that takes a function should be put at the end (last call parameter syntax).
- Inline functions:
    - Enhances the performance of higher-order functions.
    - We can exit from the function and lambda expression itself by the `return` keyword.
    - To prevent the `return`, we can mark the lambda as `crossinline`. It throws a compiler error if we add a `return` inside that lambda.
    - Inlining large functions does increase your code size (extra objects created, incurring overhead memory and cpu time).
    - Inlining can help reduce ressource usage.