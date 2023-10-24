[[Phoenix]] controllers serve as a bridge between incoming HTTP requests and the view layer of the application. They consist of functions, referred to as actions, that are triggered in response to specific HTTP requests routed from the Phoenix router. These actions are responsible for gathering necessary data, performing required operations, and then invoking the view layer to render a template or returning a JSON response [hexdocs.pm](https://hexdocs.pm/phoenix/controllers.html).

## Actions
In Elixir's Phoenix framework, controller actions are simply functions that we can name freely, provided they adhere to Elixir's naming conventions. The crucial requirement is that the action name corresponds to a route defined in the router. For example, in a new Phoenix app, the default route action `home` in `PageController` can be changed to `index`, as long as we also change the action name in `PageController` to `index` [hexdocs.pm](https://hexdocs.pm/phoenix/Phoenix.Controller.html).

```rb
get "/", PageController, :index

defmodule HelloWeb.PageController do
  ...

  def index(conn, _params) do
    render(conn, :index)
  end
end
```

While action names can be freely chosen, there are conventions to follow for better readability and understanding of the code. These include:
- index - renders a list of all items of the given resource type
- show - renders an individual item by ID
- new - renders a form for creating a new item
- create - receives parameters for one new item and saves it in a data store
- edit - retrieves an individual item by ID and displays it in a form for editing
- update - receives parameters for one edited item and saves the item to a data store
- delete - receives an ID for an item to be deleted and deletes it from a data store

## Rendering
Phoenix Framework provides several ways for controllers to render content:

1. **Rendering Plain Text**: The simplest way to render content is to render some plain text using the `text/2` function provided by Phoenix. For example:
```rb
def show(conn, %{"messenger" => messenger}) do
	text(conn, "From messenger #{messenger}")
end
```
When you visit `/hello/Frank` in your browser, it should display `From messenger Frank` as plain text without any HTML [hexdocs.pm](https://hexdocs.pm/phoenix/Phoenix.Controller.html).

2. **Rendering JSON**: Phoenix also provides the `json/2` function for rendering pure JSON. The function takes something that the Jason library can decode into JSON, such as a map. Jason is one of Phoenix's dependencies. Here's an example:
```rb
def show(conn, %{"messenger" => messenger}) do
  json(conn, %{id: messenger})
end
```
If you visit `/hello/Frank` in your browser, you should see a block of JSON with the key `id` mapped to the string "Frank" [hexdocs.pm](https://hexdocs.pm/phoenix/Phoenix.Controller.html).

3. **Rendering HTML and Views**: For rendering HTML, Phoenix provides the `html/2` function. However, most of the time, Phoenix views are used to build responses. Phoenix includes the `render/3` function, which is especially important for HTML responses, as Phoenix Views provide performance and security benefits [hexdocs.pm](https://hexdocs.pm/phoenix/Phoenix.Controller.html).
If we need to pass values into the template when using `render`, that's easy. We can pass a keyword like we've seen with `messenger: messenger`, or we can use [`Plug.Conn.assign/3`](https://hexdocs.pm/plug/1.14.2/Plug.Conn.html#assign/3), which conveniently returns `conn`.
```rb
def show(conn, %{"messenger" => messenger}) do
	conn
	|> Plug.Conn.assign(:messenger, messenger)
	|> render(:show)
end
```
Note: Using [`Phoenix.Controller`](https://hexdocs.pm/phoenix/Phoenix.Controller.html) imports [`Plug.Conn`](https://hexdocs.pm/plug/1.14.2/Plug.Conn.html), so shortening the call to [`assign/3`](https://hexdocs.pm/plug/1.14.2/Plug.Conn.html#assign/3) works just fine.
Passing more than one value to our template is as simple as connecting [`assign/3`](https://hexdocs.pm/plug/1.14.2/Plug.Conn.html#assign/3) functions together:
```rb
def show(conn, %{"messenger" => messenger}) do
    conn
    |> assign(:messenger, messenger)
    |> assign(:receiver, "Dweezil")
    |> render(:show)
end
```
Or you can pass the assigns directly to `render` instead:
```rb
def show(conn, %{"messenger" => messenger}) do
    render(conn, :show, messenger: messenger, receiver: "Dweezil")
end
```

## Sending response directly
In Elixir, you can send HTTP responses directly using the `Plug.Conn.send_resp/3` function. This function takes three arguments: the connection, the status code, and the body of the response. Here's an example of sending a 201 status code with no body:
```rb
def home(conn, _params) do
  send_resp(conn, 201, "")
end
```
Additionally, if you want to be specific about the content type of the response, you can use the `put_resp_content_type/2` function in conjunction with `send_resp/3`. Here's how you can set the content type to "text/plain":
```rb
def home(conn, _params) do
  conn
  |> put_resp_content_type("text/plain")
  |> send_resp(201, "")
end
```
## Setting the content type
If we wanted to render an XML version of our `home` action, we might implement the action like this in `lib/hello_web/page_controller.ex`.
```rb
def home(conn, _params) do
  conn
  |> put_resp_content_type("text/xml")
  |> render(:home, content: some_xml_content)
end
```

## Setting HTTP status
[`Plug.Conn.put_status/2`](https://hexdocs.pm/plug/1.14.2/Plug.Conn.html#put_status/2) takes `conn` as the first parameter and as the second parameter either an integer or a "friendly name" used as an atom for the status code we want to set. The list of status code atom representations can be found in [`Plug.Conn.Status.code/1`](https://hexdocs.pm/plug/1.14.2/Plug.Conn.Status.html#code/1) documentation:
```rb
def home(conn, _params) do
  conn
  |> put_status(202)
  |> render(:home, layout: false)
end
```

## Redirection
Phoenix controllers provide the handy [`redirect/2`](https://hexdocs.pm/phoenix/Phoenix.Controller.html#redirect/2) function to make redirections:
```rb
defmodule HelloWeb.PageController do
  use HelloWeb, :controller

  def home(conn, _params) do
    redirect(conn, to: ~p"/redirect_test")
  end
end
```

## Flash messages
Flash messages in Phoenix are a way to communicate with users during the course of an action. They are set using the `put_flash/3` function provided by the `Phoenix.Controller` module. This function sets flash messages as a key-value pair and places them into a `@flash` assign in the connection:
```rb
defmodule HelloWeb.PageController do
  ...
  def home(conn, _params) do
    conn
    |> put_flash(:error, "Let's pretend we have an error.")
    |> render(:home, layout: false)
  end
end
```
To display these flash messages, you can use the `Phoenix.Flash.get/2` function to retrieve them. This function takes the flash data and the key we care about, then returns the value for that key.
For example, to display flash messages in a template layout, you can use a flash_group component like this:
```html
<.flash_group flash={@flash} />
```
The flash functionality can also be used with redirects. For instance, if you want to redirect to a page with some extra information, you can do:
```rb
def home(conn, _params) do
  conn
  |> put_flash(:error, "Let's pretend we have an error.")
  |> redirect(to: ~p"/redirect_test")
end
```