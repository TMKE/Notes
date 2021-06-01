# Filters

Filters are a handy way to get part of a list based on some condition.

```kotlin
val decorations = listOf ("rock", "pagoda", "plastic plant", "alligator", "flowerpot")

fun main() {
    println( decorations.filter {it[0] == 'p'})
		// [pagoda, plastic plant]
}
```

### Eager or lazy?

Is the result list created immediately, or when the list is accessed? In Kotlin, it happens whichever way you need it to. By default, `filter` is eager, and each time you use the filter, a list is created.

To make the filter lazy, you can use a `Sequence`, which is a collection that can only look at one item at a time, starting at the beginning, and going to the end. Conveniently, this is exactly the API that a lazy filter needs.

```kotlin
fun main() {
    val decorations = listOf ("rock", "pagoda", "plastic plant", "alligator", "flowerpot")

    // eager, creates a new list
    val eager = decorations.filter { it [0] == 'p' }
    println("eager: $eager")
		// eager: [pagoda, plastic plant]

		// lazy, will wait until asked to evaluate
    val filtered = decorations.asSequence().filter { it[0] == 'p' }
    println("filtered: $filtered")
		// filtered: kotlin.sequences.FilteringSequence@386cc1c4

		// force evaluation of the lazy list
    val newList = filtered.toList()
    println("new list: $newList")
		// new list: [pagoda, plastic plant]
}
```

When you return the filter results as a `Sequence`, the `filtered` variable won't hold a new list—it'll hold a `Sequence` of the list elements and knowledge of the filter to apply to those elements. Whenever you access elements of the `Sequence`, the filter is applied, and the result is returned to you.

We can use the `map()` function to see what happens with `Sequence` and lazy evaluation.

```kotlin
val lazyMap = decorations.asSequence().map {
		println("access: $it")
		it // return the element passed
}
```

The `map()` function performs a simple transformation on each element in the sequence.

```kotlin
println("lazy: $lazyMap")
// lazy: kotlin.sequences.TransformingSequence@5ba23b66

println("first: ${lazyMap.first()}")
// access: rock
// first: rock

println("all: ${lazyMap.toList()}")
/*
access: rock
access: pagoda
access: plastic plant
access: alligator
access: flowerpot
all: [rock, pagoda, plastic plant, alligator, flowerpot]
*/
```

With the filter applied, the `map()` function is called only on filtered elements.

```kotlin
val lazyMap2 = decorations.asSequence().filter {it[0] == "p"}.map {
		println("access: $it")
		it
}
println("filtered: ${lazyMap2.toList()}")
/*
access: pagoda
access: plastic plant
filtered: [pagoda, plastic plant]
*/
```

`filter` is a higher-order function because we passed the following lambda expression as the condition to check: `{it[0] == 'p'}`. Similarly, `map` is a higher-order function, and the lambda expression we passed to it was the transformation to apply.