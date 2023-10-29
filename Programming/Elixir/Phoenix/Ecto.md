Is the ORM provided by [[Phoenix]] Framework. Creating a new project PostgreSQL is set by default, but Ecto works with this options: 

- PostgreSQL (via [`postgrex`](https://github.com/elixir-ecto/postgrex))
- MySQL (via [`myxql`](https://github.com/elixir-ecto/myxql))
- MSSQL (via [`tds`](https://github.com/livehelpnow/tds))
- ETS (via [`etso`](https://github.com/evadne/etso))
- SQLite3 (via [`ecto_sqlite3`](https://github.com/elixir-sqlite/ecto_sqlite3))
- The `--no-ecto` flag to exclude this.

## Schemas and Migrations
Similar to models in OOP languages, the schemas specify how Elixir data types map to and from external sources, such as database tables.

Example of how to create a user example schema and migrate it to database:
```
mix phx.gen.schema User users name:string email:string \
bio:string number_of_pets:integer

* creating ./lib/hello/user.ex
* creating priv/repo/migrations/20170523151118_create_users.exs

Remember to update your repository by running migrations:

   $ mix ecto.migrate

```

## Changesets and validations
Is pipeline of transformations our data needs to be ready for our application to use. It might include type-casting, user input validation, and filtering out any extraneous parameters.

Example: 
```rb
def changeset(user, attrs) do
  user
  |> cast(attrs, [:name, :email, :bio, :number_of_pets])
  |> validate_required([:name, :email, :bio, :number_of_pets])
end
```
[`cast/3`](https://hexdocs.pm/ecto/3.10.1/Ecto.Changeset.html#cast/3) first takes a struct, then the parameters (the proposed updates), and then the final field is the list of columns to be updated. [`cast/3`](https://hexdocs.pm/ecto/3.10.1/Ecto.Changeset.html#cast/3) also will only take fields that exist in the schema. Next, [`Ecto.Changeset.validate_required/3`](https://hexdocs.pm/ecto/3.10.1/Ecto.Changeset.html#validate_required/3) checks that this list of fields is present in the changeset that [`cast/3`](https://hexdocs.pm/ecto/3.10.1/Ecto.Changeset.html#cast/3) returns. By default with the generator, all fields are required.

We can also make validations about the data values: 
```rb
def changeset(user, attrs) do
  user
  |> cast(attrs, [:name, :email, :bio, :number_of_pets])
  |> validate_required([:name, :email, :bio, :number_of_pets])
  |> validate_length(:bio, min: 2)
  |> validate_length(:bio, max: 140)
  |> validate_format(:email, ~r/@/)
end
```

## Queries
The `Repo` module's purpose is to take care of the finer details of persistence and data querying for us.

##### Inserting example:
```rb
iex> alias Hello.{Repo, User}
[Hello.Repo, Hello.User]

iex> Repo.insert(%User{email: "user1@example.com"})
[debug] QUERY OK db=6.5ms queue=0.5ms idle=1358.3ms
INSERT INTO "users" ("email","inserted_at","updated_at") VALUES ($1,$2,$3) RETURNING "id" ["user1@example.com", ~N[2021-02-25 01:58:55], ~N[2021-02-25 01:58:55]]
{:ok,
 %Hello.User{
   __meta__: #Ecto.Schema.Metadata<:loaded, "users">,
   bio: nil,
   email: "user1@example.com",
   id: 1,
   inserted_at: ~N[2021-02-25 01:58:55],
   name: nil,
   number_of_pets: nil,
   updated_at: ~N[2021-02-25 01:58:55]
 }}
```

##### Getting all example:
```rb
iex> Repo.all(User)
[debug] QUERY OK source="users" db=5.8ms queue=1.4ms idle=1672.0ms
SELECT u0."id", u0."bio", u0."email", u0."name", u0."number_of_pets", u0."inserted_at", u0."updated_at" FROM "users" AS u0 []
[
  %Hello.User{
    __meta__: #Ecto.Schema.Metadata<:loaded, "users">,
    bio: nil,
    email: "user1@example.com",
    id: 1,
    inserted_at: ~N[2021-02-25 01:58:55],
    name: nil,
    number_of_pets: nil,
    updated_at: ~N[2021-02-25 01:58:55]
  },
  %Hello.User{
    __meta__: #Ecto.Schema.Metadata<:loaded, "users">,
    bio: nil,
    email: "user2@example.com",
    id: 2,
    inserted_at: ~N[2021-02-25 02:03:28],
    name: nil,
    number_of_pets: nil,
    updated_at: ~N[2021-02-25 02:03:28]
  }
]
```

We can use `Ecto.Query` to make rich queries like:
```rb
iex> import Ecto.Query
Ecto.Query

# Selecting only email
iex> Repo.all(from u in User, select: u.email)
[debug] QUERY OK source="users" db=0.8ms queue=0.9ms idle=1634.0ms
SELECT u0."email" FROM "users" AS u0 []
["user1@example.com", "user2@example.com"]

# Counting emails that contains "1"
iex)> Repo.one(from u in User, where: ilike(u.email, "%1%"),
                               select: count(u.id))
[debug] QUERY OK source="users" db=1.6ms SELECT count(u0."id") FROM "users" AS u0 WHERE (u0."email" ILIKE '%1%') []
1

# Fetching a mak=p of  users
Repo.all(from u in User, select: %{u.id => u.email})
[debug] QUERY OK source="users" db=0.9ms
SELECT u0."id", u0."email" FROM "users" AS u0 []
[
  %{1 => "user1@example.com"},
  %{2 => "user2@example.com"}
]
```

