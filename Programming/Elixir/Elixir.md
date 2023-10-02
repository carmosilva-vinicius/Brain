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

