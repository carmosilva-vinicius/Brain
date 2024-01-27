A view is a virtual table whose contents are defined by a query. Like a table, a view consists of a set of named columns and rows of data. Unless indexed, a view does not exist as a stored set of data values in a database. The rows and columns of data come from tables referenced in the query defining the view and are produced dynamically when the view is referenced. [soruce](https://learn.microsoft.com/en-us/sql/relational-databases/views/views?view=sql-server-ver16)

```sql
-- Consulta usando subquery com substituição do HAVING por WHERE:
SELECT ESTADO_FUNC.ESTADO, ESTADO_FUNC.NUM_FUNC
FROM (
    SELECT ESTADO, SUM(NUM_FUNC)
    FROM CLIENTE
    GROUP BY ESTADO
    ORDER BY ESTADO
) ESTADO_FUNC
WHERE ESTADO_FUNC.NUM_FUNC > 60;

-- Criação da view MEDIA_EMBALAGENS para reutilização da subquery:
CREATE VIEW MEDIA_EMBALAGENS AS
SELECT EMBALAGEM, AVG(PRECO_DE_LISTA) AS PRECO_MEDIO
FROM TABELA_DE_PRODUTOS
GROUP BY EMBALAGEM;

-- Utilização da view MEDIA_EMBALAGENS em uma consulta:
SELECT EMBALAGEM, PRECO_MEDIO
FROM MEDIA_EMBALAGENS
WHERE PRECO_MEDIO <= 10;
```
