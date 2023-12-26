A `string` in Go is an immutable sequence of bytes, which don't necessarily have to represent characters.

A string literal is defined between double quotes:
```go
const name = "Jane"
```

Strings can be concatenated via the `+` operator:
```go
"Jane" + " " + "Austen"
// => "Jane Austen"
```

Some special characters need to be escaped with a leading backslash, such as `\t` for a tab and `\n` for a new line in strings.
```go
"How is the weather today?\nIt's sunny"  
// =>
// How is the weather today?
// It's sunny
```

The `strings` package contains many useful functions to work on strings. For more information about string functions, check out the [strings package documentation](https://pkg.go.dev/strings). Here are some examples:
```go
import "strings"

// strings.ToLower returns the string given as argument with all its characters lowercased
strings.ToLower("MaKEmeLoweRCase")
// => "makemelowercase"

// strings.Repeat returns a string with a substring given as argument repeated many times
strings.Repeat("Go", 3)
// => "GoGoGo"
```
# String formatting
[[Go]] provides an in-built package called `fmt` (format package) which offers a variety of functions to manipulate the format of input and output. The most commonly used function is `Sprintf`, which uses verbs like `%s` to interpolate values into a string and returns that string.

```go
import "fmt"

food := "taco"
fmt.Sprintf("Bring me a %s", food)
// Returns: Bring me a taco
```

In Go floating point values are conveniently formatted with Sprintf's verbs: `%g` (compact representation), `%e` (exponent) or `%f` (non exponent). All three verbs allow the field's width and numeric position to be controlled.

```go
import "fmt"

number := 4.3242
fmt.Sprintf("%.2f", number)
// Returns: 4.32
```

You can find a full list of available verbs in the [format package documentation](https://pkg.go.dev/fmt).

`fmt` contains other functions for working with strings, such as `Println` which simply prints the arguments it receives to the console and `Printf` which formats the input in the same way as `Sprintf` before printing it.