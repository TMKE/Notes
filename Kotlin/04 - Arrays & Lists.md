# 04 - Arrays & Lists

### Arrays

Arrays in Kotlin have fixed sizes. They can be created using: 

- `arrayOf()`: array declared with `arrayOf` doesn't have a type associated with the elements, so you can mix types, which is helpful.
- `intArrayOf()`, `charArrayOf()`, `booleanArrayOf()`, `longArrayOf()`, `shortArrayOf()`, `byteArrayOf()`: declare arrays with one type for all the elements.

Using an array of a primitive type such as `Int` or `Byte` avoids the overhead of boxing.

```kotlin
var a1 = arrayOf(1, 39, 33, 12, 9)
a1.set(0, 4)
a1[1] = 54

println(java.util.Arrays.toString(a1))

var a2 = arrayOf<Int>(1, 39, 33, 12, 9)
for(e in a2) {
		println(e)
}

val a3 = arrayOf<String>("Ajay","Prakesh","Michel","John","Sumit")
println(a3.get(0))
println(a3[1])

val a4 = arrayOf(3, 98, 22, "Ajay","Prakesh")
for(i in 0..a4.size - 1) println(a4[i])

var a5: IntArray = intArrayOf(3, 9, 99, 23, 12)
var a6 = Array<Int>(5) {0}

var a7 = a2 + a5

// Initializing a8 with code
var a8 = Array(5) {it * 2}
println(java.util.Arrays.toString(a8))
// [0, 2, 4, 6, 8]
```

If we try to read or change an element with index not found in the array, an `ArrayIndexOutOfBoundException` exception will be thrown.

Use `java.util.Arrays.toString()` array utiliy to print out an array. When you don't use the array utility to print it, Kotlin prints the address instead of the contents of the array.

You can initialize arrays with code instead of 0s.

### Lists (mutable & immutable)

```kotlin
// This list cannot be changed
val school = listOf("mackerel", "trout", "halibut")
println(school)

// This list can be changed
val myList = mutableListOf("tuna", "salmon", "shark")
myList.remove("shark")
```

The `remove()` method returns `true` when ut successfully removes the item passed.

With a list (or array) defined with `val`, you can't change which list the variable refers to, but you can still change the contents of the list.

There's no mutable version of an `Array`. Once you created an array, the size is fixed. You can't add or remove elements, except by copying to a new array.

In Kotlin, you can loop through the elements and the indexes at the same time:

```kotlin
for ((index, element) in school.withIndex()) {
    println("Item at $index is $element\n")
}
```