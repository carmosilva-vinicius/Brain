Here are the main functions of [[SQL Server]]
### Strings:

```sql
-- Função lower: converte uma expressão de caracteres para minúsculas
SELECT LOWER('o jOÃO eSTEVE lá em casa') AS lower_resultado;

-- Função upper: converte uma expressão de caracteres para maiúsculas
SELECT UPPER('o jOÃO eSTEVE lá em casa') AS upper_resultado;

-- Função concat: concatena várias expressões de caracteres
SELECT CONCAT('O JOÃO', ' ESTEVE ', 'LÁ EM CASA') AS concat_resultado;

-- Função right: retorna a parte direita de uma cadeia de caracteres
SELECT RIGHT('O JOÃO ESTEVE LÁ EM CASA', 6) AS right_resultado;

-- Função left: retorna a parte esquerda de uma cadeia de caracteres
SELECT LEFT('O JOÃO ESTEVE LÁ EM CASA', 6) AS left_resultado;

-- Função replicate: repete uma cadeia de caracteres um número de vezes
SELECT REPLICATE('O JOÃO ESTEVE LÁ EM CASA', 2) AS replicate_resultado;

-- Função substring: retorna uma parte de uma expressão de caracteres
SELECT SUBSTRING('O JOÃO ESTEVE LÁ EM CASA', 3, 10) AS substring_resultado;

-- Função ltrim: remove os espaços em branco do início de uma cadeia de caracteres
SELECT LTRIM('          O JOÃO ESTEVE LÁ EM CASA') AS ltrim_resultado;

-- Função rtrim: remove os espaços em branco do final de uma cadeia de caracteres
SELECT RTRIM('O JOÃO ESTEVE LÁ EM CASA          ') AS rtrim_resultado;

-- Função trim: remove os espaços em branco do início e do final de uma cadeia de caracteres
SELECT TRIM('      O JOÃO ESTEVE LÁ EM CASA      ') AS trim_resultado;

-- Função replace: substitui um conjunto de caracteres por outro
SELECT REPLACE('O JOÃO ESTEVE LÁ EM CASA', ' ', '-') AS replace_resultado;

-- Função len: retorna o número de caracteres de uma expressão de caracteres
SELECT LEN('O JOÃO ESTEVE LÁ EM CASA') AS len_resultado;

-- Exemplo de uso das funções em uma consulta
SELECT NOME, LOWER(NOME) AS NOME_MINUSCULO, UPPER(NOME) AS NOME_MAIUSCULO 
FROM TABELA_DE_CLIENTES;

SELECT NOME, CONCAT(ENDERECO_1, ' ', BAIRRO, ' ', CIDADE, ' ', ESTADO, ' - ', CEP) AS ENDERECO_COMPLETO 
FROM TABELA_DE_CLIENTES;

SELECT NOME, ENDERECO_1 + ' ' + BAIRRO + ' ' + CIDADE + ' ' + ESTADO + ' - ' + CEP AS ENDERECO_COMPLETO 
FROM TABELA_DE_CLIENTES;

SELECT NOME_DO_PRODUTO, LEFT(NOME_DO_PRODUTO, 3) AS TRES_PRIMEIROS_CHAR 
FROM TABELA_DE_PRODUTOS;

SELECT TAMANHO, REPLACE((REPLACE(TAMANHO, 'Litros', 'L')), 'Litro', 'L') AS TAMANHO_MODIFICADO 
FROM TABELA_DE_PRODUTOS;
```

### Dates:

