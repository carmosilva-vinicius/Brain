Phoenix is a web development framework written in [[Elixir]] which implements the server-side Model View Controller (MVC) pattern. 

## Getting start
Creating a Phoenix project with [[Mix]]:
```zsh
$ mix phx.new hello
```
We are almost there! The following steps are missing: 
```zsh
$ cd hello
```
Then configure your database in config/dev.exs and run: 
```zsh
$ mix ecto.create 
```
Start your Phoenix app with: 
```zsh
$ mix phx.server 
```
You can also run your app inside IEx (Interactive Elixir) as: 
```zsh
$ iex -S mix phx.server
```

## Directory Structure
When we use [`mix phx.new`](https://hexdocs.pm/phoenix/Mix.Tasks.Phx.New.html) to generate a new Phoenix application, it builds a top-level directory structure like this:
```
├── _build
├── assets
├── config
├── deps
├── lib
│   ├── hello
│   ├── hello.ex
│   ├── hello_web
│   └── hello_web.ex
├── priv
└── test
```

We will go over those directories one by one:

- `_build` - holds all compilation artifacts. This directory must not be checked into version control and it can be removed at any time. Removing it will force Mix to rebuild your application from scratch. 
- `assets` - a directory that keeps source code for your front-end assets, like JavaScript and CSS. These sources are automatically bundled by the `esbuild` tool. Static files like images and fonts go in `priv/static`.
- `config` - holds your project configuration. The `config/config.exs` file is the entry point for your configuration, it imports environment specific configuration, which can be found in `config/dev.exs`, `config/test.exs`, and `config/prod.exs`. Finally, `config/runtime.exs` is executed and it is the best place to read secrets and other dynamic configuration.
- `deps` - a directory with all of our Mix dependencies. You can find all dependencies listed in the `mix.exs` file, inside the `defp deps do` function definition. This directory must not be checked into version control and it can be removed at any time. Removing it will force Mix to download all deps from scratch.
- `lib` - holds your application source code. This directory is broken into two subdirectories, `lib/hello` and `lib/hello_web`. The `lib/hello` hosts all of your business logic and business domain. It typically interacts directly with the database - it is the "Model" in Model-View-Controller (MVC) architecture. `lib/hello_web` is responsible for exposing your business domain to the world. It holds both the View and Controller from MVC.
- `priv` - keeps all resources that are necessary in production but are not directly part of your source code. You typically keep database scripts, translation files, images, and more in here. Generated assets, created from files in the `assets` directory, are placed in `priv/static/assets` by default.
- `test` - a directory with all of our application tests. It often mirrors the same structure found in `lib`.

Here we are telling `Phoenix.Component` to embed all `.heex` templates found in the sibling `hello_html` directory into our module as function definitions.
Next, we need to add files to the `lib/hello_web/controllers/hello_html` directory.
Note the controller name (`HelloController`), the view name (`HelloHTML`), and the template directory (`hello_html`) all follow the same naming convention and are named after each other. They are also collocated together in the directory tree:

```
lib/hello_web
├── controllers
│   ├── hello_controller.ex
│   ├── hello_html.ex
│   ├── hello_html
|       ├── index.html.heex
```

## Life-Cycle
Each layer serves a distinct purpose:
- endpoint ([`Phoenix.Endpoint`](https://hexdocs.pm/phoenix/Phoenix.Endpoint.html)) - the endpoint contains the common and initial path that all requests go through. If you want something to happen on all requests, it goes to the endpoint.  
- router ([`Phoenix.Router`](https://hexdocs.pm/phoenix/Phoenix.Router.html)) - the router is responsible for dispatching verb/path to controllers. The router also allows us to scope functionality. For example, some pages in your application may require user authentication, others may not.
- controller ([`Phoenix.Controller`](https://hexdocs.pm/phoenix/Phoenix.Controller.html)) - the job of the controller is to retrieve request information, talk to your business domain, and prepare data for the presentation layer. 
- view - the view handles the structured data from the controller and converts it to a presentation to be shown to users. Views are often named after the content format they are rendering.

## Exploring parameters and HEEx tags

You can extract the `messenger` parameter from the `conn` parameter and pass it to the template using the `render` function. Here's an example:
```rb
def show(conn, %{"messenger" => messenger}) do
  render(conn, :show, messenger: messenger)
end
```
you can also access the full map of parameters bound to the `params` variable by using the `= params` pattern match assertion. This can be useful if you need access to other parameters in addition to the `messenger` parameter. Here's an example:
```rb
def show(conn, %{"messenger" => messenger} = params) do
  # Access other parameters from `params` if needed
  ...
end
```

 Using the special HEEx tags for executing Elixir expressions: `<%= %>`. Notice that the initial tag has an equals sign like this: `<%=` . That means that any Elixir code that goes between those tags will be executed, and the resulting value will replace the tag in the HTML output. If the equals sign were missing, the code would still be executed, but the value would not appear on the page:
```html
<section>
  <h2>Hello World, from <%= @messenger %>!</h2>
</section>
```