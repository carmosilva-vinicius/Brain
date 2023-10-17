Doctests in Elixir are a way to include examples in module documentation and automatically test them. They are written as code snippets in the `@doc` attribute of a module or function[1](https://hexdocs.pm/elixir/1.12/writing-documentation.html)[3](https://dev.to/sampriddy/works-as-shown-elixirs-doctest-macro-2gmj). Here's how they work:

1. Doctests are written within the `@doc` attribute using the `iex>` prompt to indicate the code snippe[1](https://hexdocs.pm/elixir/1.12/writing-documentation.html)[3](https://dev.to/sampriddy/works-as-shown-elixirs-doctest-macro-2gmj). For example:

```rb
@doc """
Says hello to the given `name`.
Returns `:ok`.

## Examples

    iex> MyApp.Hello.world(:john)
    :ok
"""
```

2. The doctests are executed using the [[ExUnit]] framework, which parses the code snippets and compares the expected output with the actual output[1](https://hexdocs.pm/elixir/1.12/writing-documentation.html). If the output matches, the test passes; otherwise, it fails.

3. Doctests are a great way to ensure that the examples in your documentation stay up to date and correct over time[3](https://dev.to/sampriddy/works-as-shown-elixirs-doctest-macro-2gmj). They serve as both documentation and tests, helping to validate the behavior of your code.

4. Doctests work well for simple examples that don't rely on state or side-effects[3](https://dev.to/sampriddy/works-as-shown-elixirs-doctest-macro-2gmj). If a function requires complex setup or generates side effects, it may not be suitable for a doctest.

When running tests with ExUnit, doctests are included in the test suite and reported separately from other tests[1](https://hexdocs.pm/elixir/1.12/writing-documentation.html)[5](http://elixir-lang.readthedocs.io/en/latest/mix_otp/9.html). They are a useful tool for testing and documenting code at the same time.

To generate documentation that includes doctests, you can use tools like ExDoc. ExDoc generates HTML documentation from your project's code and includes the doctests alongside the documentation[7](https://elixirschool.com/en/lessons/basics/documentation/). You can generate the documentation by running `mix docs` command[7](https://elixirschool.com/en/lessons/basics/documentation/). The generated documentation can be viewed in a browser and can be deployed to various platforms like GitHub or HexDocs[7](https://elixirschool.com/en/lessons/basics/documentation/).

In summary, doctests in Elixir are a way to include examples in module documentation and automatically test them. They help ensure that the examples in your documentation stay accurate and serve as both documentation and tests for your code. They are executed using the ExUnit framework and can be generated alongside your documentation using tools like ExDoc.