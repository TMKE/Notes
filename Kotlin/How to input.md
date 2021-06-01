# How to input?

The `readLine()` function reads line of string input from standard input stream and returns the line read or null.

```kotlin
val name = readLine()
```

We need to explicitly convert types other than String when using `readLine()` function.

```kotlin
val age: Int = Integer.valueOf(readLine())
```

We don't need to use Scanner object `java.util.Scanner` class form Java standard library to read strings, but we need it with other types

```kotlin
import java.util.Scanner

val read = Scanner(System.`in`)

val a = read.nextInt() // Int

val b = read.nextBoolean()  // Boolean

val c = read.nextFloat() // Float

val d = read.nextLong() // Long

val e = read.nextDouble() // Double
```