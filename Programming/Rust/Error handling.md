[[Rust]] handles errors by categorizing them into recoverable and unrecoverable errors. Recoverable errors, like a file not found, can be dealt with by reporting to the user and retrying the operation. On the other hand, unrecoverable errors, which are typically bugs in the code, need to stop the program immediately. Rust uses the `Result<T, E>` type for recoverable errors and the `panic!` macro for unrecoverable errors [doc.rust-lang.org](https://doc.rust-lang.org/book/ch09-02-recoverable-errors-with-result.html?highlight=Result).

For recoverable errors, Rust uses a `Result<T, E>` enum where `T` and `E` are generic type parameters. `T` represents the type of the value that will be returned in the success case within the `Ok` variant, and `E` stands for the type of the error that will be returned in the failure case within the `Err` variant.

### Examples
```rust
fn erros() {
	panic!("Erro proposital");
}
```

```rust
fn erros() {
	match resultado() {
		Ok(s) => println!("String de sucesso = {}", s),
		Err(numero) => println!("Código de erro = {}", numero)
	}
}

fn resultado() -> Result<String, u8>{
	Err(42)
}
```