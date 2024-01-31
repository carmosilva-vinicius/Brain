## Group By
To use the `group by` in [[SQL Server]], it is important that you have, in the field selection, at least one field in which we apply what we call an aggregation function. The aggregation functions contained in SQL are four: the `SUM`, the `AVG`, the `MAX` and the `MIN`.
```sql
-- Seleciona a coluna CIDADE e calcula a soma das idades agrupadas por cidade
SELECT CIDADE, SUM(IDADE) AS IDADE 
FROM TABELA_DE_CLIENTES
GROUP BY CIDADE;

-- Seleciona a coluna CIDADE, calcula a soma das idades e a soma dos limites de crédito agrupadas por cidade
SELECT CIDADE, SUM(IDADE) AS IDADE, SUM(LIMITE_DE_CREDITO) AS CREDITO
FROM TABELA_DE_CLIENTES
GROUP BY CIDADE;

-- Seleciona a coluna CIDADE, calcula a média das idades e a soma dos limites de crédito agrupadas por cidade
SELECT CIDADE, AVG(IDADE) AS IDADE, SUM(LIMITE_DE_CREDITO)
FROM TABELA_DE_CLIENTES
GROUP BY CIDADE;

-- Seleciona a coluna CIDADE e conta o número de clientes agrupados por cidade
SELECT CIDADE, COUNT(*) AS NUMERO_DE_CLIENTES
FROM TABELA_DE_CLIENTES
GROUP BY CIDADE;

-- Seleciona a coluna EMBALAGEM e conta o número de produtos por embalagem, filtrando apenas os de sabor 'Laranja'
SELECT EMBALAGEM, COUNT(*) AS NUMERO_DE_PRODUTOS
FROM TABELA_DE_PRODUTOS
WHERE SABOR = 'Laranja'
GROUP BY EMBALAGEM;
```
## Having
HAVING is a clause used in SQL queries that allows filtering the results of an aggregation. It is used in conjunction with the GROUP BY clause to specify conditions that must be met by aggregation functions, such as `SUM`, `COUNT`, `AVG`, `MAX`, `MIN`, among others.

Unlike the `WHERE` clause, which is used to [[Filtering|filter]] data before aggregation, `HAVING` is applied after aggregation, allowing you to filter the results based on the resulting values from the aggregation functions.
```sql
-- Exemplo do uso da cláusula HAVING
-- Filtro usando função de agregação

-- Consulta original com cláusula HAVING
SELECT ESTADO, SUM(NUM_FUNC) FROM CLIENTE
GROUP BY ESTADO HAVING SUM(NUM_FUNC) > 60;

-- Consulta com filtro incorreto usando WHERE e função de agregação
-- WHERE não pode ser usado com funções de agregação
-- Essa consulta não funciona
-- WHERE SUM(NUM_FUNC) > 60;

-- Consulta correta usando HAVING para filtrar a agregação
SELECT ESTADO, SUM(NUM_FUNC) FROM CLIENTE
GROUP BY ESTADO HAVING SUM(NUM_FUNC) > 60;

-- Consulta inicial para exibir todos os clientes
SELECT * FROM TABELA_DE_CLIENTES;

-- Consulta com agregação para obter a soma do limite de crédito por estado
SELECT ESTADO, SUM(LIMITE_DE_CREDITO) AS CREDITO
FROM TABELA_DE_CLIENTES GROUP BY ESTADO;

-- Consulta com filtro incorreto usando WHERE e função de agregação
-- Essa consulta gera um erro, pois a agregação não pode aparecer na cláusula WHERE
-- WHERE SUM(LIMITE_DE_CREDITO_) >= 900000
-- GROUP BY ESTADO;

-- Consulta correta usando HAVING para filtrar a agregação
SELECT ESTADO, SUM(LIMITE_DE_CREDITO) AS CREDITO
FROM TABELA_DE_CLIENTES GROUP BY ESTADO
HAVING SUM(LIMITE_DE_CREDITO) >= 900000;

-- Consulta para obter o maior e menor preço de produtos por tipo de embalagem
SELECT EMBALAGEM, MAX(PRECO_DE_LISTA) AS PRECO_MAX, MIN(PRECO_DE_LISTA) AS PRECO_MIN
FROM TABELA_DE_PRODUTOS GROUP BY EMBALAGEM;

-- Consulta com filtro para exibir apenas produtos com preço maior que dez unidades monetárias
SELECT EMBALAGEM, MAX(PRECO_DE_LISTA) AS PRECO_MAX, MIN(PRECO_DE_LISTA) AS PRECO_MIN
FROM TABELA_DE_PRODUTOS
WHERE PRECO_DE_LISTA >= 10
GROUP BY EMBALAGEM;

-- Consulta com filtro usando HAVING para exibir apenas produtos com o maior preço de lista maior que 20 unidades monetárias
SELECT EMBALAGEM, MAX(PRECO_DE_LISTA) AS PRECO_MAX, MIN(PRECO_DE_LISTA) AS PRECO_MIN
FROM TABELA_DE_PRODUTOS
WHERE PRECO_DE_LISTA >= 10
GROUP BY EMBALAGEM
HAVING MAX(PRECO_DE_LISTA) >= 20;
```