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
Phoenix will return waning if `.greet`is being using without pass tributes. In this case a default attribute should be set:
```rb
attr :messenger, :string, default: nil
```

## HEEx
HEEx, which stands for HTML+EEx, is a template language used in the [[Phoenix]] framework of the Elixir programming language. It is an extension of EEx (Embedded Elixir), which is a library for embedding Elixir code inside strings [1](https://hexdocs.pm/phoenix/components.html)[2](https://studioindie.co/blog/heex-guide/). It uses `<%= expression %>` to execute Elixir expressions. The `=` means the expression output something to template, but the without ones, just execute.

Example:
In a controller we can invoke: `render(conn, :show, username: "joe")`.
Then we can access the username in the template:
```html
<%= if some_condition? do %>
  <p>Some condition is true for user: <%= @username %></p>
<% else %>
  <p>Some condition is false for user: <%= @username %></p>
<% end %>
```
In the above example we have a `if` and `else` condition example and we can also use loops:
```html
<table>
  <tr>
    <th>Number</th>
    <th>Power</th>
  </tr>
  <%= for number <- 1..10 do %>
    <tr>
      <td><%= number %></td>
      <td><%= number * number %></td>
    </tr>
  <% end %>
</table>
```

### HTML extensions
To use an HTML in HEEx, the `raw` should be used. Without it the HTML tags would be considered plain text.
```html
<%= raw "<b>Bold?</b>" %>
```
HEEx also supports shorthand syntax for `if` and `for` expressions via the special `:if` and `:for` attributes. For example, rather than this:
```html
<%= if @some_condition do %>
  <div>...</div>
<% end %>
```
You can write:
```html
<div :if={@some_condition}>...</div>
```
Likewise, for comprehensions may be written as:
```html
<ul>
  <li :for={item <- @items}><%= item.name %></li>
</ul>
```

### Layouts
Layouts are just function components. They are defined in a module, just like all other function component templates.

To disable layout:
```rb
def index(conn, _params) do
  conn
  |> put_root_layout(html: false)
  |> render(:index)
end
```
To use specific one(file `admin.html.heex` in the same directory `lib/hello_web/components/layouts`):
```rb
def index(conn, _params) do
  conn
  |> put_layout(html: :admin)
  |> render(:index)
end
```