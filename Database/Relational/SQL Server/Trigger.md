A trigger in [[SQL Server]] is a database object that contains SQL code designed to automatically execute when a specific event occurs in the database. These events can be related to data modifications (INSERT, UPDATE, DELETE), data definition language (DDL) operations (CREATE, ALTER, DROP), or logon activities. Triggers are associated with a particular table and are activated by these events occurring on that table. They can be used to enforce business rules, maintain data integrity, automate processes, and ensure consistency across related tables.

There are several types of triggers in SQL Server:

- **DML (Data Manipulation Language) Triggers**: These are triggered by INSERT, UPDATE, or DELETE operations on a table or view. They can operate at the statement level (affecting all rows in the operation) or at the row level (affecting individual rows).

- **DDL (Data Definition Language) Triggers**: These are fired by events related to the creation, alteration, or deletion of database objects like tables or stored procedures. They can also be set at the database or server level.

- **CLR (Common Language Runtime) Triggers**: Implemented using C# or VB.NET, these triggers allow for complex logic and operations that might not be feasible with standard T-SQL triggers, such as sending emails or interacting with external systems.

- **Logon Triggers**: These are triggered by the logon events of SQL Server users. They can be used for enforcing security policies or auditing logon activities.

Triggers are a powerful feature but require careful management due to their potential impact on database performance and data integrity. They should be used judiciously to ensure they enhance the database's functionality without introducing unnecessary overhead or complexity.

```sql
-- Cria a trigger TG_ITENS_VENDIDOS
CREATE TRIGGER TG_ITENS_VENDIDOS 
ON [dbo].[TABELA_DE_ITENS_VENDIDOS]
AFTER INSERT, UPDATE, DELETE
AS 
BEGIN
    -- Deleta todos os registros da tabela TAB_FATURAMENTO
    DELETE FROM TAB_FATURAMENTO;

    -- Insere os registros consolidados na tabela TAB_FATURAMENTO
    INSERT INTO TAB_FATURAMENTO 
    SELECT 
        TV.DATA_VENDA, 
        SUM(TIV.QUANTIDADE * TIV.PRECO) AS TOTAL_VENDA 
    FROM TABELA_DE_VENDAS TV 
    INNER JOIN TABELA_DE_ITENS_VENDIDOS TIV 
    ON TV.NUMERO = TIV.NUMERO 
    GROUP BY TV.DATA_VENDA;
END;

-- Seleciona todos os registros da tabela TAB_FATURAMENTO para verificação
SELECT * FROM TAB_FATURAMENTO;

-- Insere uma nova nota na tabela TABELA_DE_VENDAS
INSERT INTO TABELA_DE_VENDAS 
VALUES (
    '0105', '2018-05-16', '1471156710', '235', 0.18
);

-- Insere itens vendidos relacionados à nova nota
INSERT INTO TABELA_DE_ITENS_VENDIDOS 
VALUES (
    '0105', '1000889', 150, 10
);

-- Insere outra nova nota na tabela TABELA_DE_VENDAS
INSERT INTO TABELA_DE_VENDAS 
VALUES (
    '0106', '2018-05-16', '1471156710', '235', 0.18
);

-- Insere itens vendidos relacionados à segunda nova nota
INSERT INTO TABELA_DE_ITENS_VENDIDOS 
VALUES (
    '0106', '1000889', 150, 10
);

-- Atualiza a quantidade de itens vendidos para a nota fiscal 0106
UPDATE TABELA_DE_ITENS_VENDIDOS SET QUANTIDADE = 200 
WHERE NUMERO = '0106';

-- Exclui os itens vendidos relacionados à nota fiscal 0106
DELETE FROM TABELA_DE_ITENS_VENDIDOS 
WHERE NUMERO = '0106';

```