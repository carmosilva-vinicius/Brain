In [[Elixir]] and many functional languages, functions are main entity. All functions should be defines inside a module.

## Syntax
There are different approaches to write functions.

```rb
defmodule MeuModulo.Math do
  def soma(a, b) do
    a + b
  end
end

# The same function with another syntax:
defmodule MeuModulo.Math do
  def soma(a, b) do
    a + b
  end
end
```

## Private functions
It can only be called from within their own Module. We define them in Elixir with `defp`:
```rb
defmodule MeuModulo do
  import IO, only: [puts: 1]
  import Kernel, except: [inspect: 1]

  alias MeuModulo.Math, as: MyMath

  def ola_mundo() do
    inspect(MyMath.soma(2, 2))
  end

  def exibe_se_for_par(numero) do
    require Integer
    puts("O número #{numero} é par? #{Integer.is_even(numero)}")
  end

  defp inspect(parametro) do
    puts("Começando a inspeção")
    puts(parametro)
    puts("Terminando a inspeção")
  end
end
```
Testing it in Interactive shell, I compiled a `test.exs` script, with the above module. The inspect function works just internally:
```rb
iex(4)> c "teste.exs"
[MeuModulo]

iex(5)> MeuModulo.inspect("teste")
** (UndefinedFunctionError) function MeuModulo.inspect/1 is undefined or private
    MeuModulo.inspect("teste")

iex(5)> MeuModulo.ola_mundo()
Começando a inspeção
4
Terminando a inspeção
:ok
```

## Anonymous function
Functions that has no name. To define an anonymous function in Elixir we need the `fn` and `end` keywords. Within these we can define any number of parameters and function bodies separated by `->`.

#### & shorthand
In the shorthand version our parameters are available to us as `&1`, `&2`, `&3`, and so on.

```rb
iex(8)> lista = [1,2,3]
[1, 2, 3]
iex(9)> Enum.map(lista, fn (numero) -> numero * 2 end)
[2, 4, 6]
iex(10)> Enum.map(lista, &(&1 * 2))                    
[2, 4, 6]
iex(11)> soma_2 = &(&1 + 2)
#Function<42.125776118/1 in :erl_eval.expr/6>
iex(12)> soma_2.(5)
7
```

### Store in variable
We can store a function inside a variable, to do it, we need to `&`and the arity of the funcion. And to call it, a dot `.` should be used. Example:
```rb
iex(1)> is_number(1)
true
iex(2)> i_n = &is_number/1
&:erlang.is_number/1
iex(3)> i_n.(2)
true
```