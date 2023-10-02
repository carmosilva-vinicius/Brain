The pipe operator `|>` passes the result of an expression as the first parameter of another expression.
```rb
iex(5)> Enum.sum(Enum.filter(Enum.map(1..10, &(&1 * 5)), &Integer.is_even(&1)))
150

# With pipes:
iex(6)> 1..10 |>
...(6)> Enum.map(&(&1 * 5)) |>
...(6)> Enum.filter(&Integer.is_even(&1)) |> 
...(6)> Enum.sum()
150
iex(7)> 
```