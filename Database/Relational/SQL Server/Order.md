## Order By
is used to sort the result set in either ascending or descending order based on one or more columns. It is typically used in conjunction with the SELECT statement to control the order in which the rows are returned.
```sql
-- Exemplo 1: Ordenação ascendente por data
SELECT * FROM CLIENTES ORDER BY DATA_COMP;

-- Exemplo 2: Seleção na ordem natural da tabela
SELECT * FROM TABELA_DE_PRODUTOS;

-- Exemplo 3: Ordenação ascendente por preço de lista
SELECT * FROM TABELA_DE_PRODUTOS ORDER BY PRECO_DE_LISTA;

-- Exemplo 4: Ordenação ascendente por preço de lista (opcional, pois o padrão é ASC)
SELECT * FROM TABELA_DE_PRODUTOS ORDER BY PRECO_DE_LISTA ASC;

-- Exemplo 5: Ordenação descendente por preço de lista
SELECT * FROM TABELA_DE_PRODUTOS ORDER BY PRECO_DE_LISTA DESC;

-- Exemplo 6: Ordenação alfabética por nome do produto
SELECT * FROM TABELA_DE_PRODUTOS ORDER BY NOME_DO_PRODUTO;

-- Exemplo 7: Ordenação por embalagem e nome do produto
SELECT * FROM TABELA_DE_PRODUTOS ORDER BY EMBALAGEM, NOME_DO_PRODUTO;

-- Exemplo 8: Ordenação descendente por embalagem e nome do produto
SELECT * FROM TABELA_DE_PRODUTOS ORDER BY EMBALAGEM DESC, NOME_DO_PRODUTO DESC;

-- Exemplo 9: Selecionando os 5 produtos mais caros
SELECT TOP 5 * FROM TABELA_DE_PRODUTOS ORDER BY PRECO_DE_LISTA DESC;
```