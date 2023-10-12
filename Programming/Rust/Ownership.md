This is why [[Rust]] is considered a safe memory language. Ownership is Rust’s most unique feature and has deep implications for the rest of the language. It allows to manage memory allocation safety without using garbage collector.

Lets use some example:
When we define a `String`, a memory in the [[Memory Management#Heap|Heap]] will be allocated to save the text. Initially, in the example bellow the `um_string` will be the owner of this heap memory value. But when we pass the variable to a functions the ownership of the value in the memory will be transferred to the `string` variable int he `rouba` function scope. When the function `rouba` finish the string will be out of te scope, then it will be automatically freed, without need a garbage collector or an action from the programmer.
```rust
fn main(){
	ownership();
}

fn ownership(){
	let uma_string = String::from("Vini");
	rouba(uma_string);
}

fn rouba(string: String){
	 println!("{}", string);
}
```

If we try to use this the var after pass the ownership to another scope we will have error:
```rust
fn main(){
	ownership();
}

fn ownership(){
	let uma_string = String::from("Vini");
	rouba(uma_string);
	
	println!("{}", uma_string);
}

fn rouba(string: String){
	 println!("{}", string);
}
```

```c
error[E0382]: borrow of moved value: `uma_string`
  --> main.rs:9:18
   |
6  |   let uma_string = String::from("Vini");
   |       ---------- move occurs because `uma_string` has type `String`, which does not implement the `Copy` trait
7  |   rouba(uma_string);
   |         ---------- value moved here
8  |
9  |   println!("{}", uma_string); // Erro, pois a string foi movida para a função rouba
   |                  ^^^^^^^^^^ value borrowed here after move
   |
note: consider changing this parameter type in function `rouba` to borrow instead if owning the value isn't necessary
  --> main.rs:12:18
   |
12 | fn rouba(string: String){
   |    -----         ^^^^^^ this parameter takes ownership of the value
   |    |
   |    in this function
   = note: this error originates in the macro `$crate::format_args_nl` which comes from the expansion of the macro `println` (in Nightly builds, run with -Z macro-backtrace for more info)
help: consider cloning the value if the performance cost is acceptable
   |
7  |   rouba(uma_string.clone());
   |                   ++++++++

error: aborting due to previous error
```
To solve this we can solve this return the same value:
```rust
fn main(){
	ownership();
}

fn ownership(){
	let uma_string = String::from("Vini");
	let outra_string = rouba(uma_string);
	
	println!("{}", outra_string);
}

fn rouba(string: String) -> String {
	 println!("{}", string);
	
	string
}
```

## References e Borrowing
The above code is not a good approach, because we are depending to always return the value. We can use the **Borrowing** to pass the value, as reference, to another scope.
```rust
fn main(){
	ownership();
}

fn ownership(){
	let uma_string = String::from("Vini");
	rouba(uma_string);
	
	println!("{}", uma_string);
}

fn rouba(string: String){
	 println!("{}", string);
}
```
But the another scope still couldn't modify the variable, because it is immutable. If we try:
```c
error[E0596]: cannot borrow `*string` as mutable, as it is behind a `&` reference
  --> main.rs:13:3
   |
13 |   string.push_str(" Henrique");
   |   ^^^^^^^^^^^^^^^^^^^^^^^^^^^^ `string` is a `&` reference, so the data it refers to cannot be borrowed as mutable
   |
help: consider changing this to be a mutable reference
   |
12 | fn rouba(string: &mut String){
   |                   +++

error: aborting due to previous error

For more information about this error, try `rustc --explain E0596`.
```
So, to be able to change we need to change the variable source and reference to mutable:
```rust
fn main(){
	ownership();
}

fn ownership(){
	let mut uma_string = String::from("Vini");
	
	rouba(&mut uma_string);
	
	println!("{}", uma_string); // Erro, pois a string foi movida para a função rouba
}

fn rouba(string: &mut String){
	string.push_str(" Henrique");
	println!("{}", string);
}
```