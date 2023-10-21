Is the core of the [[Phoenix]] [[HTTP]] layer. We interact with plugs at every step of the request life-cycle, and the core Phoenix components like endpoints, routers, and controllers are all just plugs internally.

## Functions plug
To implement a function plug we need:
1. It receives a connection and options (that we do not use)
2. It prints some connection information to the terminal
3. It returns the connection

Example:
```rb
def introspect(conn, _opts) do
  IO.puts """
  Verb: #{inspect(conn.method)}
  Host: #{inspect(conn.host)}
  Headers: #{inspect(conn.req_headers)}
  """

  conn
end
```
To learn about all fields available in the connection and all of the functionality associated to it, see the [documentation for `Plug.Conn`](https://hexdocs.pm/plug/Plug.Conn.html).
##  Module plugs
Module plugs are another type of plug that let us define a connection transformation in a module. The module only needs to implement two functions:
- [`init/1`](https://hexdocs.pm/plug/1.14.2/Plug.html#c:init/1) which initializes any arguments or options to be passed to [`call/2`](https://hexdocs.pm/plug/1.14.2/Plug.html#c:call/2)
- [`call/2`](https://hexdocs.pm/plug/1.14.2/Plug.html#c:call/2) which carries out the connection transformation. [`call/2`](https://hexdocs.pm/plug/1.14.2/Plug.html#c:call/2) is just a function plug that we saw earlier
```rb
defmodule HelloWeb.Plugs.Locale do
  import Plug.Conn

  @locales ["en", "fr", "de"]

  def init(default), do: default

  def call(%Plug.Conn{params: %{"locale" => loc}} = conn, _default) when loc in @locales do
    assign(conn, :locale, loc)
  end

  def call(conn, default) do
    assign(conn, :locale, default)
  end
end
```

```rb
defmodule HelloWeb.Router do
  use HelloWeb, :router

  pipeline :browser do
    plug :accepts, ["html"]
    plug :fetch_session
    plug :fetch_flash
    plug :protect_from_forgery
    plug :put_secure_browser_headers
    plug HelloWeb.Plugs.Locale, "en"
  end
  ...nd
end
```

## Where to plug

The endpoint, router, and controllers in Phoenix accept plugs.

##### Endpoint
Above, at the [[Plug#Functions plug]], we saw an example in endpoint. The default endpoint plugs do quite a lot of work. Here they are in order:

- [`Plug.Static`](https://hexdocs.pm/plug/1.14.2/Plug.Static.html) - serves static assets. Since this plug comes before the logger, requests for static assets are not logged.
- `Phoenix.LiveDashboard.RequestLogger` - sets up the _Request Logger_ for Phoenix LiveDashboard, this will allow you to have the option to either pass a query parameter to stream requests logs or to enable/disable a cookie that streams requests logs from your dashboard.
- [`Plug.RequestId`](https://hexdocs.pm/plug/1.14.2/Plug.RequestId.html) - generates a unique request ID for each request. 
- [`Plug.Telemetry`](https://hexdocs.pm/plug/1.14.2/Plug.Telemetry.html) - adds instrumentation points so Phoenix can log the request path, status code and request time by default.
- [`Plug.Parsers`](https://hexdocs.pm/plug/1.14.2/Plug.Parsers.html) - parses the request body when a known parser is available. By default, this plug can handle URL-encoded, multipart and JSON content (with [`Jason`](https://hexdocs.pm/jason/1.4.0/Jason.html)). The request body is left untouched if the request content-type cannot be parsed.
- [`Plug.MethodOverride`](https://hexdocs.pm/plug/1.14.2/Plug.MethodOverride.html) - converts the request method to PUT, PATCH or DELETE for POST requests with a valid `_method` parameter.
- [`Plug.Head`](https://hexdocs.pm/plug/1.14.2/Plug.Head.html) - converts HEAD requests to GET requests and strips the response body.
- [`Plug.Session`](https://hexdocs.pm/plug/1.14.2/Plug.Session.html) - a plug that sets up session management. Note that `fetch_session/2` must still be explicitly called before using the session, as this plug just sets up how the session is fetched.

##### Routers
As we saw in [[Plug#Module plugs]] we can declare plugs inside pipelines.
For example, accessing "/" will pipe through the `:browser` pipeline, consequently invoking all of its plugs.
As we will see in the [routing guide](https://hexdocs.pm/phoenix/routing.html), the pipelines themselves are plugs. There, we will also discuss all plugs in the `:browser` pipeline.
##### Controller
Finally, controllers are plugs too, so we can do:
```rb
defmodule HelloWeb.PageController do
  use HelloWeb, :controller

  plug HelloWeb.Plugs.Locale, "en"
```
In particular, controller plugs provide a feature that allows us to execute plugs only within certain actions. For example, you can do:
```rb
defmodule HelloWeb.PageController do
  use HelloWeb, :controller

  plug HelloWeb.Plugs.Locale, "en" when action in [:index]
```
And the plug will only be executed for the `index` action.

### Plugs as composition
Here are an example of how Plug can help use to have a [[Clean Code]]:

```rb
defmodule HelloWeb.MessageController do
  use HelloWeb, :controller

  def show(conn, params) do
    case Authenticator.find_user(conn) do
      {:ok, user} ->
        case find_message(params["id"]) do
          nil ->
            conn |> put_flash(:info, "That message wasn't found") |> redirect(to: ~p"/")
          message ->
            if Authorizer.can_access?(user, message) do
              render(conn, :show, page: message)
            else
              conn |> put_flash(:info, "You can't access that page") |> redirect(to: ~p"/")
            end
        end
      :error ->
        conn |> put_flash(:info, "You must be logged in") |> redirect(to: ~p"/")
    end
  end
end
```
Notice how just a few steps of authentication and authorization require complicated nesting and duplication? Let's improve this with a couple of plugs.
```rb
defmodule HelloWeb.MessageController do
  use HelloWeb, :controller

  plug :authenticate
  plug :fetch_message
  plug :authorize_message

  def show(conn, params) do
    render(conn, :show, page: conn.assigns[:message])
  end

  defp authenticate(conn, _) do
    case Authenticator.find_user(conn) do
      {:ok, user} ->
        assign(conn, :user, user)
      :error ->
        conn |> put_flash(:info, "You must be logged in") |> redirect(to: ~p"/") |> halt()
    end
  end

  defp fetch_message(conn, _) do
    case find_message(conn.params["id"]) do
      nil ->
        conn |> put_flash(:info, "That message wasn't found") |> redirect(to: ~p"/") |> halt()
      message ->
        assign(conn, :message, message)
    end
  end

  defp authorize_message(conn, _) do
    if Authorizer.can_access?(conn.assigns[:user], conn.assigns[:message]) do
      conn
    else
      conn |> put_flash(:info, "You can't access that page") |> redirect(to: ~p"/") |> halt()
    end
  end
end
```
