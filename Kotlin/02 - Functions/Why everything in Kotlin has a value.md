# Why everything in Kotlin has a value?

```kotlin
val isUnit = println("This is an expression")
println(isUnit)
// kotlin.Unit

val temperature = 10
val message = "The water temperature is ${ if (temperature > 50) "too warm" else "OK" }."
println(message)
// The water temperature is OK.
```

Loops are exceptions to "everything has a value". There's no sensible value for for loops or while loops, so they do not have values. If you try to assign a loop's value to something, the compiler gives an error.