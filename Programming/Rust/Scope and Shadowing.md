In [[Rust]] we can separate scopes using `{}`, and separate the accessibility of variables. Defining more than one variable with the same name and in the same scope is allowed in Rust, but the previous one will not working anymore.

When we create a new scope, it inherits the outside ones. But in Elixir we can use ==Shadowing==, which allow us to override an specific variable just inside the scope, maintaining the original value in the outside of the scope:

```rust
fn main() {
	let a = 123;

	//new scope
	{
		let b  = 456;
		println!("dentro, b = {}", b);
		
		let a  = 777;
		println!("dentro, a = {}", a);
	}

	println!("fora, a = {}", a);
}
```