```sql
-- Vamos discutir algumas funções relacionadas com data e hora.
-- A primeira função é a "dateadd", que adiciona um número a uma parte da data.

-- Exemplo de uso da função dateadd: somar 30 dias a uma data específica
SELECT DATEADD(DAY, 30, '2022-01-01') AS Resultado
-- Resultado: '2022-01-31'

-- A função "datediff" retorna a diferença entre duas datas em um determinado "datepart"
SELECT DATEDIFF(DAY, '2022-01-01', '2022-04-12') AS Resultado
-- Resultado: 101 dias

-- A função "datepart" retorna uma parte específica da data fornecida
SELECT DATEPART(DAY, '2022-01-01') AS Resultado
-- Resultado: 1

-- A função "getdate" retorna a data atual do sistema
SELECT GETDATE() AS Resultado

-- A função "day" retorna o dia da data fornecida
SELECT DAY(GETDATE()) AS Resultado

-- A função "month" retorna o mês da data fornecida
SELECT MONTH(GETDATE()) AS Resultado

-- A função "year" retorna o ano da data fornecida
SELECT YEAR(GETDATE()) AS Resultado

-- A função "isdate" verifica se uma expressão é uma data válida
SELECT ISDATE('2022-02-31') AS Resultado
-- Resultado: 0 (falso)

-- A função "datetimefromparts" retorna uma data baseada em inteiros separados
SELECT DATETIMEFROMPARTS(2022, 12, 14, 15, 34, 22, 30) AS Resultado
-- Resultado: '2022-12-14 15:34:22.030'

-- Obtendo a data atual
SELECT GETDATE() AS Data_Hoje

-- Somando 10 dias à data atual
SELECT DATEADD(DAY, 10, GETDATE()) AS Data_Daqui_10_Dias

-- Obtendo a data que representa 48 dias atrás
SELECT DATEADD(DAY, -48, GETDATE()) AS Data_48_Dias_Atras

-- Obtendo a diferença em dias entre o primeiro dia do ano e a data atual
SELECT DATEDIFF(DAY, '2022-01-01', GETDATE()) AS Dias_Desde_Inicio_Ano

-- Obtendo a diferença em horas entre o primeiro dia do ano e a data atual
SELECT DATEDIFF(HOUR, '2022-01-01', GETDATE()) AS Horas_Desde_Inicio_Ano

-- Obtendo a diferença em meses entre o primeiro dia do ano e a data atual
SELECT DATEDIFF(MONTH, '2022-01-01', GETDATE()) AS Meses_Desde_Inicio_Ano

-- Obtendo o dia atual
SELECT DATEPART(DAY, GETDATE()) AS Dia_De_Hoje

-- Verificando se uma data é válida
SELECT ISDATE(DATETIMEFROMPARTS(2022, 02, 28, 00, 00, 00, 00)) AS Resultado
```

### Numbers:

```sql
-- Função ROUND: retorna um valor numérico arredondado com base no comprimento de precisão de arredondamento.
-- Exemplo: Arredondar o número 32.23332 com duas casas decimais
SELECT ROUND(32.23332, 2);

-- Função CEILING: retorna o menor inteiro maior ou igual à expressão numérica.
-- Exemplo: Aplicar ceiling no número 32.23332
SELECT CEILING(32.23332);

-- Função FLOOR: retorna o maior inteiro menor ou igual à expressão numérica.
-- Exemplo: Aplicar floor no número 32.23332
SELECT FLOOR(32.23332);

-- Função POWER: retorna a potência de um número.
-- Exemplo: Calcular 2 elevado à potência de 10
SELECT POWER(2, 10);

-- Função EXP: retorna o valor exponencial da expressão passada como parâmetro.
-- Exemplo: Calcular o exponencial de 10
SELECT EXP(10);

-- Função SQRT: retorna a raiz quadrada da expressão numérica.
-- Exemplo: Calcular a raiz quadrada de 144
SELECT SQRT(144);

-- Função SIGN: retorna o sinal (positivo ou negativo) da expressão numérica.
-- Exemplo: Obter o sinal do número -10
SELECT SIGN(-10);

-- Função ABS: retorna o valor absoluto (sempre positivo) da expressão numérica.
-- Exemplo: Obter o valor absoluto do número -10
SELECT ABS(-10);

-- Operador % (percent): calcula o resto da divisão entre dois números.
-- Exemplo: Calcular o resto da divisão de 10 por 3
SELECT 10 % 3;

-- Outras funções matemáticas disponíveis no SQL Server:
-- log: retorna o logaritmo natural de uma expressão float.
-- log10: retorna o logaritmo na base 10 de uma expressão float.
-- ACOS, ATAN, ASIN, COS, TAN, SIN: funções trigonométricas.
-- PI: retorna o valor de PI.
```
