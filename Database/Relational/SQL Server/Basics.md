Getting start with beginner [[SQL Server]] commands:
# Creating a database

In summary, this script creates a new database called `SUCOS_VENDAS_02` with a primary data file and a transaction log file, both having an initial size of 10 MB, a maximum size of 50 MB, and a growth increment of 5 MB. The data and log files are located in the '/tmp/TEMP2/' directory with the respective file names 'SUCOS_VENDAS_02.MDF' and 'SUCOS_VENDAS_02.LDF'.

```sql
CREATE DATABASE SUCOS_VENDAS_02
ON (NAME = 'SUCOS_VENDAS.DAT',
	FILENAME = '/tmp/TEMP2/SUCOS_VENDAS_02.MDF',
	SIZE = 10MB,
	MAXSIZE = 50MB,
	FILEGROWTH = 5MB)
LOG ON
(NAME = 'SUCOS_VENDAS.LOG',
	FILENAME = '/tmp/TEMP2/SUCOS_VENDAS_02.LDF',
	SIZE = 10MB,
	MAXSIZE = 50MB,
	FILEGROWTH = 5MB);
```

# Creating tables and exploring data types

```sql
CREATE TABLE [TABELA DE CLIENTES]
   (
   [CPF] [CHAR] (11),
   [NOME] [VARCHAR] (100),
   [ENDERECO1] [VARCHAR] (150),
   [ENDERECO2] [VARCHAR] (150),
   [BAIRRO] [VARCHAR] (50),
   [CIDADE] [VARCHAR] (50),
   [ESTADO] [CHAR] (2),
   [CEP] [CHAR] (8),
   [DATA DE NASCIMENTO] [DATE],
   [IDADE] [SMALLINT],
   [GENERO] [CHAR] (1),
   [LIMITE DE CREDITO] [MONEY],
   [VOLUME DE COMPRA] [FLOAT],
   [PRIMEIRA COMPRA] [BIT]
   )

CREATE TABLE [TABELA DE VENDEDORES]
( [MATRICULA] varchar(5),
[NOME] varchar(100),
[PERCENTUAL COMISSÃO] float);
```

# Inserting data

If the order of values is the same as the columns in the table, the column names can be omitted, such as: `INSERT INTO [TABELA DE VENDEDORES] VALUES ('00235','Márcio Almeida Silva',0.08);`

```sql
INSERT INTO [TABELA DE PRODUTOS]
([CODIGO DO PRODUTO],[NOME DO PRODUTO],[EMBALAGEM],[TAMANHO],[SABOR],[PRECO DE LISTA])
VALUES
('1040107','Light - 350 ml - Melância','Lata','350 ml','Melância',4.56);

INSERT INTO [TABELA DE VENDEDORES]
([MAtRICULA], [NOME], [PERCENTUAL COMISSÃO])
VALUES
('00235','Márcio Almeida Silva',0.08);
```

Iserting more than one register, in a same INSERT query. It has a better performance comparing with the example above.

```sql
INSERT INTO [TABELA DE PRODUTOS]
VALUES
('1088126','Linha Citros - 1 Litro - Limão','PET','1 Litro','Limão',7),
('544931','Frescor do Verão - 350 ml - Limão','Lata','350 ml','Limão',2.46)
```

# Updating data

To update the data, we must use a filter that limits which records should be changed, otherwise all rows would be changed. The famous _Update withou WHERE._

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

# Deleting data

Similar to `UPDATE` , `DELETE` needs to works with a `WHERE` filter

```sql
DELETE FROM [TABELA DE PRODUTOS]
WHERE [CODIGO DO PRODUTO] = '1004327';
```

# Alter Tables

Adding columns in a table:

```sql
ALTER TABLE [TABELA DE PRODUTOS] ADD COLUMN
```

Pratical example: Alter a columns to `not nuallable`, to allow it to be a `Pirmary Key` :

```sql
ALTER TABLE [TABELA DE PRODUTOS] ALTER COLUMN [CODIGO DO PRODUTO] VARCHAR(20) NOT NULL;
ALTER TABLE [TABELA DE PRODUTOS] ADD CONSTRAINT PK_TABELA_DE_PRODUTOS
PRIMARY KEY CLUSTERED ([CODIGO DO PRODUTO])
```

# Using Dates and Logical

```sql
INSERT INTO [TABELA DE CLIENTES]
VALUES
('00384393555','Maria Clara','Rua Projetada A','Numero 233','Copacabana',
'Rio de janeiro','RJ','20000000','1975-03-21',47,'F',200000,3000.30,'TRUE');

//  OR

INSERT INTO [TABELA DE CLIENTES]
VALUES
('00384393555','Maria Clara','Rua Projetada A','Numero 233','Copacabana',
'Rio de janeiro','RJ','20000000','1975-03-21',47,'F',200000,3000.30,1);
```

# Using Alias

To change a name of a column in a query

```sql
SELECT [NOME] AS [NOME DO CLIENTE], [CPF] AS [IDENTIFICADOR]]
FROM [TABELA DE CLIENTES]
```

We can use ALIAS for columns or tables. In table it could be used to make queries in tables that has columns with the same name.
```sql
SELECT CPF AS IDENTIFICADOR, NOME AS [NOME DE CLIENTE], 
BAIRRO, CIDADE FROM TABELA_DE_CLIENTES;

SELECT CPF AS IDENTIFICADOR, NOME AS [NOME DE CLIENTE], 
BAIRRO, CIDADE FROM TABELA_DE_CLIENTES TDC;
SELECT TDC.CPF, TDC.NOME, TDC.BAIRRO FROM TABELA_DE_CLIENTES TDC;

SELECT TABELA_DE_CLIENTES.CPF, TABELA_DE_CLIENTE.NOME 
FROM TABELA_DE_CLIENTES;
```
