HEEx, which stands for HTML+EEx, is a template language used in the [[Phoenix]] framework of the Elixir programming language. It is an extension of EEx (Embedded Elixir), which is a library for embedding Elixir code inside strings [1](https://hexdocs.pm/phoenix/components.html)[2](https://studioindie.co/blog/heex-guide/).

## Function component
A function component need a template which should be returned by and Elixir function. This is an example of template with correct path and extention: `lib/hello_web/controllers/hello_html/show.html.heex`
```html
<section>
  <h2>Hello World, from <%= @messenger %>!</h2>
</section>
```
This template, is embedded as part of module `HelloHTML`, at `lib/hello_web/controllers/hello_html.ex`:
```rb
defmodule HelloWeb.HelloHTML do
  use HelloWeb, :html

  embed_templates "hello_html/*"
end
```

Refactoring the above code, is also possible to render the html in a function inside the `HelloHTTML`:
```rb
defmodule HelloWeb.HelloHTML do
  use HelloWeb, :html

  embed_templates "hello_html/*"

  attr :messenger, :string

  def greet(assigns) do
    ~H"""
    <h2>Hello World, from <%= @messenger %>!</h2>
    """
  end
end
```
We declared the attributes we accept via `attr` provided by `Phoenix.Component`, then we defined our `greet/1` function which returns the HEEx template.

Next we need to update `show.html.heex`:
```html
<section>
  <.greet messenger={@messenger} />
</section>
```