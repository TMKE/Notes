# 03 - Classes

### OOP

- *Classes:* blueprints for objects
- *Objects:* instances of classes
- *Properties:* characteristics of objects
- *Methods (member functions):* functionality of the class
- *Interface:* a specification that a class can implement
- *Packages:* a way to group related code to keep it organized

    ```kotlin
    package example.myapp // at the top of the file
    ```

### Properties

Classes represent state using properties. A property is a class-level variable that can include a getter, a setter and a backing field.

```kotlin
class Car {
	val color: String
	val wheels: listOf<Wheel>()
}
```

```kotlin
val car = Car() // construct
val wheels = car.wheels // retrieve a value
```

Under the hood, Kotlin automatically creates getters and setters for the properties.

### Constructors

If we want to customize the wheels, we can define a custome constructor that specifies how the class properties are initialized:

```kotlin
class Car(color: String, wheels: List<Wheel) {
		val color: String = color
		val wheels : List<Wheel> = wheels
		...
}
```

Or with a more compact Kotlin way, we can define the properties directly with the constructor, using `var` and `val`, and Kotlin also creates the getters and setters automatically:

```kotlin
class Car(val color: String, val wheels: List<Wheel>) {
		...
}
```

In some programming languages, the constructor is defined by creating a method within the class that has the same name as the class. In Kotlin, you define the constructor directly in the class declaration itself, specifying the parameters inside parentheses as if the class was a method.

When we create an object with the constructor, we can specifiy no argument (in case of default values), or specify some or all of them.

### `init` blocks

```kotlin
class Car(val color: String, val wheels: List<Wheel>) {
		init {
				println("car initializing")
		}
		init {
				println("Color: $color")
}
```

The `init` blocks are executed in the order in which they appear in the class definition, and all of them are executed when the constructor is called.

Any properties used in initializer blocks must be declared previously.

### Seconday constructors

A Kotlin class can have one or more secondary constructors to allow constructor overloading, that is, constructors with different arguments.

Kotlin coding style says each class should have only one constructor, using default values and named parameters. This is because using multiple constructors leads to more code paths, and the likelihood that one or more paths will go untested.

Every secondary constructor must call the primary constructor first, either directly using `this()`, or indirectly by calling another secondary constructor. This means that any `init` blocks in the primary will be called for all constructors, and all the code in the primary constructor will be executed first.

```kotlin
class Car(val color: String, val wheels: List<Wheel>) {
		init {
				println("car initializing")
		}
		init {
				println("Color: $color")

		constructor(model: String): this() {
				val model = model
		}
}
```

We could include the `constructor` keyword in the primary constructor.

### Getters and setters

Sometimes the value for a property needs to be adjusted or calculated (The getter needs to return the caluculated value). 

```kotlin
var volume: Int
		get() = width * height * length / 1000
		set(value) {
				height = (value * 1000) / (width * length) // suppose we could change the height only
		}
```

### Class functions and encapsulation

Classes use functions to model behavior. Functions can modify state, helping you to expose only the data that you wish to expose (encapsulation).

```kotlin
class Car(val wheels: List<Wheel>) {

    private val doorLock: DoorLock = ...

		var gallonsOfFuelInTank: Int = 15
        private set

    fun unlockDoor(key: Key): Boolean {
        // Return true if key is valid for door lock, false otherwise
    }
}
```

The visibility modifiers:

- `public`: means visible outside the class (everything is public by default)
- `internal`: means visible only within the module (a set of files compiled together, like a library or application)
- `private`: means visible only in the class (or source file if you are working with functions)
- `protected`: same as `private`, but also visible to subclasses

```kotlin
var volume: Int
		get() = width * height * length / 1000
		private set(value) {
				height = (value * 1000) / (width * length)
		}
```

### Inheritance and overriding functions

```kotlin
class LoginFragment : Fragment()
```

Within `LoginFragment`, we can override a number of lifecycle callbacks to respond to state changes in our Fragment.

```kotlin
override fun OnCreateView(
	inflater: LayoutInflater,
	container: ViewGroup?,
	savedInstanceState: Bundle?
): View? {
	return inflater.inflate(R.layout.login_fragment, container, false)
}
```

We can reference a function from the superclass using the `super` keyword.

```kotlin
override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
    super.onViewCreated(view, savedInstanceState)
}
```

In Kotlin, we must initialize an object's properties when declaring it. This implies that when we obtain an instance of a class, we can immediately reference any of its accessible properties.

In Kotlin, by default, classes cannot be subclassed. Similarly, properties and member variables cannot be overridden by subclasses (though they can be accessed).

You must mark a class as `open` to allow it to be subclassed. Similarly, you must mark properties and member variables as `open`, in order to override them in the subclass.

```kotlin
open class Aquarium (open var length: Int = 100, open var width: Int = 20, open var height: Int = 40) {
    open var volume: Int
        get() = width * height * length / 1000
        set(value) {
            height = (value * 1000) / (width * length)
        }
		open val shape = "rectangle"

		open var water: Double = 0.0
				get() = volume * 0.9

		fun printSize() {
				println(shape)
				println("Width: $width cm" +
								"Length: $lenght cm" +
								"Height: $height cm")
				println("Volume: $volume l Water: $water l (${water/volume*100.0}% full})")
		}
}

class TowerTank (override var height: Int, var diameter: Int): Aquarium(height = height, width = diameter, length = diameter) {
		override var volume: Int
				get() = (width/2 * length/2 * height / 1000 * 3.14).toInt()
				set(value) {
						height = ((value * 1000 / 3.14) / (width/2 * length/2)).toInt()
				}
		
		override var water: Double = volume * 0.8
		override val shape = "cylinder"
}
```

