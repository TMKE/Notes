# 02 - Functions

```kotlin
fun sum(a: Int, b: Int): Int {
	return a + b
}
```

Parameters are defined using Pascal notation (i.e. *name: type*) and separated with commas

### Single-expression functions (compact)

```kotlin
fun sum(a: Int, b: Int) = a + b
```

This function is called a single-expression function. The curly braces are omitted and the body is specified after a `=` symbol.

Explicitly declaring the return type is optional when this can be inferred by the compiler

```kotlin
fun printSum(a: Int, b: Int): Unit {
	println("sum of $a and $b is ${a + b}")
}
```

### Making compact functions

```kotlin
fun shouldChangeWater (day: String, temperature: Int = 22, dirty: Int = 20): Boolean {
    return when {
        temperature > 30 -> true
        dirty > 30 -> true
        day == "Sunday" ->  true
        else -> false
    }
}
```

When a lot of logic is packed into a small amount of code, we could use some well-named local variables. But the Kotlin way to do it is with compact functions.

```kotlin
fun isTooHot(temperature: Int) = temperature > 30

fun isDirty(dirty: Int) = dirty > 30

fun isSunday(day: String) = day == "Sunday"

fun shouldChangeWater (day: String, temperature: Int = 22, dirty: Int = 20): Boolean {
    return when {
        isTooHot(temperature) -> true
        isDirty(dirty) -> true
        isSunday(day) -> true
        else  -> false
    }
}
```

### `main()` function

```kotlin
fun main(args: Array<String>) {
    println("Hello, world!")
}
```

- `main()` returns a type `kotlin.Unit`.
- As of Kotlin 1.3, if the `main()` function doesn't use any parameters, you don't need to define args.

### Explicit return types

Functions with block body must always specify return types explicitly, unless it's intended for them to return `Unit`. Kotlin doesn't infer return types for functions with block bodies because such functions may have complex control flow in the body, and the return type will be non-obvious to the reader (and sometimes for the compiler).

