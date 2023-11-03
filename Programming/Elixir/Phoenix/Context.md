Are dedicated modules to organize related functionality, providing a better application design. In [[Phoenix]], contexts often encapsulate data access and data validation. They often talk to a database or APIs.

Phoenix includes the [`mix phx.gen.html`](https://hexdocs.pm/phoenix/Mix.Tasks.Phx.Gen.Html.html), [`mix phx.gen.json`](https://hexdocs.pm/phoenix/Mix.Tasks.Phx.Gen.Json.html), [`mix phx.gen.live`](https://hexdocs.pm/phoenix/Mix.Tasks.Phx.Gen.Live.html), and [`mix phx.gen.context`](https://hexdocs.pm/phoenix/Mix.Tasks.Phx.Gen.Context.html) generators that apply the ideas of isolating functionality in our applications into contexts. 
For example, [`mix phx.gen.html`](https://hexdocs.pm/phoenix/Mix.Tasks.Phx.Gen.Html.html) creates a context module that wraps up [[Ecto]] access for creating, updating, and deleting products, along with web files like controllers and templates for the web interface into our context. Or [`mix phx.gen.context`](https://hexdocs.pm/phoenix/Mix.Tasks.Phx.Gen.Context.html), which is just like [`mix phx.gen.html`](https://hexdocs.pm/phoenix/Mix.Tasks.Phx.Gen.Html.html), except it doesn't generate the web files for us.

#### Example
Generating a context:
```
$mix phx.gen.context Catalog Category categories title:string:unique

You are generating into an existing context.
...
Would you like to proceed? [Yn] y
* creating lib/hello/catalog/category.ex
* creating priv/repo/migrations/20210203192325_create_categories.exs
* injecting lib/hello/catalog.ex
* injecting test/hello/catalog_test.exs
* injecting test/support/fixtures/catalog_fixtures.ex
```

Creating a custom table revelation migration:
- Generate the migration:
```
mix ecto.gen.migration create_product_categories

* creating priv/repo/migrations/20210203192958_create_product_categories.exs
```

- Writing the migration relation table code:
```rb
defmodule Hello.Repo.Migrations.CreateProductCategories do
  use Ecto.Migration

  def change do
    create table(:product_categories, primary_key: false) do
      add :product_id, references(:products, on_delete: :delete_all)
      add :category_id, references(:categories, on_delete: :delete_all)
    end

    create index(:product_categories, [:product_id])
    create unique_index(:product_categories, [:category_id, :product_id])
  end
end
```

- Finally migrate the database: `mix ecto.migrate`.

We also can seeds a table with a initial data:
- In the file `priv/repo/seeds.exs` write something like:
```rb
for title <- ["Home Improvement", "Power Tools", "Gardening", "Books", "Education"] do
  {:ok, _} = Hello.Catalog.create_category(%{title: title})
end
```
And run `mix run priv/repo/seeds.exs` to run this script.

Our context know how to associate products and categories. We need to add the following association at the schema:
```rb
+ alias Hello.Catalog.Category

  schema "products" do
    field :description, :string
    field :price, :decimal
    field :title, :string
    field :views, :integer

+   many_to_many :categories, Category, join_through: "product_categories", on_replace: :delete

    timestamps()
  end
```

## Cross-context dependencies
