Is commonly present in functional programming language. In [[Elixir]] id id used to match simple values, data structure and functions. I other programming language, there are similar of some pattern matches, named argument destructuring, array destructuring, etc.

The `=` operator is actually a match operator, comparable to the equals sign in algebra. Writing it turns the whole expression into an equation and makes Elixir match the values on the left hand with the values on the right hand. If the match succeeds, it returns the value of the equation. Otherwise, it throws an error. Let’s take a look:

```zsh
iex(1)> x=1
1
iex(2)> 1=x
1
iex(3)> 2=x
** (MatchError) no match of right hand side value: 1
```

In the major of programming languages the `x=1` code means that the x variable receive the 1 value, but in Elixir it does the ==match== of the two sides. In this case, if the variable doesn't exist, it assumes the value.

## Pin operator
In case of `x=2` the elixir will change the value of variable x to 2. To match with the variable in the left hand we need to use the pin operator `^`.
```zsh
iex(1)> x=1
1
iex(2)> 1=x
1
iex(3)> ^x=2
** (MatchError) no match of right hand side value: 1
```

## Some examples
### Tuples
```rb
iex(9)> {:ok, conteudo} = File.read("teste")
** (MatchError) no match of right hand side value: {:error, :enoent}

iex(9)> {:error, conteudo} = File.read("teste")
{:error, :enoent}
iex(10)> conteudo
:enoent
iex(11)> 
```
### Lists
in the example, `_` is used to ignore some part of match.
```rb
iex(1)> lista = [1,2,3]
[1, 2, 3]
iex(2)> hd(lista)
1
iex(3)> tl(lista)
[2, 3]
iex(4)> [cabeca|cauda] = lista
[1, 2, 3]
iex(5)> cabeca
1
iex(6)> cauda
[2, 3]
iex(7)> x=1
1
iex(8)> [a,^x,c] = lista
** (MatchError) no match of right hand side value: [1, 2, 3]

iex(8)> [a,2,c] = lista 
[1, 2, 3]
iex(9)> a
1
iex(10)> c
3
iex(11)> [a,_,c] = lista
[1, 2, 3]

```