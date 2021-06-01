# Type checks & casts

### `is` & `!is` operators

Used to check if an object conforms to a given type at runtime.

```kotlin
if (obj is String) {
    print(obj.length)
}

if (obj !is String) { // same as !(obj is String)
    print("Not a String")
}
else {
    print(obj.length)
}
```

### Smart casts

We don't need to use explicit cast operators in Kotlin, because the compiler trachs the `is`-checks and explicit casts for immutable values and inserts (safe) casts automatically when needed.

```kotlin
fun demo(x: Any) {
    if (x is String) {
        print(x.length) // x is automatically cast to String
    }
}
```

The compiler is smart enough to know a cast to be safe if a negative check leads to a return:

```kotlin
if (x !is String) return

print(x.length) // x is automatically cast to String
```

or in the right-hand side of `&&` and `||`:

```kotlin
// x is automatically cast to string on the right-hand side of `||`
if (x !is String || x.length == 0) return

// x is automatically cast to string on the right-hand side of `&&`
if (x is String && x.length > 0) {
    print(x.length) // x is automatically cast to String
}
```

Such *smart casts* work for when expressions and while loops as well:

```kotlin
when (x) {
    is Int -> print(x + 1)
    is String -> print(x.length + 1)
    is IntArray -> print(x.sum())
}
```

Smart casts do not work when the compiler cannot guarantee that the variable cannot change between the check and the usage.

[Rules of application of smart casts](Type%20checks%20&%20casts%20f16f8aab41704065afc82a929936d8cc/Rules%20of%20application%20of%20smart%20casts%20ec1d22db80f346afb7838061461ccc0c.md)

## Checking for `null`

### "Unsafe" cast operator

The unsafe cast in Kotlin is done by the infix operator `as`. We call it unsafe because it throws an exception (`ClassCastException`) if the cast is not possible.

```kotlin
val x: String = y as String
```

`null` cannot be cast to `String` as this type is not nullable

```kotlin
val x: String? = y as String?
```

Unsafe cast operator is not equivalent to the `unsafeCast<T>()` method available in Kotlin/JS. `unsafeCast` will do no type-checking at all, whereas the cast operator throws a `ClassCastException` when the cast fails.

### Safe (nullable) cast operator

We use a safe cast operator `as?` that returns `null` on failure.

```kotlin
val x: String? = y as? String
```

Despite the fact that the right-hand side of *`as?`* is a non-null type `String`, the result of the cast is nullable

### Not-null assertion operator `!!`

It converts any value to a non-null type and throws an exception if the value is null. We can write `b!!`, and this will return a non-null value of `b` or throw an NPE if `b` is null:

```kotlin
val l = b!!.length
```

In programming slang, the exclamation mark `!` is often called a **bang**, so the not-null assertion operator is sometimes called the **double-bang** or **bang bang** operator.

It's generally a bad idea to use the double-bang operator. That's why the language creators made you enter two exclamation marks instead of one. However, sometimes you need the double-bang when dealing with legacy Java code.

### Collections of nullable type

If you have a collection of elements of a nullable type and want to filter non-null elements, you can do so by using `filterNotNull`:

```kotlin
val nullableList: List<Int?> = listOf(1, 2, null, 4)
val intList: List<Int> = nullableList.filterNotNull()
```