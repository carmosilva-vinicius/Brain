in [[Elixir]] are a way to add more complex checks to pattern matching. They can be used in function definitions, case clauses, and other constructs where pattern matching is allowed. Guard clauses are a set of predicates that are attached to a function definition using the `when` keyword.

In the example bellow guard helps the function `zero?` to works just with integers and when a non integer value is used it returns an error: 
```rb
defmodule MeuModulo.Math do
	def soma(a, b), do: a + b
	
	def zero?(0), do: true
	def zero?(x) when(is_integer(x)), do: false
end
```

#### Testing:
```rb
Interactive Elixir (1.15.4) - press Ctrl+C to exit (type h() ENTER for help)
iex(1)> MeuModulo.Math.zero?(0)
true
iex(2)> MeuModulo.Math.zero?(4)
false
iex(3)> MeuModulo.Math.zero?([4,2])
** (FunctionClauseError) no function clause matching in MeuModulo.Math.zero?/1    
    
    The following arguments were given to MeuModulo.Math.zero?/1:
    
        # 1
        [4, 2]
    
    math.exs:4: MeuModulo.Math.zero?/1
```