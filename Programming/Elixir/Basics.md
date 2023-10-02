Here are the bases and elementary concepts about syntax, functional paradigm and pattern matching of [[Elixir]] language.
### Variáveis

definindo variável:

```rb
variavel = 2

#Divisão:

#retorna 1.0
variavel/2

#retorn 1 (inteiro)
div variavel, 2 #ou div(variavel,2)

```

Printando variaveis

```rb
IO.puts("teste")
#retorna:
# teste
# :ok
```

### String

Devem sempre estar em aspas duplas, em aspas simples teremos uma lista de caracteres. Strings em Elixir já são armazenadas por padrão em UTF-8

```rb
byte_size("Vinícius")
#retorn 9

String.length("Vinícius")
#retorna 8
```

Concatenando ou interpolando em string:

```rb
nome =  "Vinícius"

"Bem-vindo " <> nome <> "."
#retorna Bem-vindo Vinícius.

"Bem-vindo #{nome}."
#retorna Bem-vindo Vinícius.

IO.puts("Bem-vindo\\n#{nome}.")
#retorna   Bem-vindo 
#          Vinícius.

```

### Listas

```rb
[1, "Dois", :tres, 4.0]
```

Operações com lista:

como se trata de uma lista ligada, adicionar ou encontrar itens no final da lista é uma trabalho muito custoso. No entanto, no início da lista é mais eficiente, uma vez que a operação não precisa percorrer toda a lista.

```rb
minha_lista = [1, 2, 3]

minha_lista ++ [4, 5, 6]
#retorna [1, 2, 3, 4, 5, 6]

[1, true, 2, false, 3, true] -- [true, false]
#retorna [1, 2, 3, true]
```

**Head and tail:**

```rb
list= [1, 2, 3]
hd(list)
# 1
tl(list)
# [2, 3]

#Usando o operador cons

[0 | list]
#[0, 1, 2, 3]

#Pattern matching

[zero | resto] = [0, 1, 2 ,3 ,4]
# [0, 1, 2 ,3 ,4]

zero
# 0

resto
# [1, 2 ,3 ,4] 
```

**Maps**

Mapas são estruturas de dados com chave e valor.

Em Elixir qualquer tipo de dado pode ser chave ou valor:

```rb
%{}
# %{}
%{"one" => :two, 3 => "four"}
# %{3 => "four", "one" => :two}
```

### Atoms

São variáveis, imutáveis, onde o valor armazenado é sempre o nome da variável. Em outras linguagens podem ser conhecidas com símbolos. São geralmente utilizados para enumerar entre valores distintos.

```rb
iex> :apple
:apple
iex> :orange
:orange
iex> :watermelon
:watermelon

iex> :apple == :apple
true
iex> :apple == :orange
false

:"isso é um atomo"
IO.puts(:"isso é um atomo")
# retorna: isso é um atomo
```

**Booleans** in **Elixir** are aways **atoms**:

```rb
iex> true == :true
true
iex> is_atom(false)
true
iex> is_boolean(:false)
true
```

### Keyword lists

Juntando o conceito de tuplas (um conjunto de dados relacionados) com atoms, temos as keyword lists. Esse tipo de dados é muito parecido com mapas.

```rb
keyword_list = [{:um, 1}, {:dois, 2}, {:tres, 3}]

keykeyword_list[:um] # retorna 1
```

podemos simplificar a definição de keyword lists da seguinte forma:

```rb
keyword_list = [um: 1, dois: 2, tres: 3]
```

## Tuplas

Valores em Tuplas são armazenados sequencialmente na memória, da mesma forma como temos vetores em outras linguagens. Sendo assim, acessar algum dos elementos no meio da tupla é uma operação rápida. Agora adicionar valores na tupla é um processo mais custoso, já que precisamos criar uma nova tupla para isso. Neste ponto as listas são mais rápidas. Para saber quando usar cada tipo: [Lists or tuples?](https://elixir-lang.org/getting-started/basic-types.html#lists-or-tuples)

```rb
primeira_tupla = {"um", 1, 1.0, "I"}

elem(primeria_tupla, 0) # retorna "um"
elem(primeria_tupla, 2) # retorna 1.0

{:ok, "Conteúdo do arquivo"}
vinicius = {"Vinincius Henrique", 27}
```

## Imutabilidade

Característica fundamental geralmente encontrada em linguagens de paradigma funcional.

O valor de uma variável nunca é alterado no endereço de memória, ao contrario disso, um novo endereço assume o novo valor. Com isso uma thread não corre o risco de ter uma variável alterada por outra thread.

## Loops with recursion
Elixir don't have loops, to do it we need to use recursion. In other words we need to calla function inside itself and implement a way to break this loop. Pattern matching helps in this cases:
```rb
defmodule MeuModulo.Loop do
  defp tabuada(_, 11), do: nil

  def tabuada(multiplicador) do
    tabuada(multiplicador, 1)
  end

  defp tabuada(produto1, produto2) do
    IO.puts "#{produto1} x #{produto2} = #{produto1 * produto2}"
    tabuada(produto1, produto2 + 1)
  end
end
```

## Working with files
The function read of the File module return a tuple with the `:error` or `:ok` with the content.
Here is an example of how to capture the error.
```rb
defmodule MeuModulo.Arquivos do
	def ler(arquivo) do
		{:error, erro} = File.read(arquivo)
		erro
	end
end
```

```rb
#arquivo inexistente
iex(1)> MeuModulo.Arquivos.ler("teste")
:enoent

#arquivo sem permissão
iex(2)> MeuModulo.Arquivos.ler("arquivo")
:eacces
```

We also can return just the content string and throw an exception in case of some error:
```rb
defmodule MeuModulo.Arquivos do
	def ler(arquivo) do
		File.read!(arquivo)
	end
end
```
A more complete example:
```rb
defmodule MeuModulo.Arquivos do
	def ler(arquivo) do
		case File.read(arquivo) do
			{:ok, conteudo} -> conteudo
			{:error, :enoent} -> "Arquivo inexistente"
			{:error, :eacces} -> "Sem permissão de leitura"
			_ -> "Erro desconhecido"
		end
	end
end
```