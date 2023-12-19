In [[Rust]] we can declare an [[Array]] with type and size:
```rust
fn main() {
    let notas: [f32; 4] = [8.5, 9f32, 7.5, 10f32];
    
    for indice in 0..notas.len() {
        println!("A nota {} é = {}", indice + 1, notas[indice]);
    }
}
```

We can also repeat a and specific value in all positions of the array: 
```rust
let notas: [f32; 4] = [6.5; 4];
```