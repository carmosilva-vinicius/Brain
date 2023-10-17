Unit testing framework for [[Elixir]].

To start ExUnit:
```rb
ExUnit.start()
```

To test, the `ExUnit.Case` should be used:
```rb
defmodule ElixirTestTest do	
	use ExUnit.Case
	doctest ElixirTest
	
	test "greets the world" do
		assert ElixirTest.hello() == :world
	end
end
```

To run the tests of a project:
```
mix test
```

To run tests of a specific file:
```
mix test test/elixir_test_test.exs
```

## Tags
This can be use to manage which tests will be executed. The standard tag is `:test`.

```rb
defmodule ElixirTestTest do	
	use ExUnit.Case
	doctest ElixirTest
	
	test "greets the world" do
		assert ElixirTest.hello() == :world
	end
	
	@tag falha: true
	test "teste que falha de propósito" do
		assert ElixirTest.hello() != :world
	end
end
```

To run tests of a specific tag:
```
mix test --only falha
```

To run tests of a specific tag:
```
mix test --exclude falha
```