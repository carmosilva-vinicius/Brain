In [[Go]] numbers can be compared using the following relational and equality operators.

|Comparison|Operator|
|---|---|
|equal|`==`|
|not equal|`!=`|
|less|`<`|
|less or equal|`<=`|
|greater|`>`|
|greater or equal|`>=`|

The result of the comparison is always a boolean value, so either `true` or `false`.
```go
a := 3

a != 4 // true
a > 5  // false
```

The comparison operators above can also be used to compare strings. In that case a lexicographical (dictionary) order is applied. For example:
```Go
	"apple" < "banana"  // true
	"apple" > "banana"  // false
```

### If Statements
Conditionals in Go are similar to conditionals in other languages. The underlying type of any conditional operation is the `bool` type, which can have the value of `true` or `false`. Conditionals are often used as flow control mechanisms to check for various conditions.

For checking a particular case an `if` statement can be used, which executes its code if the underlying condition is `true` like this:
```go
var value string

if value == "val" {
    return "was val"
}
```

In scenarios involving more than one case many `if` statements can be chained together using the `else if` and `else` statements.
```go
var number int
result := "This number is "

if number > 0 {
    result += "positive"
} else if number < 0 {
    result += "negative"
} else {
    result += "zero"
}
```

If statements can also include a short initialization statement that can be used to initialize one or more variables for the if statement. For example:
```go
num := 7
if v := 2 * num; v > 10 {
    fmt.Println(v)
} else {
    fmt.Println(num)
}
// Output: 14
```

> Note: any variables created in the initialization statement go out of scope after the end of the if statement.

# Switch statement
Like other languages, Go also provides a `switch` statement. Switch statements are a shorter way to write long `if ... else if` statements. To make a switch, we start by using the keyword `switch` followed by a value or expression. We then declare each one of the conditions with the `case` keyword. We can also declare a `default` case, that will run when none of the previous `case` conditions matched:
```go
operatingSystem := "windows"

switch operatingSystem {
case "windows":
    // do something if the operating system is windows
case "linux":
    // do something if the operating system is linux
case "macos":
    // do something if the operating system is macos
default:
    // do something if the operating system is none of the above
} 
```

One interesting thing about switch statements, is that the value after the `switch` keyword can be omitted, and we can have boolean conditions for each `case`:
```go
age := 21

switch {
case age > 20 && age < 30:
    // do something if age is between 20 and 30
case age == 10:
    // do something if age is equal to 10
default:
    // do something else for every other case
}
```