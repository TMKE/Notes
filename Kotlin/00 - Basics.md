# 00 - Basics

Kotlin is a new, modern programming language created by programmers, for programmers. It's focused on clarity, conciseness, and code safety.

### Robust code

The creators of Kotlin made various design decisions about the language to help programmers create robust code. For example, null-pointer exceptions in software have caused financial losses and spectacular computer crashes, and have resulted in countless hours of debugging. So Kotlin distinguishes between nullable and non-nullable data types, which helps catch more errors at compile time. Kotlin is strongly typed, and it does a lot to infer the types from your code. It has lambdas, coroutines, and properties, which allow you to write less code with fewer bugs.

### Mature platform

Kotlin has been around since 2011, and was released as open source in 2012. It reached version 1.0 in 2016, and since 2017 Kotlin has been an officially supported language for building Android apps. It's included with the IntelliJ IDEA as well as Android Studio 3.0 and later.

### Concise, readable code

Code written in Kotlin can be very concise, and the language is designed to eliminate boilerplate code such as getters and setters. For example, consider the following Java code:

```java
public class Aquarium {

   private int mTemperature;

   public Aquarium() { }

   public int getTemperature() {
       return mTemperature;
   }

   public void setTemperature(int mTemperature) {
       this.mTemperature = mTemperature;
   }

   @Override
   public String toString() {
       return "Aquarium{" +
               "mTemperature=" + mTemperature +
               '}';
   }
}
```

It can be written concisely like this in Kotlin:

```kotlin
data class Aquarium (var temperature: Int = 0)
```

### Interoperable with Java

Kotlin code compiles so that you can use Java and Kotlin code side-by-side, and continue to use your favorite Java libraries. You can add Kotlin code to an existing Java program, or if you want to migrate your program completely, IntelliJ IDEA and Android Studio both include tools to migrate existing Java code to Kotlin code.

### Verify the JDK installation

```bash
java -version
javac -version
```

If you receive an error from either command, confirm you've added the correct path for the JRE.

### REPL

REPL (Read-Eval-Print Loop) is Kotlin's interactive shell. Commands (code) that you type into the REPL are interpreted as soon as you press `Control+Enter` (`Command+Enter` on a Mac).

[Read-eval-print loop](https://en.wikipedia.org/wiki/Read%E2%80%93eval%E2%80%93print_loop)

In IntelliJ IDEA, select **Tools > Kotlin > Kotlin REPL**.