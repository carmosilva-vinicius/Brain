These [[Database/Relational/SQL Server/Functions|Functions]] convert an expression of one data type to another.

```sql
-- Funções de conversão no SQL Server

-- Conversão de data para texto usando a função CONVERT e máscaras
-- A máscara é definida por um número que representa um formato de saída

-- Exemplo: Conversão da data atual para texto no formato yyyy-mm-dd
SELECT CONVERT(VARCHAR(10), GETDATE(), 121);

-- Conversão da data de nascimento dos clientes para texto com máscara 106 (dd mon yyyy)
SELECT DATA_DE_NASCIMENTO, CONVERT(VARCHAR(25), DATA_DE_NASCIMENTO, 106)
FROM TABELA_DE_CLIENTES;

-- Conversão de números para texto usando a função CONCAT
-- Exemplo: Concatenação do texto "O preço de lista é: " com o campo PRECO_DE_LISTA
SELECT NOME_DO_PRODUTO, CONCAT('O preço de lista é: ', PRECO_DE_LISTA) AS PRECO
FROM TABELA_DE_PRODUTOS;

-- Conversão explícita de números para texto usando a função CAST
-- Exemplo: Conversão explícita do campo PRECO_DE_LISTA para VARCHAR(10)
SELECT NOME_DO_PRODUTO, CONCAT('O preço de lista é: ', CAST(PRECO_DE_LISTA AS VARCHAR(10))) AS PRECO
FROM TABELA_DE_PRODUTOS;
```