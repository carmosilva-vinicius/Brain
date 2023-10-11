## If, unless and else
In [[Elixir]] they work much the same way but they are defined as macros, not language constructs. You can find their implementation in the [Kernel module](https://hexdocs.pm/elixir/Kernel.html).
```rb
defmodule MeuModulo.Enum do
  def primeiro(lista) do
    if length(lista) == 0 do
      nil
    else
      hd(lista)
    end
  end
end
```

The above function has the same effect of bellow one:
```rb
defmodule MeuModulo.Enum do
  def primeiro(lista) do
    unless length(lista) == 0 do
      hd(lista)
    end
  end
end
```

Another options is to implement another definitions to the same function. That is similar to **_overloading_**, but it uses [[Programming/Elixir/Pattern matching]], to decide which function will be executed.  So, we can use it to make conditions:
```rb
defmodule MeuModulo.Enum do
  def primeiro([]), do: nil
  def primeiro(lista), do: hd(lista)
end
```
## Case
If it’s necessary to match against multiple patterns we can use `case/2`:
```rb
defmodule MeuModulo.Calendario do
  def abreviacao_dia_semana(dia_semana) do
    case dia_semana do
      :Segunda -> "Seg"
      :Terca -> "Ter"
      :Quarta -> "Qua"
      :Quinta -> "Qui"
      :Sexta -> "Sex"
      :Sabado -> "Sab"
      :Domingo -> "Dom"
      _ -> "Dia invalido"
    end  
  end
end
```
## Cond
Is a kind of syntax sugar for if else:
```rb
defmodule MeuModulo.Calendario do
  def abreviacao_dia_semana(dia_semana) do
    case dia_semana do
      :Segunda -> "Seg"
      :Terca -> "Ter"
      :Quarta -> "Qua"
      :Quinta -> "Qui"
      :Sexta -> "Sex"
      :Sabado -> "Sab"
      :Domingo -> "Dom"
      _ -> "Dia invalido"
    end  
  end
end
```

Finally we  also can use pattern matching to it:
```rb
def abreviacao_dia_semana3(:Segunda), do: "Seg"
def abreviacao_dia_semana3(:Terca), do: "Ter"
def abreviacao_dia_semana3(:Quarta), do: "Qua"
def abreviacao_dia_semana3(:Quinta), do: "Qui"
def abreviacao_dia_semana3(:Sexta), do: "Sex"
def abreviacao_dia_semana3(:Sabado), do: "Sab"
def abreviacao_dia_semana3(:Domingo), do: "Dom"
def abreviacao_dia_semana3(_), do: "Dia invalido"
```
