# 06 - Extensions

### Pairs and triples

Pairs and triples are premade data classes for 2 or 3 generic items. This can, for example, be useful for having a function return more than one value.

You can create a pair by creating an expression connecting two values, such as two strings, with the keyword `to`, then using `.first` or `.second` to refer to each value.

```kotlin
val equipment = "fish net" to "catching fish"
println("${equipment.first} used for ${equipment.second}")
// fish net used for catching fish
```

You create a triple using `Triple()` with 3 values. Use `.first`, `.second` and `.third` to refer to each value.

```kotlin
val numbers = Triple(6, 9, 42)
println(numbers.toString())
// (6, 9, 12)
println(numbers.toList())
// [6, 9, 12]
```

It's not required to use the same type for all the parts of the pair or triple.

```kotlin
val equipment2 = ("fish net" to "catching fish") to "equipment"
println("${equipment2.first} is ${equipment2.second}\n")
// (fish net, catching fish) is equipment
println("${equipment2.first.second}")
// catching fish
```

### Destructuring pairs and triples

Separating pairs and triples into their parts is called destructuring. Assign the pair or triple to the appropriate number of variables, and Kotlin will assign the value of each part in order.

```kotlin
val equipment = "fish net" to "catching fish"
val (tool, use) = equipment
println("$tool is used for $use")
// fish net is used for catching fish

val numbers = Triple(6, 9, 42)
val (n1, n2, n3) = numbers
println("$n1 $n2 $n3")
// 6 9 42
```

### More about lists

[Built-in functions for lists](06%20-%20Extensions%20cf5417234ce240658852eb5cdeac166f/Built-in%20functions%20for%20lists%2011e847b4b1084fa4b67c175f8cf10b60.csv)

```kotlin
val list = listOf(1, 5, 3, 4)
println(list.sum())
// 13

val list2 = listOf("a", "bbb", "cc")
println(list2.sum())
// error: none of the following functions can be called with the arguments supplied:
```

If the element isn't something `List` knows how to sum directly, such as a string, you can specify how to sum it using `.sumBy()` with a lambda function.

```kotlin
val list2 = listOf("a", "bbb", "cc")
println(list2.sumBy { it.length })
// 6

for (s in list2.listIterator()) {
    println("$s ")
}
// a bbb cc

```

### Hash maps

Hash maps are sort of like a list of pairs, where the first value acts as a key.

```kotlin
val cures = hashMapOf("white spots" to "Ich", "red sores" to "hole disease")

println(cures.get("white spots"))
// Ich

println(cures["red sores"])
// hole disease

println(cures["scale loss"])
// null
```

If a key isn't in the map, Kotlin provides the `getOrDefault()` function.

```kotlin
println(cures.getOrDefault("bloating", "sorry, I don't know"))
// sorry, I don't know
```

If we need more than returning a value, Kotlin provides the `getOrElse()` function. Whatever code is between the `{}` is executed.

```kotlin
println(cures.getOrElse("bloating") {"No cure for this"})
// No cure for this
```

Just like `mutableListOf`, you can also make a `mutableMapOf`.

```kotlin
val inventory = mutableMapOf("fish net" to 1)
inventory.put("tank scrubber", 3)
println(inventory.toString())
// {fish net=1, tank scrubber=3}

inventory.remove("fish net")
println(inventory.toString())
// {tank scrubber=3}
```

### Constants

```kotlin
const val rocks = 3
```

The value is assigned, and can't be changed, which sounds a lot like declaring a regular `val`. The difference is that the value for `const val` is determined at compile time, where as the value for `val` is determined during program execution, which means, `val` can be assigned by a function at run time.

```kotlin
val value1 = complexFunctionCall() // OK
const val CONSTANT1 = complexFunctionCall() // NOT ok
```

In addition, `const val` only works at the top level, and in singleton classes declared with `object`, not with regular classes. You can use this to create a file or singleton object that contains only constants, and import them as needed.

```kotlin
object Constants {
    const val CONSTANT2 = "object constant"
}
val foo = Constants.CONSTANT2
```

### Companion objects

Kotlin does not have a concept of class level constants.

To define constants inside a class, you have to wrap them into companion objects declared with the **`companion`** keyword. The companion object is basically a singleton object within the class.

```kotlin
class MyClass {
    companion object {
        const val CONSTANT3 = "constant in companion"
    }
}
```

The basic difference between companion objects and regular objects is:

- Companion objects are initialized from the static constructor of the containing class, that is, they are created when the object is created.
- Regular objects are initialized lazily on the first access to that object; that is, when they are first used.

### Extension functions

Extension functions allow you to add functions to an existing class without having to access its source code. For example, you could declare them in an **Extensions.kt** file that is part of your package. This doesn't actually modify the class, but it allows you to use the dot-notation when calling the function on objects of that class.

```kotlin
fun String.hasSpaces(): Boolean {
    val found = this.find { it == ' ' }
    return found != null
}
println("Does it have spaces?".hasSpaces())
// true
```

You can simplify the `hasSpaces()` function.

```kotlin
fun String.hasSpaces() = find { it == ' ' } != null
```

Extension functions only have access to the public API of the class they're extending. Variables that are `private` can't be accessed.

Extension functions are resolved statically, at compile time, based on the type of the variable.

In addition to extension functions, Kotlin also lets you add extension properties.

```kotlin
val AquariumPlant.isGreen: Boolean
   get() = color == "green"
```

The class you extend is called the receiver, and it is possible to make that class nullable. If you do that, the `this` variable used in the body can be `null`, so make sure you test for that. You would want to take a nullable receiver if you expect that callers will want to call your extension method on nullable variables, or if you want to provide a default behavior when your function is applied to `null`.

```kotlin
fun AquariumPlant?.pull() {
   this?.apply {
       println("removing $this")
   }
}

val plant: AquariumPlant? = null
plant.pull()
```

In this case, there is no output when you run the program. Because `plant` is `null`, the inner `println()` is not called.