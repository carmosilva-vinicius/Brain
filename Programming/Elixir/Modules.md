[[Elixir]] modules provide a way to organize a group of functions in namespaces and allow to define private functions.

## Import
To have access and use [[Functions]] and [[Macros]] of a module, initially  we need to import the module:
```rb
import List
```

### Filtering
On the other hand, we can filter them using the `:only` and `:except` options.

To import specific functions and macros, we must provide the name/arity pairs to `:only` and `:except`. Examples:
```rb
#import just last/1
import List, only: [last: 1]

#import all List but last/1
import List, except: [last: 1]
```

### Alias
is a keyword used to create an alias for a module. This is useful when you want to refer to a module by a different name, or when you want to avoid naming conflicts.

For example, in the code you provided, `alias MeuModulo.Math, as: MyMath` creates an alias `MyMath` for the `MeuModulo.Math` module. This allows you to refer to `MeuModulo.Math` as `MyMath` throughout the rest of the module.

### require
We could use `require` to tell Elixir you’re going to use macros from another module. The slight difference with `import` is that it allows using macros, but not functions from the specified module:

```rb
defmodule Example do
  require SuperMacros

  SuperMacros.do_stuff
end
```

## Running example
We can load a module in the interactive shell (**IEx**) in terminal: `iex teste.exs`. Then we can run the functions of this module inside the IEX. If anything were changed in the module, it can be reloaded with `r(MeuModulo)` command in the interactive shell.
If our module depends of a module of another file, we can include it using `import_file math.exs`
#### Example
Below we have the creation of the `inspect` function, however, this is the name of a standard function loaded in the IO and `Kernel` modules. So in `import` of `IO` we select only the `puts` function, while in `Kernel` we import everything except the `inspect` function.
```rb
defmodule MeuModulo do
  import IO, only: [puts: 1]
  import Kernel, except: [inspect: 1]

  alias MeuModulo.Math, as: MyMath

  def ola_mundo() do
    inspect(MyMath.soma(2, 2))
  end

  def exibe_se_for_par(numero) do
    require Integer
    puts("O número #{numero} é par? #{Integer.is_even(numero)}")
  end

  def inspect(parametro) do
    puts("Começando a inspeção")
    puts(parametro)
    puts("Terminando a inspeção")
  end
end
```

In the above example use import filtering functions of module, alias to call a modulo with a custom name and require to use just macros of module. 
Modules has lexical scope, so this will works just inside the scope where is was imported. For example, the Integer macros are available to use just inside the  `exibe_se_for_par(numero)` function.