Is similar to [[Arrays]], but if a dynamic size.  So, it is contiguous grow-able. 
## Get method
Returns a reference to an element or sub-slice depending on the type of index.
- If given a position, returns a reference to the element at that position or `None` if out of bounds.
- If given a range, returns the sub-slice corresponding to that range, or `None` if out of bounds.

Example:
```rust
fn vectors() {
    let mut notas: Vec<f32> = Vec::new();
    notas.push(10.0);
    notas.push(8.8);
    notas.push(6.5);
    
    print!("{:?}", notas);
    
    notas.push(6.8);
    print!("{:?}", notas);
    
	println!("Nota 1 = {}", notas[0]);
	
    println!(
        "Nota 6 = {}",
        match notas.get(7) {
            Some(n) => *n, // or Some(&n) => n
            None => 0.0,
        }
    );
}
```

or

```rust
fn vectors() {
	let mut notas: Vec<f32> = vec![10.0, 8.0, 6.5];
	
    print!("{:?}", notas);
    
    notas.push(6.8);
    print!("{:?}", notas);
        
	println!("Nota 1 = {}", notas[0]);
	
    println!(
        "Nota 6 = {}",
        match notas.get(7) {
            Some(n) => *n, // or Some(&n) => n
            None => 0.0,
        }
    );
}
```

## Capacity
The `vec!` macro is an vector initialization approach that could be more efficient than allocation and initialization in different moments of the code. But we can also just allocate the vector memory in the [[Memory Management#Heap|Heap]], without input any data.

For each time a new value is entered and exceeds the capacity, it will be doubled.

```rust
fn vectors() {
    let mut notas: Vec<f32> = Vec::with_capacity(4);
    notas.push(10.0);
    notas.push(8.0);
    notas.push(6.5);
    println!("Capacity = {}", notas.capacity());

    println!("{:?}", notas);

    notas.push(6.8);
    println!("Capacity = {}", notas.capacity());
    println!("{:?}", notas);

    println!("Nota 1 = {}", notas[0]);

    println!(
        "Nota 6 = {}",
        match notas.get(7) {
            Some(n) => *n, // or Some(&n) => n
            None => 0.0,
        }
    );

    /*
    while let Some(nota) = notas.pop() {
        println!("Valor removido = {}" nota);
    }
    */
    for nota in &notas {
        println!("Nota = {}", nota);
    }

    println!("{:?}", notas)
}
```