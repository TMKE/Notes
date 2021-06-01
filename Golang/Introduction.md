### What is Go?

- fast, statically typed, compiled language.
  - compiled: doesn't need to be interpreted one line at a time
  - statically typed: variable types are checked before runtime by the complier
  - strongly typed: variable type cannot change after being declared
- general purpose language
- built-in testing support
- OOP language (in it's own way)

### `main.go`

```go
package main

import "fmt"

func main() {
    fmt.Println("Hello!")
}
```

- `package`: every `go` file is part of a package (a collection of files/code).
- `main()`: entry point for the application (one in a package)
- `"fmt"`: a package for formatting strings and printing from the golang standard library which contains packages for all kinds of different functionality,

### Variables, Strings and numbers

```go
var name string = "mario" // double quotes
var name2 = "luigi" // type inference
var name3 string // setting the var for future use - empty string is the default value
name4 := "yoshi" // shorthand version - just when initialising the var - cannot be used outside of a function
var age int = 20
var age2 = 18
age3 := 19

var num1 int8 = 12 // 8-bits integer
var num2 uint = 2 // unsigned integer

var score float32 = 333.33 // float64 is the default type when using shorthands
```

