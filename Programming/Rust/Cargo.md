Is the [[Rust]] dependency and build manager. It uses the `src` folder to organize the code and `Cargo.toml` to store the dependencies and package information. That is a basic structure of this file:
```toml
[package]
name = "rust_studies"
version = "0.0.1"
authors = ["Vinícius Henrique <vini@co.dev>"]
```

### New project
We can start a new project with Cargo [[CLI]]:
```zsh
$ cargo new rust_hello_world
```
And run it:
```zsh
$ cargo run
```