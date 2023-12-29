- An open-source [[Programming]] language supported by Google
- Easy to learn and great for teams
- Built-in concurrency and a robust standard library
- Large ecosystem of partners, communities, and tools
Almost all contento of markdown Go content present here comes from [Exercism](https://exercism.org/tracks/go)
# Hello world
```go
package greeting

// HelloWorld greets the world.
func HelloWorld() string {
	return "Hello, World!"
}
```

## Packages
Go applications are organized in packages. A package is a collection of source files located in the same directory. All source files in a directory must share the same package name. When a package is imported, only entities (functions, types, variables, constants) whose names start with a capital letter can be used / accessed. The recommended style of naming in Go is that identifiers will be named using `camelCase`, except for those meant to be accessible across packages which should be `PascalCase`.

Go provides an extensive standard library of packages which you can use in your program using the `import` keyword. Standard library packages are imported using their name.
```go
package greeting

import "fmt"
```

An imported package is then addressed with the package name:
```go
world := "World"
fmt.Sprintf("Hello %s", world)
```

#### Access Modifiers
Go determines if an item can be called by code in other packages through how it is declared. To make a function, type, variable, constant or struct field externally visible (known as _exported_) the name must start with a capital letter.
```go
package greeting

// Hello is a public function (callable from other packages).
func Hello(name string) string {
    return "Hello " + name
}

// hello is a private function (not callable from other packages).
func hello(name string) string {
    return "Hello " + name
}
```

## Variables
Go is statically-typed, which means all variables [must have a defined type](https://en.wikipedia.org/wiki/Type_system) at compile-time.
Variables can be defined by explicitly specifying a type:

```go
var explicit int // Explicitly typed
```

You can also use an initializer, and the compiler will assign the variable type to match the type of the initializer.

```go
implicit := 10   // Implicitly typed as an int
```

Once declared, variables can be assigned values using the `=` operator. Once declared, a variable's type can never change.

```go
count := 1 // Assign initial value
count = 2  // Update to new value

count = false // This throws a compiler error due to assigning a non `int` type
```

### Constants
Constants hold a piece of data just like variables, but their value cannot change during the execution of the program.

Constants are defined using the `const` keyword and can be numbers, characters, strings or booleans:

```go
const Age = 21 // Defines a numeric constant 'Age' with the value of 21
```

### Functions
Go functions accept zero or more parameters. Parameters must be explicitly typed, there is no type inference. Values are returned from functions using the `return` keyword.

Note that Go supports two types of comments. Single line comments are preceded by `//` and multiline comments are inserted between `/*` and `*/`.

```go
package greeting

// Hello is a public function.
func Hello (name string) string {
    return hi(name)
}

// hi is a private function.
func hi (name string) string {
    return "hi " + name
}
```

## Booleans
Are represented by the predeclared boolean type `bool`, which values can be either `true` or `false`. It's a defined type.

```go
var closed bool    // boolean variable 'closed' implicitly initialized with 'false'
speeding := true   // boolean variable 'speeding' initialized with 'true'
hasError := false  // boolean variable 'hasError' initialized with 'false' 
```
Go supports three logical operators that can evaluate expressions down to Boolean values, returning either `true` or `false`.

|Operator|What it means|
|---|---|
|`&&` (and)|It is true if both statements are true.|
|`\|` (or)|It is true if at least one statement is true.|
|`!` (not)|

