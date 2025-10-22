# 🧠 Curso 03 – Praticando SQL: Entendendo Funções de String  

Neste módulo, eu estudei sobre **manipular textos e cadeias de caracteres (strings)** em SQL, explorando funções como `UPPER`, `LOWER`, `LENGTH`, `TRIM`, `CONCAT`, `SUBSTR`, `REPLACE` e outras variações entre bancos diferentes (**SQLite**, **PostgreSQL** e **SQL Server**).  
Cada exemplo mostra o código SQL e uma explicação prática de seu uso.

---

## 🧩 Consultas e Explicações

```sql
-- 1️⃣ Transformando nomes em letras maiúsculas
SELECT UPPER(Nome) AS NomeMaiusculo
FROM TabelaClientes;

-- 2️⃣ Transformando nomes de colaboradores em letras minúsculas
SELECT LOWER(NomeColaborador) AS NomeMinusculo
FROM TabelaColaboradores;

-- 3️⃣ Criando identificadores com partes do nome e CPF
SELECT CONCAT(SUBSTR(Nome, 1, 3), SUBSTRING(CPF, 1, 3)) AS Identificador
FROM TabelaClientes;

-- 4️⃣ Calculando o comprimento de nomes (SQLite)
SELECT Nome, LENGTH(Nome) AS Comprimento
FROM TabelaClientes;

-- 5️⃣ Calculando o comprimento de nomes (PostgreSQL)
SELECT Nome, LENGTH(Nome) AS Comprimento
FROM TabelaClientes;

-- 6️⃣ Calculando o comprimento de nomes (SQL Server)
SELECT Nome, LEN(Nome) AS Comprimento
FROM TabelaClientes;

-- 7️⃣ Unindo nome e cargo na mesma coluna
SELECT NomeColaborador || ' - ' || Cargo AS Nome_Completo_Cargo
FROM TabelaColaboradores;

-- 8️⃣ Substituindo texto em um nome de departamento
SELECT REPLACE(NomeDepartamento, 'Recursos Humanos', 'RH') AS Nome_Atualizado
FROM TabelaDepartamento;

-- 9️⃣ Montando descrição de empréstimos (SQLite)
SELECT CONCAT(TRIM(Tipo), ' - ', Status, ' - $', Valor) AS DescricaoEmprestimo
FROM TabelaEmprestimo;

-- 🔟 Montando descrição de empréstimos (PostgreSQL)
SELECT TRIM(Tipo) || ' - ' || Status || ' - $' || Valor AS DescricaoEmprestimo
FROM TabelaEmprestimo;

-- 11️⃣ Montando descrição de empréstimos (SQL Server)
SELECT LTRIM(RTRIM(Tipo)) + ' - ' + CAST(Status AS NVARCHAR) + ' - $' + CAST(Valor AS NVARCHAR) AS DescricaoEmprestimo
FROM TabelaEmprestimo;

-- 12️⃣ Criando identificadores de pagamento (SQLite)
SELECT id_pagamento,
SUBSTR(Status, 1, 3) || id_pagamento AS IdentificadorPagamento
FROM TabelaPagamentos;

-- 13️⃣ Criando identificadores de pagamento (PostgreSQL)
SELECT id_pagamento,
SUBSTRING(Status FROM 1 FOR 3) || id_pagamento AS IdentificadorPagamento
FROM TabelaPagamentos;

-- 14️⃣ Criando identificadores de pagamento (SQL Server)
SELECT id_pagamento,
SUBSTRING(Status, 1, 3) + id_pagamento AS IdentificadorPagamento
FROM TabelaPagamentos;

-- 15️⃣ Padronizando fonte de score de crédito
SELECT 
    id_score,
    Fonte,
    UPPER(REPLACE(REPLACE(Fonte, 'Boa Vista', 'BOA'), 'Serasa', 'SER')) AS FonteAbreviada
FROM TabelaScoreCredito;

-- 16️⃣ Removendo espaços extras no tipo de empréstimo (SQLite)
SELECT
id_emprestimo,
TRIM(Tipo) AS Tipo
FROM TabelaEmprestimo;

-- 17️⃣ Removendo espaços extras no tipo de empréstimo (PostgreSQL)
SELECT
id_emprestimo,
TRIM(BOTH ' ' FROM Tipo) AS Tipo
FROM TabelaEmprestimo;

-- 18️⃣ Removendo espaços extras no tipo de empréstimo (SQL Server)
SELECT
id_emprestimo,
LTRIM(RTRIM(Tipo)) AS Tipo
FROM TabelaEmprestimo;


📘 Resumo geral:
Neste curso, foram exploradas as principais funções de manipulação de strings nos bancos SQLite, PostgreSQL e SQL Server.
Eu tive a oportunidade de poder praticar sobre:
1) Transformar textos (UPPER, LOWER)
2) Medir comprimentos (LENGTH, LEN)
3) Juntar informações (CONCAT, ||, +)
4) Substituir e limpar valores (REPLACE, TRIM, LTRIM, RTRIM)
5) Extrair partes de texto (SUBSTR, SUBSTRING)
Essas funções são essenciais para padronizar, tratar e formatar textos dentro de consultas SQL.

👨‍💻 Autor: Thiago Pedrazi
📅 Atualizado em: Outubro/2025






























