To update the data in [[SQL Server]], we must use a filter that limits which records should be changed, otherwise all rows would be changed. The famous _Update withou WHERE._

```sql
UPDATE [TABELA DE PRODUTOS]
SET [PRECO DE LISTA] = 7.50
WHERE [CODIGO DO PRODUTO] = '1088126';

UPDATE [TABELA DE PRODUTOS]
SET [EMBALAGEM] = 'Garrafa'
WHERE [CODIGO DO PRODUTO] = '1088126';
```

Is there a way to execute these two commands at once?
```sql
UPDATE [TABELA DE PRODUTOS]
SET [PRECO DE LISTA] = 7.50, [EMBALAGEM] = 'Garrafa'
WHERE [CODIGO DO PRODUTO] = '1088126';
```

## Getting data from other table

We can use [[Join]] to update data of one table, using data of another table.
```sql
UPDATE A SET A.PRECO_LISTA = B.PRECO_DE_LISTA 
FROM PRODUTOS A 
INNER JOIN SUCOS_FRUTAS.DBO.TABELA_DE_PRODUTOS B 
ON A.CODIGO = B.CODIGO_DO_PRODUTO;
```
### Merge
Another way to do it is using merge:
```sql
MERGE INTO PRODUTOS A 
USING SUCOS_FRUTAS.DBO.TABELA_DE_PRODUTOS B 
ON A CODIGO = B.CODIGO_DO_PRODUTO 
WHEN MATCHED THEN 
UPDATE SET A.PRECO_LISTA = B.PRECO_DE_LISTA;
```