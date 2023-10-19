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