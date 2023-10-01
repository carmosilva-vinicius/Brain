[[Elixir]] functions are declared with `fn`. Its arguments are type annotated, just like variables, and, if the function returns a value, the return type must be specified after an arrow `->`.

Omitting the `;` function will be used as return value. Alternatively, the `return` statement can be used to return a value earlier.

```rust
fn soma(a:i32, b:i32) -> i:32
{
	println!("{} + {} = {}", a, b, a+b);
	a + b
}
```