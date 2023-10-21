 They match HTTP requests to controller actions, wire up real-time channel handlers, and define a series of pipeline transformations scoped to a set of routes. Both the router and controller module names will be prefixed with the name you gave your application suffixed with `Web`. It looks like:
```rb
defmodule HelloWeb.Router do
  use HelloWeb, :router

  pipeline :browser do
    plug :accepts, ["html"]
    plug :fetch_session
    plug :fetch_live_flash
    plug :put_root_layout, html: {HelloWeb.Layouts, :root}
    plug :protect_from_forgery
    plug :put_secure_browser_headers
  end

  pipeline :api do
    plug :accepts, ["json"]
  end

  scope "/", HelloWeb do
    pipe_through :browser

    get "/", PageController, :home
  end

  # Other scopes may use custom stacks.
  # scope "/api", HelloWeb do
  #   pipe_through :api
  # end
  # ...
end
```

Inside the scope block, however, we have our first actual route:
```rb
get "/", PageController, :home
```
`get` is a Phoenix macro that corresponds to the HTTP verb GET. Similar macros exist for other HTTP verbs, including POST, PUT, PATCH, DELETE, OPTIONS, CONNECT, TRACE, and HEAD.

We can use [[Phoenix]] tool for investigating routes in an application: [`mix phx.routes`](https://hexdocs.pm/phoenix/Mix.Tasks.Phx.Routes.html).
```zsh
$ mix phx.routes
GET  /  HelloWeb.PageController :home
...
```

## Resources
As mentioned all HTTP verbs can be user. On the other hand Phoenix has the `resources` macro, which provide a group of common routes with some verbs:
```rb
scope "/", HelloWeb do
  pipe_through :browser

  get "/", PageController, :home
  resources "/users", UserController
  ...
end
```
Run [`mix phx.routes`](https://hexdocs.pm/phoenix/Mix.Tasks.Phx.Routes.html) once again at the root of your project. You should see something like the following:
```zsh
...
GET     /users           HelloWeb.UserController :index
GET     /users/:id/edit  HelloWeb.UserController :edit
GET     /users/new       HelloWeb.UserController :new
GET     /users/:id       HelloWeb.UserController :show
POST    /users           HelloWeb.UserController :create
PATCH   /users/:id       HelloWeb.UserController :update
PUT     /users/:id       HelloWeb.UserController :update
DELETE  /users/:id       HelloWeb.UserController :delete
...
```