`Unit` return type can be omitted (i.e. it's optional). It correspends to the `void` in Java, but it's a real class (Singleton).

```kotlin
fun printSum(a: Int, b: Int) {
	println("sum of $a and $b is ${a + b}")
}
```

[Why everything in Kotlin has a value?](02%20-%20Functions%209858a5a103bb47f2a35254a0d4009d58/Why%20everything%20in%20Kotlin%20has%20a%20value%209aa2e0dc5b164e04b4605fd8a3b88478.md)

### Function usage

```kotlin
val result = sum(4, 9)
```

```kotlin
Stream().read() // create instance of classe Stream and call read()
```

### Default arguments

Function parameters can have default values, which are used when you skip the corresponding argument.

The default value for a parameter doesn't have to be a value. It can be another function.

A function used as a default value is evaluated at runtime, so do not put an expensive operation like a file read or a large memory allocation in the function. The operation is executed every time your function is called, which may slow down your program.

```kotlin
fun read(
	b: Array<Byte>,
	off: Int = 0,
	len: Int = b.size, // trailing comma
) { /* ... */ }
```

A trailing comma is a comma symbol after the last item of  a series of elements. It's entirely optional but it has several benefits.

[trailing comma](02%20-%20Functions%209858a5a103bb47f2a35254a0d4009d58/trailing%20comma%20fb795c15b07c41089bbe1e456659939d.md)

### Named arguments

You can name one or more arguments when calling a function. This is helpful when the function has a large number of arguments.

When you use named arguments, you can freely change the order they are listed in, and if you want to use default values you can just leave them out altogether.

```kotlin
fun reformat(
    str: String,
    normalizeCase: Boolean = true,
    upperCaseFirstLetter: Boolean = true,
    divideByCamelHumps: Boolean = false,
    wordSeparator: Char = ' ',
) {
/*...*/
}
```

When calling the function, you don't have to name all its arguments:

```kotlin
reformat(
	'String!',
	false,
	upperCaseFirstLetter = false,
  divideByCamelHumps = true,
  '_'
)
```

You can skip all arguments with default values:

```kotlin
reformat('This is a long String!') // positional argument
```

But if you skip some arguments with default values, you must name all subsequent arguments.

**On the JVM**: You can't use the named argument syntax when calling Java functions because Java bytecode does not always preserve names of function parameters.

### Overriding methods

Overriding methods always use the same default parameter values as the base method.

When overriding a method with default parameter values, the default parameter values must be omitted from the signature.

```kotlin
open class A {
    open fun foo(i: Int = 10) { /*...*/ }
}

class B : A() {
    override fun foo(i: Int) { /*...*/ }  // No default value is allowed
}
```

If a default parameter precedes a no default value one, the former can only be used by calling the function with named arguments:

```kotlin
fun foo(
    bar: Int = 0, 
    baz: Int,
) { /*...*/ }

foo(baz = 1) // The default value bar = 0 is used
```

### Simplifying function declarations

```kotlin
fun generateAnswerString(countThreshold: Int): String {
    val answerString = if (count > countThreshold) {
        "I have the answer."
    } else {
        "The answer eludes me."
    }

    return answerString
}
```

We can skip declaring a local variable by directly returning the result of the if-else expression:

```kotlin
fun generateAnswerString(countThreshold: Int): String {
    return if (count > countThreshold) {
        "I have the answer."
    } else {
        "The answer eludes me."
    }
}
```

We can also replace the `return` keyword with the assignment operator:

```kotlin
fun generateAnswerString(countThreshold: Int): String = if (count > countThreshold) {
        "I have the answer"
    } else {
        "The answer eludes me"
    }
```

### Anonymous functions (lambdas)

Not every function needs a name. Some functions are more directly identified by their inputs and outputs. They are called *anonymous functions*. Part of what makes this useful is that the lambda expression can now be passed as data.

Like named functions, lambdas can have parameters. The parameters go on the left of what is called a function arrow `->`. The code to execute goes to the right of `->`.

We can keep a reference to an anonymous function, using this reference to call it later just like a normal function. We can also pass the reference around the application, as with other reference types.

```kotlin
val stringLengthFunc: (String) -> Int = { input ->
    input.length
}
/*
- Make a variable called stringLengthFunc
- stringLengthFunc can be any function that takes a String and returns an Int
- Assign a lambda to stringLengthFunc
- The lambda returns the length of the String
*/
```

The function type is denoted as `(String -> Int)`.

The return value of the function is the result of the final expression

To retrieve the result of the function, you must invoke it:

```kotlin
val stringLength: Int = stringLengthFunc("Android")
```

Lets take another example:

```kotlin
val waterFilter: (Int) -> Int = {dirty -> dirty / 2}

fun updateDirty(dirty: Int, operation: (int) -> Int): Int {
		return operation(dirty)
}

println(updateDirty(30, waterFilter))
// 15
```

The function you pass doesn't have to be lambda; it can be a regular named function instead. To tell Kotlin that you are passing the function reference as an argument, and not trying to call it, we can use the `::` operator.

```kotlin
fun increaseDirty(start: Int) = start + 1
println(updateDirty(15, ::increaseDirty))
// 16
```

### Higher-order functions

Functions that use other functions as arguments are called *higher-order functions.* This pattern is useful for communicating between components in the same way that you might use a callback interface in Java.

```kotlin
fun stringMapper(str: String, mapper: (String) -> Int): Int {
    // Invoke function
    return mapper(str)
}
```

We can call `stringMapper()` by passing a `String` & a function that satisfies the other input parameter, namely a function that takes a `String` as input and outputs an `Int`.

```kotlin
stringMapper("Android", { input ->
    input.length
})
```

Kotlin prefers that any parameter that takes a function is the last parameter. If the anonymous function is the last parameter defined on a function, you can pass it outside of the parentheses used to invoke the function (last parameter call syntax).

```kotlin
stringMapper("Android") { input ->
    input.length
}
```

### Inline functions

The use of inline function enhances the performance of higher order function. The inline function tells the compiler to copy parameters and functions to the call site.

Some expressions and declarations that are not supported anywhere inside the inline functions:
declaration of local classes - declaration of inner nested classes - function expressions - declarations of local function - default value for optional parameters

```kotlin
fun main(args: Array<String>) {  
		inlineFunction({println("calling inline functions")})  
}  
  
inline fun inlineFunction(myFun: () -> Unit ) {  
		myFun()  
    print("code inside inline function")  
}
```

We use the `inline` keyword

We can exit from the function and lambda expression itself by the `return` keyword:

```kotlin
fun main(args: Array<String>) {  
		inlineFunction(
			{println("calling inline functions")  return},
			{println("next parameter in inline functions")})  
}  
  
inline fun inlineFunction(myFun: () -> Unit, nxtFun: () -> Unit) {  
		myFun()  
		nxtFun()  
    print("code inside inline function")  
}

/* OUTPUT

calling inline functions

*/
```

To prevent a `return` from lambda expression and inline function, we can mark the lambda expression as `crossinline`. This will throw a compiler error if we add a `return` statement inside that lambda.

```kotlin
fun main(args: Array<String>) {  
		inlineFunction(
				{println("calling inline functions")  
        return}, // compile time error  
				{println("next parameter in inline functions")})  
}  
  
inline fun inlineFunction(crossinline myFun: () -> Unit, nxtFun: () -> Unit) {  
		myFun()  
		nxtFun()  
    print("code inside inline function")  
}
```

lambda expression → `Function` interface → `Object`

The `Function` interface has a method, `invoke()`, which is overridden to call the lambda expression.

It is worth noting that inlining large functions does increase your code size (extra objects created, incurring overhead memory and cpu time), so it's best used for simple functions that are used many times.

Most extension functions from the libraries are `inline`.

Lambdas are objects. To avoid creating the object, you can mark the function with `inline`, and the compiler will put the contents of the lambda in the code directly.

`inline` can help reduce resource usage by the program.