In [[SQL Server]], a subquery is a query that is nested inside a `SELECT`, `INSERT`, `UPDATE`, or `DELETE` statement, or inside another subquery. [source](https://learn.microsoft.com/en-us/sql/relational-databases/performance/subqueries?view=sql-server-ver16)

## Subconsultas

```sql
-- Consulta 1: Testar quais são os clientes que têm número de funcionários igual a 10
SELECT CLIENTE FROM CLIENTE WHERE NUM_FUNC = 10;

-- Consulta 2: Pegar os movimentos apenas dos clientes obtidos na consulta anterior
SELECT * FROM MOVIMENTO WHERE CLIENTE IN ('CLIENTE1', 'CLIENTE2');

-- Consulta 3: Realizar a mesma consulta anterior utilizando uma subquery
SELECT * FROM MOVIMENTO WHERE CLIENTE IN (
    SELECT CLIENTE FROM CLIENTE
) WHERE NUM_FUNC = 10;

-- Consulta com subquery como tabela no FROM
SELECT SUBTABELA.* FROM 
(
    SELECT CLIENTE, CIDADE,ESTADO
    FROM CLIENTE
    UNION
    SELECT FORNECEDOR, CIDADE,ESTADO
    FROM FORNECEDOR
) SUBTABELA; -- Nesse caso, deve conter ALIAS

-- Consulta para listar somente clientes onde o bairro desse cliente é onde há vendedores
SELECT * FROM TABELA_DE_CLIENTES 
WHERE BAIRRO IN ('Cobacabana', 'Jardins', 'Santo Amaro', 'Tijuca');

-- Consulta utilizando subquery para obter os bairros onde há vendedores e filtrar os clientes
SELECT * FROM TABELA_DE_CLIENTES 
WHERE BAIRRO IN (SELECT DISTINCT BAIRRO FROM TABELA_DE_VENDEDORES);
```

```sql
-- Exemplo com HAVING
SELECT EMBALAGEM, AVG(PRECO_DE_LISTA) AS PRECO_MEDIO 
FROM TABELA_DE_PRODUTOS GROUP BY EMBALAGEM 
HAVING AVG(PRECO_LISTA) <= 10;

-- Exemplo com subquery
SELECT MEDIA_EMBALAGENS.EMBALAGEM, MEDIA_EMBALAGENS.PRECO_MEDIO
FROM (
    SELECT EMBALAGEM, AVG(PRECO_DE_LISTA) AS PRECO_MEDIO
    FROM TABELA_DE_PRODUTOS
    GROUP BY EMBALAGEM
) MEDIA_EMBALAGENS
WHERE MEDIA_EMBALAGENS.PRECO_MEDIO <= 10;
```