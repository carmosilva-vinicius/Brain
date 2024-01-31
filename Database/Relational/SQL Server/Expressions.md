Is a combination of symbols and operators that the [[SQL Server]] Database Engine evaluates to obtain a single data value. Simple expressions can be a single constant, variable, column, or scalar function. Operators can be used to join two or more simple expressions into a complex expression. [source](https://learn.microsoft.com/en-us/sql/t-sql/language-elements/expressions-transact-sql?view=sql-server-ver16)

## Categorizing with  **CASE** and **WHEN**

```sql
-- Exemplo 1: Utilizando o CASE para classificar clientes
SELECT CLIENTE,
  (CASE
    WHEN NUM_FUNC >= 20 THEN 'GRANDE'
    ELSE 'PEQUENO'
   END) 
FROM CLIENTE;

-- Exemplo 2: Utilizando o CASE para classificar produtos por preço
SELECT NOME_DO_PRODUTO, PRECO_DE_LISTA,
  (CASE
    WHEN PRECO_DE_LISTA > 12 THEN 'PRODUTO CARO'
    WHEN PRECO_DE_LISTA >= 7 AND PRECO_DE_LISTA < 12 THEN 'PRODUTO EM CONTA'
    ELSE 'PRODUTO BARATO'
   END) AS CLASSIFICACAO
FROM TABELA_DE_PRODUTOS
WHERE SABOR = 'Manga'
ORDER BY CLASSIFICACAO;

-- Exemplo 3: Contando o número de produtos em cada classificação
SELECT
  (CASE
    WHEN PRECO_DE_LISTA > 12 THEN 'PRODUTO CARO'
    WHEN PRECO_DE_LISTA >= 7 AND PRECO_DE_LISTA < 12 THEN 'PRODUTO EM CONTA'
    ELSE 'PRODUTO BARATO'
   END) AS CLASSIFICACAO,
   COUNT(*) AS NUMERO_DE_PRODUTOS
FROM TABELA_DE_PRODUTOS
GROUP BY
  (CASE
    WHEN PRECO_DE_LISTA > 12 THEN 'PRODUTO CARO'
    WHEN PRECO_DE_LISTA >= 7 AND PRECO_DE_LISTA < 12 THEN 'PRODUTO EM CONTA'
    ELSE 'PRODUTO BARATO'
   END);
```