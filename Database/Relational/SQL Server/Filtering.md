
To filter data in [[SQL Server]], the `SELECT` with `WHERE` should be used, as we saw in `DELETE` and `UPDATE`.
```sql
DELETE FROM [TABELA DE PRODUTOS] WHERE [CODIGO DO PRODUTO] = 1000889;
SELECT * FROM [TABELA DE PRODUTOS] WHERE SABOR = 'Uva'
SELECT * FROM [TABELA DE PRODUTOS] WHERE SABOR = 'Limão'
```
### Updating multiples registers
In this example, we filtered the records where the packaging is Can and added 10% to its price.
```sql
UPDATE [TABELA DE PRODUTOS] SET [PRECO DE LISTA] = [PRECO DE LISTA] * 1.1 WHERE [EMBALAGEM] = 'Lata'
```
## Filtering by bigger, smaller or different
```sql
SELECT * FROM [TABELA DE PRODUTOS] WHERE [PRECO DE LISTA] > 7.004;
SELECT * FROM [TABELA DE PRODUTOS] WHERE [PRECO DE LISTA] <> 7.004; //different
SELECT * FROM [TABELA DE PRODUTOS] WHERE [PRECO DE LISTA] >= 7.004;
SELECT * FROM [TABELA DE PRODUTOS] WHERE [EMBALAGEM] >= 'Lata' ;    //acording to ASC 
```
## Fieltering by dates
```sql
SELECT * FROM [TABELA DE CLIENTES] WHERE [DATA DE NASCIMENTO] = '1995-09-11';
SELECT * FROM [TABELA DE CLIENTES] WHERE [DATA DE NASCIMENTO] > '1995-09-11';
SELECT * FROM [TABELA DE CLIENTES] WHERE [DATA DE NASCIMENTO] < '1995-09-11';
SELECT * FROM [TABELA DE CLIENTES] WHERE YEAR [DATA DE NASCIMENTO] = 1995;

SELECT [NOME], [ESTADO], [DATA DE NASCIMENTO]
, YEAR ([DATA DE NASCIMENTO]) AS ANO
, MONTH ([DATA DE NASCIMENTO]) AS MES
, DAY ([DATA DE NASCIMENTO]) AS DIA
FROM [TABELA DE CLIENTES];

SELECT [NOME], [ESTADO], [DATA DE NASCIMENTO]
, YEAR ([DATA DE NASCIMENTO]) AS ANO
, MONTH ([DATA DE NASCIMENTO]) AS MES
, DAY ([DATA DE NASCIMENTO]) AS DIA
FROM [TABELA DE CLIENTES];
WHERE MONTH ([DATA DE NASCIMENTO]) = 9;
```
## Compound filters
```sql
SELECT * FROM [TABELA DE CLIENTES] WHERE DAY [DATA DE NASCIMENTO] =12 AND [BAIRRO] = 'Tijuca';
SELECT * FROM [TABELA DE CLIENTES] WHERE [BAIRRO] = 'Jardins' OR [BAIRRO] = 'Tijuca';
```
### Filter queries
```sql
SELECT FROM CLIENTE WHERE CLIENTE= 'CLIENTE1';
SELECT * FROM TABELA_DE_PRODUTOS WHERE CODIGO_DO_PRODUTO = 290478;
SELECT * FROM TABELA_DE_PRODUTOS WHERE SABOR = 'Laranja';

//ambas retornam os mesmos valores:
SELECT * FROM TABELA_DE_PRODUTOS WHERE EMBALAGEM = 'PET';
SELECT * FROM TABELA_DE_PRODUTOS WHERE EMBALAGEM = 'pet';
```

