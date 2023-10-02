## Condition
In [[Rust]], this is similar to others procedural languages like C. There are two examples of how to use condition in Rust. The first one is the common approach that we have in other languages, where we have a condition that executes a block of code. But the last one use the condition as a expression, so it returns a value instead of execute something.

```rust
fn condicionais() {
	let idade: u8 = 18;
	let responsavel_autorizou = true;
	let eh_maior = idade >= 18;
	
	if eh_maior {
		println!("Pode entrar!");
	} else if idade > 16 && responsavel_autorizou {
		println!("Pode entrar, mas com assinatura do responsável");
	} else {
		println!("Não pode entrar!");
	}
	
	let condicao = if eh_maior { "Maior de idade" } else { "Menor de idade" };
	println!("É {} de idade", condicao);
}
```

## Repetition control
### While and Loop
While need a condition and Loop will repeat infinitely, so to stop it will need a `break`:
```rust
fn repeticoes() {
	let multiplicador: u8 = 5;
	
	let mut contador: u8 = 0;
	while contador < 10 {
		contador += 1;
	if contador == 5 {
		continue;
	}
	println!("{} x {} = {}", multiplicador, contador, multiplicador * contador);
	}
	
	contador = 0;
	loop {
		contador += 1;
		println!("{} x {} = {}", multiplicador, contador, multiplicador * contador);
		if contador == 10 {
			break;
		}
	}
}
```

### For and Ranges
```rust
fn repeticoes() {
	let multiplicador: u8 = 5;
	
	for i in 1..11 {
		println!("{} x {} = {}", multiplicador, i, multiplicador * i);
	}
	
	//is the same as:
	for i in 1..=10 {
		println!("{} x {} = {}", multiplicador, i, multiplicador * i);
	}
}
```

### Match statements
provides pattern matching via the `match` keyword, which can be used like a C `switch`. The first matching arm is evaluated and all possible values must be covered:
```rust
fn main() {
    let number = 13;
    // TODO ^ Try different values for `number`

    println!("Tell me about {}", number);
    match number {
        // Match a single value
        1 => println!("One!"),
        // Match several values
        2 | 3 | 5 | 7 | 11 => println!("This is a prime"),
        // TODO ^ Try adding 13 to the list of prime values
        // Match an inclusive range
        13..=19 => println!("A teen"),
        // Handle the rest of cases
        _ => println!("Ain't special"),
        // TODO ^ Try commenting out this catch-all arm
    }

    let boolean = true;
    // Match is an expression too
    let binary = match boolean {
        // The arms of a match must cover all the possible values
        false => 0,
        true => 1,
        // TODO ^ Try commenting out one of these arms
    };
    println!("{} -> {}", boolean, binary);
}
```