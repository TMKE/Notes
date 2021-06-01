# Generate random numbers

```kotlin
import java.util.Random // required

val randomInt = (0..10).random() // generated random from 0 to 10 included

val randomInt2 = (0 until 10).random() // generated random from 0 to 10 (not included)

val randomInt3 = Random().nextInt(10)

val randomChar = ('a'..'b').random()

fun randomDay() : String {
    val week = arrayOf ("Monday", "Tuesday", "Wednesday", "Thursday",
            "Friday", "Saturday", "Sunday")
    return week[Random().nextInt(week.size)]
}
```