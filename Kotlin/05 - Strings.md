# 05 - Strings

A String represents an array of chars. They are immutable (which means that their length and elements cannot be changed).

```kotlin
val ch = charArrayOf('h', 'e', 'l', 'l', 'o')  
val st = String(ch)
```

Unlike Java, Kotlin does not require `new` keyword to instantiate an object of String class

```kotlin
val str1 = "Hello, javaTpoint" // escaped string 
val str2 = """Welcome To JavaTpoint""" // raw string
```

Some of the string properties can be accessed using these functions: `lenght` (returns the length of the sequence), `indices` (returns the ranges of valid character indices from current sequence), `lastIndex` (returns the index of the last char).