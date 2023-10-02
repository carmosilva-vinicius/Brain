## Enum
Is a set of [[Algorithms | algorithms]]  for enumerating over enumerables. Enumeration is at the core of functional programming, and combined with other perks of Elixir it can be incredibly empowering for developers.
The `Enum` module includes over 70 functions for working with enumerables. All the [[Elixir#Collections|Collections]] that we mention before, with the exception of tuples, are enumerables.

Listing this functions:

```rb
iex> Enum.__info__(:functions) |> Enum.each(fn({function, arity}) ->
...>   IO.puts "#{function}/#{arity}"
...> end)
all?/1
all?/2
any?/1
any?/2
at/2
at/3
...
```
### all?
Returns `true` if the entire elements in `enumerable` evaluate to `true`.
When an element has a falsy value (`false` or `nil`) iteration stops immediately and `false` is returned. In all other cases `true` is returned:
```rb
iex> Enum.all?(["foo", "bar", "hello"], fn(s) -> String.length(s) == 3 end)
false
iex> Enum.all?(["foo", "bar", "hello"], fn(s) -> String.length(s) > 1 end)
true
```
### any?
Unlike the `all?/2`, this will return true if at leas one element in `enumerable` evaluates to true:
```rb
iex> Enum.any?(["foo", "bar", "hello"], fn(s) -> String.length(s) == 5 end)
true
```
### chunk_every
to break your collection up into smaller groups, `chunk_every/2` is the function you’re probably looking for:
```rb
iex> Enum.chunk_every([1, 2, 3, 4, 5, 6], 2)
[[1, 2], [3, 4], [5, 6]]
```
### chunk_by
Splits enumerable on every element for which `fun` returns a new value.
In the examples below, each string of the same length is grouped together until we encounter a new string of a new length:
```rb
iex> Enum.chunk_by(["one", "two", "three", "four", "five"], fn(x) -> String.length(x) end)
[["one", "two"], ["three"], ["four", "five"]]

iex> Enum.chunk_by(["one", "two", "three", "four", "five", "six"], fn(x) -> String.length(x) end)
[["one", "two"], ["three"], ["four", "five"], ["six"]]
```
### map_every
Sometimes chunking out a collection isn’t enough for exactly what we may need. If this is the case, `map_every/3` can be very useful to hit every `nth` items, always hitting the first one:
```rb
# Apply function every three items
iex> Enum.map_every([1, 2, 3, 4, 5, 6, 7, 8], 3, fn x -> x + 1000 end)
[1001, 2, 3, 1004, 5, 6, 1007, 8]
```
### each
It may be necessary to iterate over a collection without producing a new value, for this case we use `each/2`:
```rb
iex> Enum.each(["one", "two", "three"], fn(s) -> IO.puts(s) end)
one
two
three
:ok
```
**Note**: The `each/2` function does return the atom `:ok`.
### map
To apply our function to each item and produce a new collection look to the `map/2` function:
```rb
iex> Enum.map([0, 1, 2, 3], fn(x) -> x - 1 end)
[-1, 0, 1, 2]

#or
iex> Enum.map([0, 1, 2, 3], &(&1 - 1) end)
[-1, 0, 1, 2]
```
### min
`min/1` finds the minimal value in the collection:
```rb
iex> Enum.min([5, 3, 0, -1])
-1
```
`min/2` does the same, but in case the enumerable is empty, it allows us to specify a function to produce the minimum value.
```rb
iex> Enum.min([], fn -> :foo end)
:foo
```
### max
`max/1` returns the maximal value in the collection:
```rb
iex> Enum.max([5, 3, 0, -1])
5
```
`max/2` is to `max/1` what `min/2` is to `min/1`:
```rb
iex> Enum.max([], fn -> :bar end)
:bar
```
### filter
The `filter/2` function enables us to filter the collection to include only those elements that evaluate to `true` using the provided function.
```rb
iex> Enum.filter([1, 2, 3, 4], fn(x) -> rem(x, 2) == 0 end)
[2, 4]
```
### reduce
With `reduce/3` we can distill our collection down into a single value. To do this we supply an optional accumulator (`10` in this example) to be passed into our function; if no accumulator is provided the first element in the enumerable is used:
```rb
iex> Enum.reduce([1, 2, 3], 10, fn(x, acc) -> x + acc end)
16

iex> Enum.reduce([1, 2, 3], fn(x, acc) -> x + acc end)
6

iex> Enum.reduce(["a","b","c"], "1", fn(x,acc)-> x <> acc end)
"cba1"
```
### sort
Sorting our collections is made easy with not one, but two, sorting functions.
`sort/1` uses Erlang’s [term ordering](http://erlang.org/doc/reference_manual/expressions.html#term-comparisons) to determine the sorted order:
```rb
iex> Enum.sort([5, 6, 1, 3, -1, 4])
[-1, 1, 3, 4, 5, 6]

iex> Enum.sort([:foo, "bar", Enum, -1, 4])
[-1, 4, Enum, :foo, "bar"]
```
While `sort/2` allows us to provide a sorting function of our own:
```rb
# with our function
iex> Enum.sort([%{:val => 4}, %{:val => 1}], fn(x, y) -> x[:val] > y[:val] end)
[%{val: 4}, %{val: 1}]

# without
iex> Enum.sort([%{:count => 4}, %{:count => 1}])
[%{count: 1}, %{count: 4}]
```
For convenience, `sort/2` allows us to pass `:asc` or `:desc` as the sorting function:
```rb
Enum.sort([2, 3, 1], :desc)
[3, 2, 1]
```
### uniq
We can use `uniq/1` to remove duplicates from our enumerables:
```rb
iex> Enum.uniq([1, 2, 3, 2, 1, 1, 1, 1, 1])
[1, 2, 3]
```
## uniq_by
`uniq_by/2` also removes duplicates from enumerables, but it allows us to provide a function to do the uniqueness comparison:
```rb
iex> Enum.uniq_by([%{x: 1, y: 1}, %{x: 2, y: 1}, %{x: 3, y: 3}], fn coord -> coord.y end)
[%{x: 1, y: 1}, %{x: 3, y: 3}]
```

## Ranges
```rb
iex(1)> 1..10
1..10
iex(2)> Enum.to_list(1..10)
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
iex(3)> Enum.to_list(1..10//2)
[1, 3, 5, 7, 9]
iex(4)> Enum.map(1..10, &(&1 * 5))
[5, 10, 15, 20, 25, 30, 35, 40, 45, 50]
iex(5)> 1..1000000
1..1000000
iex(6)> Enum.to_list(1..1_000_000)
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22,
 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42,
 43, 44, 45, 46, 47, 48, 49, 50, ...]
```

# Stream
Functions for creating and composing streams.

Streams are composable, lazy enumerables (for an introduction on enumerables, see the [`Enum`](https://hexdocs.pm/elixir/1.15.6/Enum.html) module). Any enumerable that generates elements one by one during enumeration is called a stream.
```rb
iex(1)> 1..1_000_000 |>
...(1)> Stream.map(&(&1 * 5))
#Stream<[enum: 1..1000000, funs: [#Function<48.48886818/1 in Stream.map/2>]]>
```

#### Why to use Stream instead of Enum?
Below we have two examples using pipes. the first one is more efficient because the Stream organize all the data structure and pipe calculations functions and execute just at the final `Enum.sum()` function.
On the other hand for each `Enum` function, the range is traveled to execute. So in the last example the run through the range three times, but the first just once.
```rb
iex(5)> 1..1_000_000 |>
...(5)> Stream.map(&(&1 * 5)) |>
...(5)> Stream.filter(&Integer.is_even(&1)) |>
...(5)> Enum.sum()
1250002500000

iex(7)> 1..1_000_000 |>
...(7)> Enum.map(&(&1 * 5)) |>  
...(7)> Enum.filter(&Integer.is_even(&1)) |>  
...(7)> Enum.sum()
1250002500000
```