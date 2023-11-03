Here are presenting approaches to build Web APIs using [[Phoenix]].

## CRUD

Create files using generators to scaffold:
```
mix phx.gen.json Urls Url urls link:string title:string
```

- Files in `lib/hello_web` responsible for effectively rendering JSON
- Files in `lib/hello` responsible for defining our context and logic to persist links to the database
- Files in `priv/repo/migrations` responsible for updating our database
- Files in `test` to test our controllers and contexts

Then, upgrading the database with `mix ecto.migrate`, and running the application with `mix phx.server`, the CRUD actions will be available:

#### CREATE
```
curl -iX POST http://localhost:4000/api/urls \
   -H 'Content-Type: application/json' \
   -d '{"url": {"link":"https://phoenixframework.org", "title":"Phoenix Framework"}}'

curl -iX POST http://localhost:4000/api/urls \
   -H 'Content-Type: application/json' \
   -d '{"url": {"link":"https://elixir-lang.org", "title":"Elixir"}}'
```
### READ
We can retrieve all links:
```
curl -i http://localhost:4000/api/urls
```

Or we can just retrieve a link by its `id`:
```
curl -i http://localhost:4000/api/urls/1
```
### UPDATE
```
curl -iX PUT http://localhost:4000/api/urls/2 \
   -H 'Content-Type: application/json' \
   -d '{"url": {"title":"Elixir Programming Language"}}'
```
### DELETE
```
curl -iX DELETE http://localhost:4000/api/urls/2 \
   -H 'Content-Type: application/json'
```

## API-only applications
In case you want to generate a Phoenix application exclusively for APIs, you can pass several options when invoking [`mix phx.new`](https://hexdocs.pm/phoenix/Mix.Tasks.Phx.New.html). Let's check which `--no-*` flags we need to use to not generate the scaffolding that isn't necessary on our Phoenix application for the REST API.

From your terminal run:

```
mix help phx.new
```