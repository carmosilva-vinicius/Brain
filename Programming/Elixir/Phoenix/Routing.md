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
- A GET request to `/users` will invoke the `index` action to show all the users.
- A GET request to `/users/:id/edit` will invoke the `edit` action with an ID to retrieve an individual user from the data store and present the information in a form for editing.
- A GET request to `/users/new` will invoke the `new` action to present a form for creating a new user.
- A GET request to `/users/:id` will invoke the `show` action with an id to show an individual user identified by that ID.
- A POST request to `/users` will invoke the `create` action to save a new user to the data store.
- A PATCH request to `/users/:id` will invoke the `update` action with an ID to save the updated user to the data store.
- A PUT request to `/users/:id` will also invoke the `update` action with an ID to save the updated user to the data store.
- A DELETE request to `/users/:id` will invoke the `delete` action with an ID to remove the individual user from the data store.
If we don't need all these routes, we can be selective using the `:only` and `:except` options to filter specific actions

IWe can be selective using the `:only` and `:except` options to filter specific actions:
```
resources "/posts", PostController, only: [:index, :show]
```

```
GET     /posts      HelloWeb.PostController :index
GET     /posts/:id  HelloWeb.PostController :show
```

Similarly, if we don't want to provide a route to delete one, we could define a route like this.
```
resources "/comments", CommentController, except: [:delete]
```

```
GET    /comments           HelloWeb.CommentController :index
GET    /comments/:id/edit  HelloWeb.CommentController :edit
GET    /comments/new       HelloWeb.CommentController :new
GET    /comments/:id       HelloWeb.CommentController :show
POST   /comments           HelloWeb.CommentController :create
PATCH  /comments/:id       HelloWeb.CommentController :update
PUT    /comments/:id       HelloWeb.CommentController :update
```

## Nested resources
It is also possible to nest resource that has a many-to-one relationship:
```rb
resources "/users", UserController do
  resources "/posts", PostController
end
```

```
...
GET     /users/:user_id/posts           HelloWeb.PostController :index
GET     /users/:user_id/posts/:id/edit  HelloWeb.PostController :edit
GET     /users/:user_id/posts/new       HelloWeb.PostController :new
GET     /users/:user_id/posts/:id       HelloWeb.PostController :show
POST    /users/:user_id/posts           HelloWeb.PostController :create
PATCH   /users/:user_id/posts/:id       HelloWeb.PostController :update
PUT     /users/:user_id/posts/:id       HelloWeb.PostController :update
DELETE  /users/:user_id/posts/:id       HelloWeb.PostController :delete
...
```

## Scoped routes
A way to group routes under a common path prefix and scoped set of plugs. We might want to do this for admin functionality, APIs, and especially for versioned APIs.
```rb
scope "/admin", HelloWeb.Admin do
  pipe_through :browser

  resources "/reviews", ReviewController
end
```
We define a new scope where all routes are prefixed with `/admin` and all controllers are under the `HelloWeb.Admin` namespace.
```
...
GET     /admin/reviews           HelloWeb.Admin.ReviewController :index
GET     /admin/reviews/:id/edit  HelloWeb.Admin.ReviewController :edit
GET     /admin/reviews/new       HelloWeb.Admin.ReviewController :new
GET     /admin/reviews/:id       HelloWeb.Admin.ReviewController :show
POST    /admin/reviews           HelloWeb.Admin.ReviewController :create
PATCH   /admin/reviews/:id       HelloWeb.Admin.ReviewController :update
PUT     /admin/reviews/:id       HelloWeb.Admin.ReviewController :update
DELETE  /admin/reviews/:id       HelloWeb.Admin.ReviewController :delete
...
```
## Forward
The [`Phoenix.Router.forward/4`](https://hexdocs.pm/phoenix/Phoenix.Router.html#forward/4) macro can be used to send all requests that start with a particular path to a particular plug. We can forward to this admin interface using:
```rb
defmodule HelloWeb.Router do
  use HelloWeb, :router

  ...

  scope "/" do
    pipe_through [:authenticate_user, :ensure_admin]
    forward "/jobs", BackgroundJob.Plug
  end
end
```