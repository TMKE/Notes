# 08 - Functional manipulation

### Annotations

Annotations are a way of attaching metadata to code. 

The annotations are read by the compiler and used to generate code or logic.

Many frameworks, such as Ktor and Kotlinx, as well as Room, use annotations to configure how they run and interact with your code. You are unlikely to encounter any annotations until you start using frameworks.

There are also annotations that are available through the Kotlin standard library that control the way code is compiled. They're really useful if you're exporting Kotlin to Java code, but otherwise you don't need them that often.

```kotlin
@file:JvmName("InteropFish")
class InteropFish {
   companion object {
       @JvmStatic fun interop()
   }
}
```

You can also create your own annotations, but this is mostly useful if you are writing a library that needs particular information about classes at runtime, that is *reflection*.

```kotlin
import kotlin.reflect.full.*    // required import

annotation class IamAPlant

@IamAPlant class Plant {
		fun trim() {}
		fun fertilize() {}
}

fun testAnnotations() {
		val classObj = Plant::class
		for(m in classObj.declaredMemberFunctions) {
        println(m.name)
    }
		// trim
		// fertilize

		val plantObject = Plant::class
		for(a in plantObject.annotations) {
				println(a.annotationClass.simpleName()
		}
		// IamAPlant

		val myAnnotationObject = plantObject.findAnnotation<IamAPlant>()
		println(myAnnotationObject)
		// @example.IamAPlant
}
```

```kotlin
annotation class ImAPlant

@Target(AnnotationTarget.PROPERTY_GETTER)
annotation class OnGet
@Target(AnnotationTarget.PROPERTY_SETTER)
annotation class OnSet

@ImAPlant class Plant {
    @get:OnGet
    val isGrowing: Boolean = true

    @set:OnSet
    var needsFood: Boolean = false
}
```

### Controlling flow

Using `return`, `break`, and `continue`.

### Lambdas

```kotlin
data class Fish(val name: String)

val myFish = listOf(Fish("Flipper"), Fish("Moby Dick"), Fish("Dory"))
myFish.filter { it.name.contains("i")}
```

In the lambda expression, `it` refers to the current list element, and the filter is applied to each list element in turn.

### Higher-order functions

```kotlin
data class Fish (var name: String)

fun fishExamples() {
    val fish = Fish("splashy")  // all lowercase
		with(fish.name) {
				println(this.capitalize())
				// Splashy
		}
}

fun main () {
    fishExamples()
}
```

The `with()` function lets you make one or more references to an object or property in a more compact way.

```kotlin
fun myWith(name: String, block: String.() -> Unit) {
		name.block()
}
```

As part of the Kotlin Standard Library, here are a few useful extensions: `run()`, `apply()`, and `let()`.

- `run()`

    An extension that works with all types. It takes one lambda as argument and returns the result of executing the lambda.

    ```kotlin
    fish.run {
    		name
    }
    ```

- `apply()`

    Similar to `run()`, but it returns the changed object it was applied to instead of the result of the lambda (useful for calling methods on a newly created object).

    ```kotlin
    val fish2 = Fish(name = "splashy").apply {
         name = "sharky"
    }
    println(fish2.name)
    // sharky
    ```

    `run()` and `apply()` are similar, but `run()` returns the result of applying the function, and `apply()` returns the object after applying the function.

- `let()`

    Similar to `apply()`, but it returns a copy of the object with the changes (useful for chaining manipulations together).

    ```kotlin
    println(fish.let { it.name.capitalize()}
    .let{it + "fish"}
    .let{it.length}
    .let{it + 31})
    // 42

    println(fish)
    // Fish(name=splashy)
    ```

### Single Abstract Methods

Single Abstract Method just means an interface with one method on it. They are very common when using APIs written in the Java programming language, so there is an acronym for it, SAM. Some examples are `Runnable`, which has a single abstract method, `run()`, and `Callable`, which has a single abstract method, `call()`.

```java
package example;

public class JavaRun {
    public static void runNow(Runnable runnable) {
        runnable.run();
    }
}
```

Kotlin lets you instantiate an object that implements an interface by preceding the type with `object:`. It's useful for passing parameters to SAMs.

```kotlin
fun runExample() {
    val runnable = object: Runnable {
        override fun run() {
            println("I'm a Runnable")
        }
    }
		
		JavaRun.runNow(runnable)
		// I'm a Runnable
}
```

Kotlin provides a simpler way to do this — using a lambda in place of the object to make the code more compact.

```kotlin
fun runExample() {
    JavaRun.runNow({
        println("Passing a lambda as a Runnable")
    })
}
```

Or even more concise:

```kotlin
fun runExample() {
    JavaRun.runNow {
        println("Last parameter is a lambda as a Runnable")
    }
}
```

You can instantiate, override and make a call to a SAM with one line of code, using the pattern: `Class.singleAbstractMethod { lambda_of_override }`