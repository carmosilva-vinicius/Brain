Example of testing with mock data with [[ExUnit]] and  [[Erlang#ets|ets]]:
```rb
test "com mock" do
	:ets.new(:conteudos, [:set, :private, :named_table])
	with_mock File, [write!: fn (_path, conteudo) -> :ets.insert_new(:conteudos, {conteudo}) end] do
		ElixirTest.EscreveNumeroAleatorio.escreve
		ElixirTest.EscreveNumeroAleatorio.escreve
	end
	conteudos = :ets.tab2list(:conteudos)
	[primeiro_valor | conteudos] = conteudos
	[segundo_valor | _] = conteudos
	assert primeiro_valor != segundo_valor
end
```