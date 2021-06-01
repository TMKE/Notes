# trailing comma

Using trailing commas has several benefits:

- It makes version-control diffs cleaner – as all the focus is on the changed value.
- It makes it easy to add and reorder elements – there is no need to add or delete the comma if you manipulate elements.
- It simplifies code generation, for example, for object initializers. The last element can also have a comma.

Kotlin supports trailing commas in the following cases:

- [Enumerations](https://kotlinlang.org/docs/reference/coding-conventions.html#enumerations)

    ```kotlin
    enum class Direction {
    	NORTH,
    	SOUTH,
    	WEST,
    	EAST, // trailing comma
    }
    ```

- [Value arguments](https://kotlinlang.org/docs/reference/coding-conventions.html#value-arguments)

    ```kotlin
    fun shift(x: Int, y: Int) { /* ... */ }

    shift(
    	25,
    	20, // trailing comma
    )

    val colors = listOf(
    	"red",
    	"green",
    	"blue", // trailling comma
    )
    ```

- [Class properties and parameters](https://kotlinlang.org/docs/reference/coding-conventions.html#class-properties-and-parameters)

    ```kotlin
    class Customer(
        val name: String,
        val lastName: String, // trailing comma
    )

    class Customer(
        val name: String,
        lastName: String, // trailing comma
    )
    ```

- [Function value parameters](https://kotlinlang.org/docs/reference/coding-conventions.html#function-value-parameters)

    ```kotlin
    fun powerOf(
        number: Int, 
        exponent: Int, // trailing comma
    ) { /*...*/ }

    constructor(
        x: Comparable<Number>,
        y: Iterable<Number>, // trailing comma
    ) {}

    fun print(
        vararg quantity: Int,
        description: String, // trailing comma
    ) {}
    ```

- [Parameters with optional type (including setters)](https://kotlinlang.org/docs/reference/coding-conventions.html#parameters-with-optional-type-including-setters)

    ```kotlin
    val sum: (Int, Int, Int) -> Int = fun(
        x,
        y,
        z, // trailing comma
    ): Int {
        return x + y + x
    }
    println(sum(8, 8, 8))
    ```

- [Indexing suffix](https://kotlinlang.org/docs/reference/coding-conventions.html#indexing-suffix)

    ```kotlin
    class Surface {
        operator fun get(x: Int, y: Int) = 2 * x + 4 * y - 10
    }
    fun getZValue(mySurface: Surface, xValue: Int, yValue: Int) =
        mySurface[
            xValue,
            yValue, // trailing comma
        ]
    ```

- [Lambda parameters](https://kotlinlang.org/docs/reference/coding-conventions.html#lambda-parameters)

    ```kotlin
    fun main() {
        val x = {
                x: Comparable<Number>,
                y: Iterable<Number>, // trailing comma
            ->
            println("1")
        }

        println(x)
    }
    ```

- `[when` entry](https://kotlinlang.org/docs/reference/coding-conventions.html#when-entry)

    ```kotlin
    fun isReferenceApplicable(myReference: KClass<*>) = when (myReference) {
        Comparable::class,
        Iterable::class,
        String::class, // trailing comma
            -> true
        else -> false
    }
    ```

- [Collection literals (in annotations)](https://kotlinlang.org/docs/reference/coding-conventions.html#collection-literals-in-annotations)

    ```kotlin
    annotation class ApplicableFor(val services: Array<String>)

    @ApplicableFor([
        "serializer",
        "balancer",
        "database",
        "inMemoryCache", // trailing comma
    ])
    fun run() {}
    ```

- [Type arguments](https://kotlinlang.org/docs/reference/coding-conventions.html#type-arguments)

    ```kotlin
    fun <T1, T2> foo() {}

    fun main() {
        foo<
                Comparable<Number>,
                Iterable<Number>, // trailing comma
                >()
    }
    ```

- [Type parameters](https://kotlinlang.org/docs/reference/coding-conventions.html#type-parameters)

    ```kotlin
    class MyMap<
            MyKey,
            MyValue, // trailing comma
            > {}
    ```

- [Destructuring declarations](https://kotlinlang.org/docs/reference/coding-conventions.html#destructuring-declarations)

    ```kotlin
    data class Car(val manufacturer: String, val model: String, val year: Int)
    val myCar = Car("Tesla", "Y", 2019)

    val (
        manufacturer,
        model,
        year, // trailing comma
    ) = myCar

    val cars = listOf<Car>()
    fun printMeanValue() {
        var meanValue: Int = 0
        for ((
            _,
            _,
            year, // trailing comma
        ) in cars) {
            meanValue += year
        }
        println(meanValue/cars.size)
    }
    printMeanValue()
    ```