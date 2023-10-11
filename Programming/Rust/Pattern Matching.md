Example [[Programming/Elixir/Pattern matching|Pattern matching]]  of in [[Rust]].
```rust
fn main(){
	pattern_matching();
}

fn pattern_matching(){
	for x in 1..=20 {
		println!("{}: {}", x, match x {
			1 => "Pouco",
			2 | 3 => "Um pouquinho",
			4..=10 => "Um bocado",
			_ if x % 2 == 0 => "Uma boa quantidade",
			_ => "Muitos!"
		});
	}
}
```