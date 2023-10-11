In [[Rust]] we have:
- [never](https://doc.rust-lang.org/std/primitive.never.html "primitive std::never")Experimental: The `!` type, also called “never”.
- [array](https://doc.rust-lang.org/std/primitive.array.html "primitive std::array"): A fixed-size array, denoted `[T; N]`, for the element type, `T`, and the non-negative compile-time constant size, `N`.
- [bool](https://doc.rust-lang.org/std/primitive.bool.html "primitive std::bool"): The boolean type.
- [char](https://doc.rust-lang.org/std/primitive.char.html "primitive std::char"): A character type.
- [f32](https://doc.rust-lang.org/std/primitive.f32.html "primitive std::f32"): A 32-bit floating point type (specifically, the “binary32” type defined in IEEE 754-2008).
- [f64](https://doc.rust-lang.org/std/primitive.f64.html "primitive std::f64"): A 64-bit floating point type (specifically, the “binary64” type defined in IEEE 754-2008).
- [fn](https://doc.rust-lang.org/std/primitive.fn.html "primitive std::fn"): Function pointers, like `fn(usize) -> bool`.
- [i8](https://doc.rust-lang.org/std/primitive.i8.html "primitive std::i8"): The 8-bit signed integer type.
- [i16](https://doc.rust-lang.org/std/primitive.i16.html "primitive std::i16"): The 16-bit signed integer type.
- [i32](https://doc.rust-lang.org/std/primitive.i32.html "primitive std::i32"): The 32-bit signed integer type.
- [i64](https://doc.rust-lang.org/std/primitive.i64.html "primitive std::i64"): The 64-bit signed integer type.
- [i128](https://doc.rust-lang.org/std/primitive.i128.html "primitive std::i128"): The 128-bit signed integer type.
- [isize](https://doc.rust-lang.org/std/primitive.isize.html "primitive std::isize"): The pointer-sized signed integer type.
- [pointer](https://doc.rust-lang.org/std/primitive.pointer.html "primitive std::pointer"): Raw, unsafe pointers, `*const T`, and `*mut T`.
- [reference](https://doc.rust-lang.org/std/primitive.reference.html "primitive std::reference"): References, `&T` and `&mut T`.
- [slice](https://doc.rust-lang.org/std/primitive.slice.html "primitive std::slice"): A dynamically-sized view into a contiguous sequence, `[T]`. Contiguous here means that elements are laid out so that every element is the same distance from its neighbors.
- [str](https://doc.rust-lang.org/std/primitive.str.html "primitive std::str"): String slices.
- [tuple](https://doc.rust-lang.org/std/primitive.tuple.html "primitive std::tuple"): A finite heterogeneous sequence, `(T, U, ..)`.
- [u8](https://doc.rust-lang.org/std/primitive.u8.html "primitive std::u8"): The 8-bit unsigned integer type.
- [u16](https://doc.rust-lang.org/std/primitive.u16.html "primitive std::u16"): The 16-bit unsigned integer type.
- [u32](https://doc.rust-lang.org/std/primitive.u32.html "primitive std::u32"): The 32-bit unsigned integer type.
- [u64](https://doc.rust-lang.org/std/primitive.u64.html "primitive std::u64"): The 64-bit unsigned integer type.
- [u128](https://doc.rust-lang.org/std/primitive.u128.html "primitive std::u128"): The 128-bit unsigned integer type.
- [unit](https://doc.rust-lang.org/std/primitive.unit.html "primitive std::unit"): The `()` type, also called “unit”.
- [usize](https://doc.rust-lang.org/std/primitive.usize.html "primitive std::usize"): The pointer-sized unsigned integer type.
### Examples:
```rust
fn main() {
	let variavel:i16 = 300;
	println!("Variavel: {}, tamanho: {} bytes", variavel, std::mem::size_of_val(&variavel));
	
	let decimal: f32 = 3.14;
	println!("Decimal: {}, tamanho: {} bytes", decimal, std::mem::size_of_val(&decimal));
	
	let mut booleano: bool = false;
	booleano = true;
	println!("Booleano: {}, tamanho: {} bytes", booleano, std::mem::size_of_val(&booleano));
	
	let letra: char = 'C';
	println!("Letra: {}, tamanho: {} bytes", letra, std::mem::size_of_val(&letra));
}
```

## Consts
To use const values, the type and the value should always be defined.

When we use variables, the compiler allocate the value and some address and get the value when it is called. And it is done in running time. But consts are processed in compiling time, the compiler don't stores it in memory, the values is embedded directly in the binary.

## Static
Similar to consts, value and type are required on the definitions. On the other hand, static is allocated in memory, so it has reference and can be modified, as global variables.
```rust
const PI: f32 = 3.14;
static mut GLOBAL:u8 = 1;

fn main() {
	println!("PI: {}", PI);
	println!("GLOBAL: {}", {GLOBAL});
}
```

But the compiler consider that use ==global mutable== variables is unsafe and not a good practice.[Error code E0133](https://doc.rust-lang.org/error_codes/E0133.html#error-code-e0133): Unsafe code was used outside of an unsafe block.
```rb
error[E0133]: use of mutable static is unsafe and requires unsafe function or block
 --> main.rs:8:29
  |
8 |     println!("GLOBAL: {}", {GLOBAL});
  |                             ^^^^^^ use of mutable static
  |
  = note: mutable statics can be mutated by multiple threads: aliasing violations or data races will cause undefined behavior
```

We can solve it creating an unsafe block:
```rust
const PI: f32 = 3.14;
static mut GLOBAL:u8 = 1;

fn main() {
	unsafe{
		println!("PI: {}", PI);
	}
	println!("GLOBAL: {}", {GLOBAL});
}
```
