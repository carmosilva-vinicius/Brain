Is the optional [[Types|type]] of Rust, where the value can be `Some(type)` or `None`. It is a way to rust deal with missing values safety, not allowing `null`. Common applications:

- Initial values
- Return values for functions that are not defined over their entire input range (partial functions)
- Return value for otherwise reporting simple errors, where [`None`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None "variant std::option::Option::None") is returned on error
- Optional struct fields
- Struct fields that can be loaned or “taken”
- Optional function arguments
- Nullable pointers
- Swapping things out of difficult situations

```rust
fn conteudo_opcional() {
    let conteudo_arquivo = ler_arquivo(String::from(""));
    
    match &conteudo_arquivo {
        Some(valor) => println!("{}", valor),
        None => print!("Arquivo não existe"),
    }
	
    print!("{:?}", conteudo_arquivo)
}
```

{:?}: This is a format specification within the print macro. The colon (:) introduces the format specifiers, and the ? indicates that the type of the variable being printed implements the Debug trait. This means that the Debug implementation for the type of conteudo_arquivo will determine how it is printed. The Debug trait provides a way to represent complex data structures in a human-readable form, typically used for debugging purposes.

## if let
Another approach to deal with optional values, is use `if let` flow control  statement. It is similar to  [[Programming/Rust/Pattern Matching|match]], but with a single condition.
```rust
fn conteudo_opcional() {
    let conteudo_arquivo = ler_arquivo(String::from(""));
    
    if let Some(valor) = conteudo_arquivo {
	    println!("Agora, tenho certeza que ha o valor {}", valor);
    }
}
```

