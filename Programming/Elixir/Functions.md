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

## Default arguments
In functions a default value for a input is defined using the `argument \\ value` syntax:
```rb
def join(a, b, sp \\ " ") do
	a <> sp <> b
end
```

But is important to know that Elixir doesn’t like default arguments in multiple matching functions. Loading the module below in the iterative shell we can see the some warnings:

```rb
defmodule MeuModulo.Concat do
	def join(a, b, sp \\ " ") do
		a <> sp <> b
	end
	def join(a, b, _sp) when is_nil(b) do
		a
	end
end
```

There are two warnings, the first on suggest to define the function default values in a header. This will eliminate the confusion with default value with multiple clauses.

The second warns that the second definitions of `join` not match because the first one always match, so we need to change the order of functions.
```zsh
warning: def join/3 has multiple clauses and also declares default values. In such cases, the default values should be defined in a header. Instead of:

    def foo(:first_clause, b \\ :default) do ... end
    def foo(:second_clause, b) do ... end

one should write:

    def foo(a, b \\ :default)
    def foo(:first_clause, b) do ... end
    def foo(:second_clause, b) do ... end

  concat.exs:7

warning: this clause for join/3 cannot match because a previous clause at line 3 always matches
  concat.exs:7
```

Solution:
```rb
defmodule MeuModulo.Concat do
	def join(a, b \\ nil, sp \\ " ")
	
	def join(a, b, _sp) when is_nil(b) do
		a
	end
	
	def join(a, b, sp) do
		a <> sp <> b
	end
end
```

## Recursion
- Tail recursion is generally more efficient and uses constant stack space because the compiler or interpreter can optimize it. It is particularly useful when dealing with large inputs, variable inputs, or streaming data.
- Body recursion may be simpler to write and understand in some cases, especially when the additional operations after the recursive call are necessary.
- In some cases, body recursion may be faster than tail recursion. For example, if the tail-recursive version of a function requires reversing a list, it may be slower than the body-recursive version that doesn't require reversing.
### Body recursion
the recursive call is not the last operation performed in the function. This means that there are additional operations or calculations performed after the recursive call. Body recursion requires more stack space because each recursive call adds a new frame to the call stack.
### Tail recursion
the recursive call is the last operation performed in the function. This means that there is no need to keep track of any additional state or perform any operations after the recursive call. Tail recursion is often considered more efficient because it can be optimized by the compiler or interpreter to use constant stack space (==Tail Call Optimization==).
```rb
defmodule MeuModulo.Tabuada do
	def calcula(multiplicador) do
		tabuada(multiplicador, 1, [])
	end
	
	def tabuada(_, 11, valores), do: valores
	def tabuada(produto1, produto2, valores) do
		tabuada(produto1, produto2 + 1, valores ++ [produto1 * produto2])
	end
end
```