Subclasses must declare their constructor parameters explicitly.

### Interfaces

To define common behavior or properties to be shared among some related classes, we use interfaces and abstract classes.

- Neither an abstract class nor an interface can be instantiated on its own.
- Abstract classes have constructors.
- Interfaces can't have any constructor logic or store any state.

Abstract classes are always open; you don't need to mark them with `open`.

Properties and methods of an abstract class are non-abstract unless you explicitly mark them with the `abstract` keyword.

If properties or methods are abstract, the subclasses must implement them.

```kotlin
abstract class AquariumFish {
		abstract val color: String
}

interface FishAction {
		fun eat() // we can do a default implementation
}

class Shark: AquariumFish(), FishAction {
		override val color = "gray"
		override fun eat() {
				println("hunt and eat fish")
		}
}

class Plecostomus: AquariumFish(), FishAction {
		override val color = "gold"
		override fun eat() {
				println("eat algae")
		}
}
```

![03%20-%20Classes%2000bfa28857fc4451ae46c7494f47375a/Untitled.png](03%20-%20Classes%2000bfa28857fc4451ae46c7494f47375a/Untitled.png)

![03%20-%20Classes%2000bfa28857fc4451ae46c7494f47375a/Untitled%201.png](03%20-%20Classes%2000bfa28857fc4451ae46c7494f47375a/Untitled%201.png)

We can use multiple interfaces in a class, but we can only subclass from one abstract class.

Composition often leads to better encapsulation, lower coupling (interdependence), cleaner interfaces, and more usable code. For these reasons, using composition with interfaces is the preferred design. On the other hand, inheritance from an abstract class tends to be a natural fit for some problems. So you should prefer composition, but when inheritance makes sense Kotlin lets you do that too!

### Interface delegation

Interface delegation is an advanced technique where the methods of an interface are implemented by a helper (or delegate) object, which is then used by a class.

This technique can be useful when you use an interface in a series of unrelated classes: you add the needed interface functionality to a separate helper class, and each of the classes uses an instance of the helper class to implement the functionality.

```kotlin
interface FishColor {
		val color: String
}

interface FishAction {
		fun eat() // we can do a default implementation
}

class Plecostomus(fishColor: FishColor = GoldColor): FishAction, FishColor by fishColor, PrintFishAction("eat algae")

class Shark: FishAction, FishColor {
    override val color = "gray"
    override fun eat() {
        println("hunt and eat fish")
    }
}

object GoldColor: FishColor { // singleton class
		override val color = "gold"
}

class PrintFishAction(val food: String): FishAction {
		override fun eat() {
				println(food)
		}
}
```

Kotlin lets you declare a class where you can only create one instance of it by using the keyword `object` instead of `class`. That instance is referenced by the class name (singleton pattern).

![03%20-%20Classes%2000bfa28857fc4451ae46c7494f47375a/Untitled%202.png](03%20-%20Classes%2000bfa28857fc4451ae46c7494f47375a/Untitled%202.png)

### Data classes

A data class is similar to a `struct` in some other languages—it exists mainly to hold some data—but a data class object is still an object. Kotlin data class objects have some extra benefits, such as utilities for printing and copying.

```kotlin
data class Decoration(val rock: String) {
}

fun makeDecorations() {
		val d1 = Decoration("granite")
		println(d1)
		// Decoration(rocks=granite)

		val d2 = Decoration("slate")
		println(d2)
		// Decoration(rocks=slate)

		val d3 = Decoration("slate")
		println(d3)
		// Decoration(rocks=slate)

		println(d1.equals(d2))
		// false
		println(d2.equals(d3))
		// true
}
```

using `==` on data class objects is the same as using `equals()` (structural equality).

The `===` operator is used to check whether two variables refer to the same object (referntial equality).

Assigning a data class object to another variable copies the reference to that object, not the contents. To copy content to a new object, use the `copy()` method.

The `copy()`, `equals()`, and other data class utilities only reference properties defined in the primary constructor.

```kotlin
// Here is a data class with 3 properties.
data class Decoration2(val rocks: String, val wood: String, val diver: String){
}

fun makeDecorations() {
    val d5 = Decoration2("crystal", "wood", "diver")
    println(d5)

// Assign all properties to variables.
    val (rock, wood, diver) = d5
    println(rock)
    println(wood)
    println(diver)
}
```

```
Decoration2(rocks=crystal, wood=wood, diver=diver)
crystal
wood
diver
```

If you don't need one or more of the properties, you can skip them by using `_` instead of a variable name.

```kotlin
val (rock, _, diver) = d5
```

### Enumerations

Enumerations allows you to create something and refer to it by name.

```kotlin
enum class Color(val rgb: Int) {
		RED(0xFF0000), GREEN(0x00FF00), BLUE(0x0000FF);
}

fun main() {
		println(Color.RED.name)
		println(Color.RED.ordinal)
		println(Color.RED.rgb)
```

```
RED
1
0xFF0000
```

### Sealed classes

A sealed class is a class that can be subclassed, but only inside the file in which it's declared. If you try to subclass the class in a different file, you get an error. This makes sealed classes a safe way to represent a fixed number of types. For example, sealed classes are great for returning success or error from a network API.

```kotlin
sealed class Seal
class SeaLion : Seal()
class Walrus : Seal()

fun matchSeal(seal: Seal): String {
		return when(seal) {
				is Walrus -> "walrus"
				is SeaLion -> "sea lion"
		}
}
```