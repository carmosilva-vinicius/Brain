SQL Server performs sort, intersect, union, and difference operations using in-memory sorting and hash join technology. Using this type of query plan, SQL Server supports vertical table partitioning. [source](https://learn.microsoft.com/en-us/sql/relational-databases/performance/joins?view=sql-server-ver16)

SQL Server implements logical join operations, as determined by Transact-SQL syntax:

- Inner join
- Left outer join
- Right outer join
- Full outer join
- Cross join

# Inner join

**Sobre o `INNER JOIN` e chaves estrangeiras:** embora não seja obrigatório ter uma chave estrangeira para utilizar o `INNER JOIN`, as chaves estrangeiras são candidatas naturais para realizar esse tipo de junção. Isso ocorre porque as chaves estrangeiras têm mais performance quando são utilizados índices nos campos correspondentes. O exemplo apresentado mostra a junção entre as tabelas de vendedores e notas fiscais, que possuem uma chave estrangeira em comum (matrícula), facilitando a ligação entre os registros.

**Sobre hierarquia:** é uma boa prática estabelecer uma hierarquia entre as tabelas quando se realiza uma junção usando `INNER JOIN`. Isso significa que a tabela considerada superior em termos de hierarquia deve ser colocada no comando `FROM`, enquanto a tabela inferior é utilizada no `INNER JOIN`. No exemplo prático apresentado, a tabela de vendedores é considerada superior à tabela de notas fiscais, pois a tabela de notas fiscais depende da existência da tabela de vendedores através do campo de chave estrangeira. Seguir essa hierarquia é uma boa prática para facilitar a compreensão e manutenção do código SQL.

```sql
-- Exemplo de junção de tabelas usando o comando INNER JOIN

-- Selecionando campos de duas tabelas diferentes
-- Ligação entre as tabelas é feita por um campo em comum
-- É necessário especificar a tabela de origem de cada campo selecionado

-- Exemplo genérico de comando de join:
-- SELECT campos FROM tabela1 INNER JOIN tabela2 ON tabela1.campo = tabela2.campo

-- Exemplo prático:

-- Selecionando campos da tabela de vendedores e da tabela de notas fiscais
-- Ligação entre as tabelas é feita pelo campo 'matrícula'
SELECT MATRICULA, NOME, COUNT(*) AS NUMERO_NOTAS
FROM NOTAS_FISCAIS
INNER JOIN TABELA_DE_VENDEDORES
ON NOTAS_FISCAIS.MATRICULA = TABELA_DE_VENDEDORES.MATRICULA
GROUP BY MATRICULA, NOME;

-- A mesma consulta acima, utilizando aliases para as tabelas
SELECT NF.MATRICULA, TV.NOME, COUNT(*) AS NUMERO_NOTAS
FROM NOTAS_FISCAIS NF
INNER JOIN TABELA_DE_VENDEDORES TV
ON NF.MATRICULA = TV.MATRICULA
GROUP BY NF.MATRICULA, TV.NOME;
```

# LEFFT, RIGHT, FULL and CROSS JOIN

```sql
-- Exemplo de inner join
SELECT TE.NOME, TD.HOBBY FROM TABELA_ESQUERDA TE 
INNER JOIN TABELA_DIREITA TD ON TE.IDENTIFICADOR = TD.IDENTIFICADOR;
-- Seleciona o nome da tabela da esquerda e o hobby da tabela da direita
-- Usando alias TE e TD para representar as tabelas
-- Fazendo a junção com base no campo IDENTIFICADOR

-- Exemplo de left join
SELECT TE.NOME, TD.HOBBY FROM TABELA_ESQUERDA TE 
LEFT JOIN TABELA_DIREITA TD ON TE.IDENTIFICADOR = TD.IDENTIFICADOR;
-- Seleciona o nome da tabela da esquerda e o hobby da tabela da direita
-- Utilizando o left join para buscar todos da tabela da esquerda e somente os em comum da tabela da direita

-- Exemplo de right join
SELECT TE.NOME, TD.HOBBY FROM TABELA_ESQUERDA TE 
RIGHT JOIN TABELA_DIREITA TD ON TE.IDENTIFICADOR = TD.IDENTIFICADOR;
-- Seleciona o nome da tabela da esquerda e o hobby da tabela da direita
-- Utilizando o right join para buscar somente os em comum da tabela da esquerda e todos da tabela da direita

-- Exemplo de full join
SELECT TE.NOME, TD.HOBBY FROM TABELA_ESQUERDA TE 
FULL JOIN TABELA_DIREITA TD ON TE.IDENTIFICADOR = TD.IDENTIFICADOR;
-- Seleciona o nome da tabela da esquerda e o hobby da tabela da direita
-- Utilizando o full join para buscar todos da tabela da esquerda e todos da tabela da direita

-- Exemplo de cross join
SELECT TE.NOME, TD.HOBBY FROM TABELA_ESQUERDA TE 
CROSS JOIN TABELA_DIREITA TD;
-- Seleciona o nome da tabela da esquerda e o hobby da tabela da direita
-- Utilizando o cross join para fazer uma análise combinatória entre todas as linhas das duas tabelas
```

## UNION

```sql
-- Explicação sobre juntar e unir consultas
-- Juntar duas consultas: colocar uma consulta do lado da outra através de campos em comum
-- Unir duas consultas: resultado com número de linhas da primeira consulta e depois da segunda consulta

-- Requisitos para unir consultas:
-- 1. Número de campos selecionados nas consultas deve ser igual
-- 2. Os campos devem ter o mesmo tipo

-- Exemplo de unir consultas usando UNION:
-- Primeira consulta: campos cliente, cidade e estado
-- Segunda consulta: campos fornecedor, cidade e estado
SELECT cliente, cidade, estado FROM tabela_de_clientes
UNION
SELECT fornecedor, cidade, estado FROM tabela_de_fornecedores;

-- Resultado: união dos campos cliente e fornecedor com correspondência nos demais campos

-- Union elimina linhas repetidas, aplicando distinct ao resultado
-- Para manter linhas repetidas, usar UNION ALL

-- Exemplo de uso do UNION e UNION ALL
SELECT cliente, cidade, estado FROM tabela_de_clientes
UNION
SELECT fornecedor, cidade, estado FROM tabela_de_fornecedores;

SELECT cliente, cidade, estado FROM tabela_de_clientes
UNION ALL
SELECT fornecedor, cidade, estado FROM tabela_de_fornecedores;

-- Contagem de bairros distintos em tabelas de clientes e vendedores
SELECT DISTINCT bairro FROM tabela_de_clientes;

SELECT DISTINCT bairro FROM tabela_de_vendedores;

-- Union de consultas para obter bairros distintos de clientes e vendedores
SELECT DISTINCT bairro FROM tabela_de_clientes
UNION
SELECT DISTINCT bairro FROM tabela_de_vendedores;

-- Union All de consultas para obter todos os bairros de clientes e vendedores, incluindo repetições
SELECT DISTINCT bairro FROM tabela_de_clientes
UNION ALL
SELECT DISTINCT bairro FROM tabela_de_vendedores;

-- Adicionando coluna de origem aos resultados das consultas
SELECT DISTINCT bairro, 'CLIENTE' AS origem FROM tabela_de_clientes
UNION ALL
SELECT DISTINCT bairro, 'FORNECEDOR' AS origem FROM tabela_de_vendedores;

SELECT DISTINCT bairro, 'CLIENTE' AS origem FROM tabela_de_clientes
UNION
SELECT DISTINCT bairro, 'FORNECEDOR' AS origem FROM tabela_de_vendedores;
```