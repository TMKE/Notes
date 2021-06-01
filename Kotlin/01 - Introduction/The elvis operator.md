# The elvis operator

`?:` takes the right-hand value if the left-hand value is null.

```kotlin
var fishFoodTreats = 6

fishFoodTreats = fishFoodTreats?.dec() ?: 0
```

Or

```kotlin
val l: Int = if (b != null) b.length else -1
```

is equivalent to:

```kotlin
val l = b?.length ?: -1
```

Since `throw` and `return` are expression in Kotlin, they can also be used on the right hand side of the elvis operator. This can be very handy, for example, for checking function arguments:

```kotlin
fun foo(node: Node): String? {
    val parent = node.getParent() ?: return null
    val name = node.getName() ?: throw IllegalArgumentException("name expected")
    // ...
}
```