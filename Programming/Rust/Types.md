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

## Usize and Isize
In Rust, `usize` and `isize` are types that are used to represent sizes and counts. They are unsigned and signed integer types that are used for indexing and size computations.

- `usize`: This type is an unsigned integer type that is used for indexing collections. It is the type returned by the `len` method on collections. The size of `usize` is platform dependent. On a 32-bit platform, it is 32 bits, and on a 64-bit platform, it is 64 bits. This means that `usize` can represent a larger range of numbers on a 64-bit platform compared to a 32-bit platform.

- `isize`: This type is a signed integer type that is used for indexing collections. It is the type returned by the `len` method on collections. The size of `isize` is also platform dependent, but it is always signed. Like `usize`, the size of `isize` is 32 bits on a 32-bit platform and 64 bits on a 64-bit platform.

Here is an example of how you might use `usize` and `isize`:

```rust
let array: [i32; 5] = [1, 2, 3, 4, 5]; let len: usize = array.len(); // len is 5 let index: isize = -1; // index is -1
```


In this example, `len` is a `usize` and `index` is an `isize`. The `len` method returns the length of the array as a `usize`, and `index` is a negative number, so it is an `isize`.

Please note that these types are primarily used for indexing and size computations, and should not be used for arithmetic operations. If you need to perform arithmetic operations, you should use the appropriate integer types (`i32`, `i64`, etc.) instead.

Remember that the size of these types is platform dependent, so they can have different sizes on different platforms. Always check the size of these types on your target platform if you need to ensure that your code behaves consistently across different platforms.

# Enum
It allows to create custom types with predefined values.

```rust
fn main() {
    println!("É fim de semana? {}", eh_fim_de_semana(DiaDaSemana::Sabado));
}

enum DiaDaSemana {
    Domingo,
    Segunda,
    Terca,
    Quarta,
    Quinta,
    Sexata,
    Sabado,
}

fn eh_fim_de_semana(dia_da_semana: DiaDaSemana) -> bool {
    match dia_da_semana {
        DiaDaSemana::Domingo | DiaDaSemana::Sabado => true,
        _ => false,
    }
}
```

It became more powerful when we use tuples and structs together:
```rust
fn main() {
    cores();
}

enum Color {
    Red,
    Green,
    Blue,
    RgbColor(u8, u8, u8),
    CymkColor {
        cyan: u8,
        magenta: u8,
        yellow: u8,
        black: u8,
    },
}

fn cores() {
    let cor = Color::CymkColor {
        cyan: 100,
        magenta: 50,
        yellow: 70,
        black: 200,
    };

    println!(
        "Cor = {}",
        match cor {
            Color::Red => "vermelho",
            Color::Green => "verde",
            Color::Blue => "blue",
            Color::RgbColor(0, 0, 0)
            | Color::CymkColor {
                cyan: _,
                magenta: _,
                yellow: _,
                black: 255,
            } => "preta",
            Color::RgbColor(_, _, _) => "RGB desconhecido",
            Color::CymkColor {
                cyan: _,
                magenta: _,
                yellow: _,
                black: _,
            } => "CYMK desconhecido",
        }
    );
}
```
