## Collections

### List
  
Lists are simple collections of values which may include **multiple types**; lists may also include **non-unique** values. 
Its implementation is a [[Linked List]]. This means that get the list length is an operation that will run in linear time [[Algorithms#O(n)|O(n)]]. For this reason, it is typically faster to prepend than to append
```rb
[3.14, :pie, "Apple"]

iex> list = [3.14, :pie, "Apple"]
[3.14, :pie, "Apple"]

# Prepending (fast)
iex> ["π" | list]
["π", 3.14, :pie, "Apple"]

# Appending (slow)
iex> list ++ ["Cherry"]
[3.14, :pie, "Apple", "Cherry"]
```

#### List Concatenation
List concatenation uses the `++/2`(++ function name and arity 2) operator:
```rb
iex> [1, 2] ++ [3, 4, 1]
[1, 2, 3, 4, 1]

iex> [1,2,2,3,2,3] -- [1,2,3,2]
[2, 3]
```
#### List Subtraction
Support for subtraction is provided via the `--/2` operator; it’s safe to subtract a missing value.
**Note:** List subtraction uses [strict comparison](https://elixirschool.com/en/lessons/basics/basics#comparison) to match the values. For example:
```rb
iex> ["foo", :bar, 42] -- [42, "bar"]
["foo", :bar]

iex> [2] -- [2.0]
[2]
iex> [2.0] -- [2.0]
[]
```
#### Head and Tail
he head is the list’s first element, while the tail is a list containing the remaining elements. Elixir provides two helpful functions, `hd` and `tl`, for working with these parts:
```rb
iex> hd [3.14, :pie, "Apple"]
3.14

iex> tl [3.14, :pie, "Apple"]
[:pie, "Apple"]
```
Usingo [pattern matching](https://elixirschool.com/en/lessons/basics/pattern_matching):
```rb
iex> [head | tail] = [3.14, :pie, "Apple"]
[3.14, :pie, "Apple"]

iex> head
3.14

iex> tail
[:pie, "Apple"]
```

### Tuples
similar to lists, but are stored contiguously in memory (like [[Array]] [[Data Structure]]). This makes accessing their length fast but modification expensive; the new tuple must be copied entirely to memory. Tuples are defined with curly braces:

```rb
iex> {3.14, :pie, "Apple"}
{3.14, :pie, "Apple"}
```
Commonly used as a mechanism to return additional information from functions:
```rb
iex> File.read("path/to/existing/file")
{:ok, "... contents ..."}
iex> File.read("path/to/unknown/file")
{:error, :enoent}
```

### Keyword list
is a special list of two-element tuples whose first element is an atom; they share performance with lists:

```rb
iex> [foo: "bar", hello: "world"]
[foo: "bar", hello: "world"]
iex> [{:foo, "bar"}, {:hello, "world"}]
[foo: "bar", hello: "world"]
```

The three characteristics of keyword lists highlight their importance:

- Keys are atoms.
- Keys are ordered.
- Keys do not have to be unique.

For these reasons, keyword lists are most commonly used to pass options to functions.
### Maps
are the “go-to” key-value store. Unlike keyword lists, they allow keys of any type and are un-ordered.

```ruby
iex> map = %{:foo => "bar", "hello" => :world}
%{:foo => "bar", "hello" => :world}

iex> map[:foo]
"bar"

iex> map["hello"]
:world

iex> key = "hello"
"hello"
iex> %{key => "world"}
%{"hello" => "world"}
```
If a duplicate is added to a map, it will replace the former value:

```ruby
iex> %{:foo => "bar", :foo => "hello world"}
%{foo: "hello world"}
```

As we can see from the output above, there is a special syntax for maps containing only atom keys:

```ruby
iex> %{foo: "bar", hello: "world"}
%{foo: "bar", hello: "world"}
iex> %{foo: "bar", hello: "world"} == %{:foo => "bar", :hello => "world"}
true
```

In addition, there is a special syntax you can use with atom keys:

```ruby
iex> map = %{foo: "bar", hello: "world"}
%{foo: "bar", hello: "world"}
iex> map.hello
"world"
```

Another interesting property of maps is that they provide their own syntax for updates (note: this creates a new map):

```ruby
iex> map = %{foo: "bar", hello: "world"}
%{foo: "bar", hello: "world"}
iex> %{map | foo: "baz"}
%{foo: "baz", hello: "world"}
```
To create a new key, instead use [`Map.put/3`](https://hexdocs.pm/elixir/Map.html#put/3)

```ruby
iex> map = %{hello: "world"}
%{hello: "world"}
iex> %{map | foo: "baz"}
** (KeyError) key :foo not found in: %{hello: "world"}
    (stdlib) :maps.update(:foo, "baz", %{hello: "world"})
    (stdlib) erl_eval.erl:259: anonymous fn/2 in :erl_eval.expr/5
    (stdlib) lists.erl:1263: :lists.foldl/3
iex> Map.put(map, :foo, "baz")
%{foo: "baz", hello: "world"}
```
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

`uniq_by/2` also removes duplicates from enumerables, but it allows us to provide a function to do the uniqueness comparison.

```rb
iex> Enum.uniq_by([%{x: 1, y: 1}, %{x: 2, y: 1}, %{x: 3, y: 3}], fn coord -> coord.y end)
[%{x: 1, y: 1}, %{x: 3, y: 3}]
```
