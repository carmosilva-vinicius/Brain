Is a build tool that provides tasks for creating, compiling, and testing [[Elixir]] projects, managing its dependencies, and more. 

### New project
This will generate our project’s folder structure and necessary boilerplate. This is pretty straightforward, so let’s get started:

```
mix new example
```

### IEx
We can start the interactive shell with a mix project content.
```
iex -S mix
```
#### Observer
To start the observer in a mix project opened with IEx, you probably will need to ensure some services is running:
```rb
iex> Mix.ensure_application!(:wx)
iex> Mix.ensure_application!(:runtime_tools)
iex> Mix.ensure_application!(:observer)
iex> :observer.start()
```


## Tasks
We can run a module that can  be run directly in the mix [[CLI]]. To do that, we should to write a module that start with `MixTasks` and implement the `run()` function. The name of the module will be used to call the task, for the example bellow we would call using `mix escreve`
```rb
defmodule Mix.Tasks.Escreve do
	def run(_) do
		ElixirTest.EscreveNumeroAleatorio.escreve
	end
end
```

#### Documenting 
We can call it `mix help` to see the `@shortdoc`, or `mix help escreve` to see the `@moduledoc`
```rb
defmodule Mix.Tasks.Escreve do
	@moduledoc """
	Escreve um número aleatório em um arquivo.
	`mix escreve`
	"""
	use Mix.Task

	@shortdoc "Escreve um número aleatório no arquivo.txt"
	def run(_) do
		ElixirTest.EscreveNumeroAleatorio.escreve
	end
end
```