### Quantitative queries
```sql
SELECT * FROM TABELA_DE_CLIENTES WHERE IDADE < 20;
SELECT * FROM TABELA_DE_CLIENTES WHERE IDADE > 20;

SELECT * FROM TABELA_DE_CLIENTES WHERE IDADE < = 20;
SELECT * FROM TABELA_DE_CLIENTES WHERE IDADE <> 18;

SELECT * FROM TABELA_DE_CLIENTES WHERE DATA_DE_NASCIMENTO >= '1995-11-14';

//Inclui Lapa e valores após, em ordem alfabética
SELECT * FROM TABELA_DE_CLIENTES WHERE BAIRRO >= 'Lapa';
```
### Expressões lógicas
```sql
-- Selecionando todo o conteúdo da tabela de produtos
SELECT * FROM TABELA_DE_PRODUTOS;

-- Filtrando por sabor manga e tamanho 470 ml
SELECT * FROM TABELA_DE_PRODUTOS WHERE SABOR = 'Manga' AND TAMANHO ='470 ml';

-- Filtrando por sabor manga ou tamanho 470 ml
SELECT * FROM TABELA_DE_PRODUTOS WHERE SABOR = 'Manga' OR TAMANHO ='470 ml';

-- Aplicando o NOT na expressão de filtro
SELECT * FROM TABELA_DE_PRODUTOS WHERE NOT (SABOR = 'Manga' AND TAMANHO='470 ml');

-- Filtrando por vários sabores usando IN
SELECT * FROM TABELA_DE_PRODUTOS WHERE SABOR IN ('Manga', 'Laranja', 'Melancia');

-- Filtrando por sabores específicos e tamanho 1 Litro
SELECT * FROM TABELA_DE_PRODUTOS WHERE SABOR IN ('Manga', 'Laranja', 'Melancia') AND TAMANHO = '1 Litro';

-- Filtrando clientes das cidades do Rio de Janeiro e São Paulo
SELECT * FROM TABELA_DE_CLIENTES WHERE CIDADE IN ('Rio de Janeiro', 'Sao Paulo');

-- Filtrando clientes das cidades do Rio de Janeiro e São Paulo com idade maior ou igual a 20
SELECT * FROM TABELA_DE_CLIENTES WHERE CIDADE IN ('Rio de Janeiro', 'Sao Paulo') AND IDADE >= 20;

-- Filtrando clientes das cidades do Rio de Janeiro e São Paulo com idade entre 20 e 25
SELECT * FROM TABELA_DE_CLIENTES WHERE CIDADE IN ('Rio de Janeiro', 'Sao Paulo') AND (IDADE >= 20 AND IDADE <= 25);

-- Filtrando clientes das cidades do Rio de Janeiro e São Paulo com idade entre 20 e 25 usando BETWEEN
SELECT * FROM TABELA_DE_CLIENTES WHERE CIDADE IN ('Rio de Janeiro', 'Sao Paulo') AND (IDADE BETWEEN 20 AND 25);
```
### Like
- O comando **`LIKE`** é usado para realizar filtros em bancos de dados com base em expressões textuais.
- O símbolo **`%`** é utilizado como um coringa para representar qualquer sequência de caracteres.
- **`%TESTE%`** seleciona registros que contenham a palavra 'TESTE' em qualquer posição do campo.
- **`%Limão`** seleciona registros em que o campo termina com a palavra 'Limão'.
- **`%Maca`** seleciona registros em que o campo contém a palavra 'Maca' em qualquer posição.
- **`Morango%`** seleciona registros em que o campo começa com a palavra 'Morango'.
- O operador lógico **`AND`** é usado para combinar múltiplos critérios de filtro.

```sql
-- Selecionar todos os registros da tabela CLIENTE onde o campo contém a expressão 'TESTE'
SELECT * FROM CLIENTE WHERE CAMPO LIKE '%TESTE%';

-- Selecionar todos os registros da tabela TABELA_DE_PRODUTOS onde o campo SABOR contém a palavra 'Limão'
SELECT * FROM TABELA_DE_PRODUTOS WHERE SABOR LIKE '%Limão';

-- Selecionar todos os registros da tabela TABELA_DE_PRODUTOS onde o campo SABOR contém a palavra 'Maçã'
SELECT * FROM TABELA_DE_PRODUTOS WHERE SABOR LIKE '%Maca';

-- Selecionar todos os registros da tabela TABELA_DE_PRODUTOS onde o campo SABOR começa com a palavra 'Morango' e a EMBALAGEM é igual a 'PET'
SELECT * FROM TABELA_DE_PRODUTOS WHERE (SABOR LIKE 'Morango%') AND (EMBALAGEM = 'PET');
```
## Distinct
Is a keyword used in a SELECT statement to eliminate duplicate rows from the result set. It allows you to retrieve unique values from a specific column or a combination of columns. For example, if you have a table with a column 'Country', the DISTINCT keyword will return a list of unique countries from the table without any duplicates. The syntax for using the DISTINCT keyword is:

`SELECT DISTINCT column1, column2, ... FROM table_name`

This will return all unique combinations of the specified columns from the table.
```sql
//Busca por valores unicos de embalagens
SELECT DISTINCT EMBALAGEM FROM TABELA_DE_PRODUTOS

//Busca embalagens de usadas por um sabor especifico
SELECT DISTINCT EMBALAGEM FROM TABELA _DE_PRODUTOS WHERE SABOR = 'Maca';

//Busca as possiveis combinações de embalagens e sabor
SELECT DISTINCT EMBALAGEM, SABOR FROM TABELA _DE_PRODUTOS;
```

## TOP
is used to limit the number of rows returned by a SELECT statement.
```sql
SELECT TOP 5 * FROM TABELA_DE_PRODUTOS;
SELECT TOP 5 * FROM TABELA_DE_PRODUTOS WHERE SABOR = 'Maca';
```
