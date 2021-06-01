# 07 - Generics

Kotlin, like many programming languages, has generic types. A generic type allows you to make a class generic, and thereby make a class much more flexible.

Imagine you were implementing a `MyList` class that holds a list of items. Without generics, you would need to implement a new version of `MyList` for each type: one for `Double`, one for `String`, one for `Fish`. With generics, you can make the list generic, so it can hold any type of object. It's like making the type a wildcard that will fit many types.

To define a generic type, put T in angle brackets `<T>` after the class name.

You could use another letter or a longer name, but the convention for a generic type is T.

```kotlin
class MyList<T> {
    fun get(pos: Int): T {
        TODO("implement")
    }
    fun addItem(item: T) {}
}
```

### Example

```kotlin
package generics

fun genericsExample() {
    val aquarium = Aquarium<TapWater>(TapWater())
		aquarium.waterSupply.addChemicalCleaners()
}

class Aquarium<T>(val waterSupply: T)

open class WaterSupply(var needProcessing: Boolean)

class TapWater : WaterSupply(true) {
		fun addChemicalCleaners() {
				needsProcessing = false
		}
}

class FishStoreWater : WaterSupply(false)

class LakeWater : WaterSupply(true) {
   fun filter() {
       needsProcessing = false
   }
}
```

Files don't have to have the same name as their class, and you can have multiple classes in a file.

When creating the `Aquarium` object, you can remove the angle brackets and what's between them because Kotlin has type inference.

### Generic constraints

Generic means you can pass almost anything, and sometimes that's a problem. When we don't put any limitations on `T`, any type (`String`, `Int`, etc.) can be passed in.

We can also pass `null`. This is possible because by default, `T` stands for the nullable `Any?` type (the type at the top of the type hierarchy).

To not allow passing `null`, make `T` of type `Any` explicitly:

```kotlin
class Aquarium<T: Any>(val waterSupply: T)
```

In this context, `Any` is called a generic constraint (It means any type can be passed for T as long as it isn't `null`).

To define a more specific generic constraint, we can replace `Any` with `WaterSupply`.

```kotlin
class Aquarium<T: WaterSupply>(val waterSupply: T)
```

### Checking

The `check()` function is a standard library function in Kotlin. It acts as an assertion and will throw an `IllegalStateException` if its argument evaluates to false.

```kotlin
class Aquarium<T: WaterSupply>(val waterSupply: T) {
    fun addWater() {
        check(!waterSupply.needsProcessing) { "water supply needs processing first" }
        println("adding water from $waterSupply")
    }    
}
```

### `in` & `out` types

An `in` type is a type that can only be passed into a class, not returned. An `out` type is a type that can only be returned from a class.

`val` and `var` are about the VALUES of variables. val protects the variable value from being changed.

`in` and `out` are about the TYPES of variables. in and out make sure that when working with generic types, only safe types are passed in and out of functions.

```kotlin
class Aquarium<out T: WaterSupply>(val waterSupply: T) {
    fun addWater(cleaner: Cleaner<T>) {
        if (waterSupply.needsProcessing) {
            cleaner.clean(waterSupply)
        }
        println("water added")
    }
}

interface Cleaner<in T: WaterSupply> {
    fun clean(waterSupply: T)
}

class TapWaterCleaner : Cleaner<TapWater> {
    override fun clean(waterSupply: TapWater) =   waterSupply.addChemicalCleaners()
}

fun addItemTo(aquarium: Aquarium<WaterSupply>) = println("item added")
```

### Generic functions

Typically, making a generic function is a good idea whenever the function takes an argument of a class that has a generic type.

```kotlin
fun isWaterClean(aquarium: Aquarium<WaterSupply>) {
   println("aquarium water is clean: ${!aquarium.waterSupply.needsProcessing}")
}
```

This means `Aquarium` must have an `out` type parameter for this to be called. You can remove the `out` requirement by making the function generic.

```kotlin
fun <T: WaterSupply> isWaterClean(aquarium: Aquarium<T>) {
   println("aquarium water is clean: ${!aquarium.waterSupply.needsProcessing}")
}

fun genericsExample() {
    val aquarium = Aquarium(TapWater())
    isWaterClean<TapWater>(aquarium)
}
```

### Generic method with a reified type

```kotlin
class Aquarium<out T: WaterSupply>(val waterSupply: T) {
		inline fun <reified R: WaterSupply> hasWaterSupplyOfType() = waterSupply is R
}

inline fun <reified T: WaterSupply> WaterSupply.isOfType() = this is T

fun genericsExample() {
    val aquarium = Aquarium(TapWater())
    println(aquarium.hasWaterSupplyOfType<TapWater>())   // true
		println(aquarium.waterSupply.isOfType<TapWater>())   // true
}
```

To do an `is` check, you need to tell Kotlin that the type is reified, or real, and can be used in the function. To do that, put `inline` in front of the fun keyword, and `reified` in in front of the generic type `R`.

Once a type is reified, you can use it like a normal type—because it is a real type after inlining. That means you can do is checks using the type.

All generic types are only used at compile time by Kotlin. This lets the compiler make sure that you're doing everything safely. By runtime all the generic types are erased.

It turns out the compiler can create correct code without keeping the generic types until runtime. But it does mean that sometimes you do something, like `is` checks on generic types, that the compiler can't support. That's why Kotlin added reified, or real, types.

Reified types, unlike generic types, persist to runtime.