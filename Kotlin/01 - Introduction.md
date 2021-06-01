# 01 - Introduction

## Variable declaration

We use two different keywords to declare variables *(two types of variables)*: `val` and `var`.

- `val` is used for a variable whose value never changes (unchangeable). You can't reassign a value to a variable that was declared using `val`.
- `var` is used for a variable whose value can change (changeable).

```kotlin
var count: Int = 10
count = 15

val languageName: String = "Kotlin"
// The value of languageName cannot be changed
```

Kotlin coding style prefers immutable data when possible.

## Type inference

When you assign a value to a variable, the Kotlin compiler infers the type based off of the type of the assigned value.

Kotlin is a *statically-typed* language. This means that the type is resolved at compile time and never changed.

```kotlin
val languageName = "Kotlin"
val upperCaseName = languageName.toUpperCase()

// Fails to compile
languageName.inc()
```

Because `toUpperCase()` is a function that can only be called on a `String`, you can safely call it. `inc()`, however, is an `Int` operator function, so it can't be called on a `String`.

- Numbers

    Six types: `Int`, `Byte`, `Short`, `Long`, `Float` and `Double`.

    Kotlin keeps numbers as primitives, but it lets you call methods on numbers as if they were objects. Examples: `2.times(3)`, `3.5.plus(4)`, `2.4.div(2)`, etc.

    It's possible to create actual object wrappers around numbers (boxing), but it takes more memory than storing just a number primitive. Thus, do not use boxing unless it is needed (such as in a collection).

    Kotlin does not implicitly convert between number types, so you can't assign a short value directly to a long variable, or a Byte to an Int. This is because implicit number conversion is a common source of errors in programs. You can always assign values of different types by casting.

    ```kotlin
    val i1: Int = 6
    val b1 = i.toByte()

    val b2: Byte = 1
    val i2: Int = b2.toInt()
    ```

    Kotlin allows placing underscores in numbers.

    ```kotlin
    val oneMillion = 1_000_000
    val socialSecurityNumber = 999_99_9999L
    val hexBytes = 0xFF_EC_DE_5E
    val bytes = 0b11010010_01101001_10010100_10010010
    ```

- Strings
    - `"`: for strings
    - `'`: for single characters
    - `+`: concatenation
    - `$`: variable interpolation (create string template)

        Use curly braces `{}` for expressions.

## Null safety

In some languages, a reference type variable can be declared without providing an initial explicit value. In these cases, the variables usually contain a null value.

Kotlin variables can't hold null values by default.

```kotlin
// Fails to compile
val languageName: String = null
```

For a variable to hold a null value, it must be of a nullable type. 

```kotlin
val languageName: String? = null
```

`?` as a suffix specifies a variable as being nullable

You must handle nullable variables carefully or risk a dreaded `NullPointerException`. In Java, for example, if you attempt to invoke a method on a null value, your program crashes.

When you have complex data types, such as a list:

- you can allow the elements of the list to be null.
- you can allow for the list to be null, but if it's not null its elements cannot be null.
- you can allow both the list and its elements to be null.

## Conditionals

```kotlin
if (count == 42) {
    println("I have the answer.")
} else if (count > 35) {
    println("The answer is close.")
} else {
    println("The answer eludes me.")
}
```

Conditional statements are useful, but you may find that you repeat yourself when writing them. In the example above, you simply print a `String` in each branch. To avoid this repitition, Kotlin offers *conditional expressions.* 

```kotlin
val answerString: String = if (count == 42) {
    "I have the answer."
} else if (count > 35) {
    "The answer is close."
} else {
    "The answer eludes me."
}

println(answerString)
```

Implicitly, *each conditional branch returns the result of the expression of its final line*, so you don't need to use a `return` keyword.

Type inference can be used to omit the explicit type declaration for `answerString`, but it's often a good idea to include it for clarity.

Kotlin doesn't include a traditional ternary operator, instead favoring the use of conditional expressions

[Ternary operator](01%20-%20Introduction%20505d392610ab461d90776fc571c32235/Ternary%20operator%20a23eb19ac7064efc99bebb18471b38e3.md)

As the complexity of our conditional statement grows, we might consider replacing the if-else expression with a *when* expression.

```kotlin
val answerString = when {
    count == 42 -> "I have the answer."
    count > 35 -> "The answer is close."
		count in 0..35 -> "You are far"
    else -> "The answer eludes me."
		// condition -> result
}

println(answerString)
```

We can use *smart casting* rather than using the *safe-call operator* or the *not-null assertion operator* to work with nullable values. We can check if a variable contains a reference to a null value using a conditional statement.

```kotlin
val languageName: String? = null

// safe-call operator (kotlin way)
println(languageName?.toUpperCase())

// not-null assertion operator

// smart casting
if (languageName != null) {
    // No need to write languageName?.toUpperCase()
    println(languageName.toUpperCase())
}
```

The *smart casting* works for null checks, type checks, or any condition that satisfies a contract.

[***The elvis operator***](01%20-%20Introduction%20505d392610ab461d90776fc571c32235/The%20elvis%20operator%20885684b2bde94eaaa0d3a719d542fe32.md)

[Type checks & casts](01%20-%20Introduction%20505d392610ab461d90776fc571c32235/Type%20checks%20&%20casts%20f16f8aab41704065afc82a929936d8cc.md)

### Iterating through range

```kotlin
for(i in 1..5) print(i)

for(i in 5 downTo 1) print(i)

for(i in 5 downTo 1 step 2) print(i)

repeat(2) {
     println("A fish is swimming")
}
```

### Jump expressions

A **break** expression is used to terminate the nearest enclosing loop.

It's almost used with if-else condition

```kotlin
fun main(args: Array<String>) {  
    for (i in 1..5) {  
        if (i == 3) {  
            break  
        }  
        println(i)  
    }  
}
```

We can make an expression as label. we just put the label in front of expression (a label is an identifier followed by `@`).

Kotlin labeled beak expression is used to terminate a specific loop.

```kotlin
fun main(args: Array<String>) {  
    loop@ for (i in 1..3) {  
        for (j in 1..3) {  
            println("i = $i and j = $j")  
            if (i == 2)  
                break@loop  
        }  
    }  
}
```

The **continue** statement is used to skip the remaining code at specified condition. It only affects the inner loop.

```kotlin
fun main(args: Array<String>) {  
    labelname@ for (i in 1..3) {  
    for (j in 1..3) {  
        println("i = $i and j = $j")  
        if (i == 2) {  
            continue@labelname  
        }  
        println("this is below if")  
    }  
 }  
}
```

### Tail recursion

The compiler is unable to call large number of recursive function call and throws an exception of `java.lang.StackOverflowError`.

Here comes **tail recursion**, which performs the calculation first, then makes the recursive call. The recursive call must be the last call of the method.

```kotlin
fun main(args: Array<String>) {  
    var number = 100000.toLong()  
    var result = recursiveSum(number)  
    println("sum of $number number = $result")  
}  
tailrec fun recursiveSum(n: Long, semiresult: Long = 0) : Long {  
    return if (n <= 0) {  
        semiresult  
    } else {  
        recursiveSum( (n - 1), n+semiresult)  
    }  
}
```

To declare a recursion as tail recursion we need to use `tailrec` modifier before the recursive function