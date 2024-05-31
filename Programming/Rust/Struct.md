Is a way to create custom types in rust. It is similar to classes of other languages. So it allow to create a type divided in named pieces of data. Struct are stored directly in [[Memory Management#Stack|Stack]].

Methods can be implemented using `impl` keyword.

```rust
struct Conta {
    titular: Titular,
    saldo: f64,
}
impl Conta {
    fn sacar(&mut self, valor: f64) {
        self.saldo -= valor;
    }
}

struct Titular {
    nome: String,
    sobrenome: String,
}

fn conta_corrente() {
    let titular = Titular {
        nome: String::from("Vinícius"),
        sobrenome: String::from("Silva"),
    };
    let mut conta: Conta = Conta {
        titular,
        saldo: 100.0,
    };

    conta.sacar(50.0);

    println!(
        "
        Dados da conta: Titular = {} {}, Saldo = {}",
        conta.titular.nome, conta.titular.sobrenome, conta.saldo
    );
}
```