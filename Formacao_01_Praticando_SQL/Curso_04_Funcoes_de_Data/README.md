# 🧠 Curso 04 – Praticando SQL: Funções de Data  

Neste módulo, eu tive a oportunidade de poder praticar sobre manipulação e formatação de datas utilizando funções nativas de bancos de dados.  
O foco está em comparar, calcular e transformar datas em **SQLite**, **PostgreSQL** e **SQL Server**.  
Cada exemplo inclui o código SQL e um resumo explicativo.

---

## 🧩 Consultas e Explicações

```sql
-- 1️⃣ Obtendo a data e hora atuais
-- SQLite
SELECT CURRENT_TIMESTAMP AS DataHoraAtual;

-- PostgreSQL
SELECT NOW() AS DataHoraAtual;

-- SQL Server
SELECT GETDATE() AS DataHoraAtual;

-- 2️⃣ Formatando a data de nascimento no formato YYYY-MM-DD
-- SQLite
SELECT Nome, STRFTIME('%Y-%m-%d', DataNascimento) AS DataFormatada 
FROM TabelaClientes;

-- PostgreSQL
SELECT Nome, TO_CHAR(DataNascimento, 'YYYY-MM-DD') AS DataFormatada 
FROM TabelaClientes;

-- SQL Server
SELECT Nome, FORMAT(DataNascimento, 'yyyy-MM-dd') AS DataFormatada 
FROM TabelaClientes;

-- 3️⃣ Calculando a quantidade total de dias de um empréstimo
-- SQLite
SELECT id_emprestimo, 
       JULIANDAY(DATE(DataInicio, '+' || Prazo || ' days')) - JULIANDAY(DataInicio) AS DiasTotais
FROM TabelaEmprestimo;

-- PostgreSQL
SELECT id_emprestimo, 
       (DataInicio + INTERVAL '1 day' * Prazo - DataInicio)::INT AS DiasTotais
FROM TabelaEmprestimo;

-- SQL Server
SELECT id_emprestimo, 
       DATEDIFF(DAY, DataInicio, DATEADD(DAY, Prazo, DataInicio)) AS DiasTotais
FROM TabelaEmprestimo;

-- 4️⃣ Extraindo apenas o ano de nascimento dos clientes
-- SQLite
SELECT Nome, STRFTIME('%Y', DataNascimento) AS AnoNascimento 
FROM TabelaClientes;

-- PostgreSQL
SELECT Nome, EXTRACT(YEAR FROM DataNascimento) AS AnoNascimento 
FROM TabelaClientes;

-- SQL Server
SELECT Nome, YEAR(DataNascimento) AS AnoNascimento 
FROM TabelaClientes;

-- 5️⃣ Selecionando empréstimos realizados entre janeiro e março de 2023
-- SQLite / PostgreSQL / SQL Server
SELECT * 
FROM TabelaEmprestimo 
WHERE DataInicio BETWEEN '2023-01-01' AND '2023-03-31';

-- 6️⃣ Calculando a data de vencimento de um empréstimo
-- SQLite
SELECT id_emprestimo, 
       DataInicio, 
       DATE(DataInicio, '+' || Prazo || ' days') AS DataVencimento 
FROM TabelaEmprestimo;

-- PostgreSQL
SELECT id_emprestimo, 
       DataInicio, 
       DataInicio + INTERVAL '1 day' * Prazo AS DataVencimento 
FROM TabelaEmprestimo;

-- SQL Server
SELECT id_emprestimo, 
       DataInicio, 
       DATEADD(DAY, Prazo, DataInicio) AS DataVencimento 
FROM TabelaEmprestimo;

-- 7️⃣ Ordenando pagamentos pela data mais antiga para a mais recente
-- SQLite / PostgreSQL / SQL Server
SELECT * 
FROM TabelaPagamentos 
ORDER BY DataPagamento ASC;

-- 8️⃣ Calculando a idade dos clientes
-- SQLite
SELECT Nome, 
       (strftime('%Y', 'now') - strftime('%Y', DataNascimento)) - 
       (strftime('%m', 'now') < strftime('%m', DataNascimento)) AS Idade
FROM TabelaClientes;

-- PostgreSQL
SELECT Nome, 
       EXTRACT(YEAR FROM AGE(CURRENT_DATE, DataNascimento)) AS Idade
FROM TabelaClientes;

-- SQL Server
SELECT Nome, 
       DATEDIFF(YEAR, DataNascimento, GETDATE()) - 
       CASE 
           WHEN MONTH(DataNascimento) > MONTH(GETDATE()) OR 
                (MONTH(DataNascimento) = MONTH(GETDATE()) AND DAY(DataNascimento) > DAY(GETDATE())) 
           THEN 1 
           ELSE 0 
       END AS Idade
FROM TabelaClientes;

-- 9️⃣ Verificando se um empréstimo está vencido ou no prazo
-- SQLite
SELECT id_emprestimo, 
       CASE 
           WHEN JULIANDAY(DATE(DataInicio, '+' || Prazo || ' days')) < JULIANDAY('now') THEN 'Vencido'
           ELSE 'No Prazo'
       END AS StatusEmprestimo
FROM TabelaEmprestimo;

-- PostgreSQL
SELECT id_emprestimo, 
       CASE 
           WHEN CURRENT_DATE > DataInicio + INTERVAL '1 day' * Prazo THEN 'Vencido'
           ELSE 'No Prazo'
       END AS StatusEmprestimo 
FROM TabelaEmprestimo;

-- SQL Server
SELECT id_emprestimo, 
       CASE 
           WHEN DATEDIFF(DAY, DATEADD(DAY, Prazo, DataInicio), GETDATE()) > 0 THEN 'Vencido'
           ELSE 'No Prazo'
       END AS StatusEmprestimo
FROM TabelaEmprestimo;

-- 🔟 Calculando a data do próximo pagamento (30 dias após o início)
-- SQLite
SELECT id_emprestimo, 
       datainicio, 
       DATE(datainicio, '+30 days') AS ProximoPagamento
FROM TabelaEmprestimo;

-- PostgreSQL
SELECT id_emprestimo, 
       DataInicio, 
       DataInicio + INTERVAL '30 days' AS ProximoPagamento
FROM TabelaEmprestimo;

-- SQL Server
SELECT id_emprestimo, 
       DataInicio, 
       DATEADD(DAY, 30, DataInicio) AS ProximoPagamento
FROM TabelaEmprestimo;
```


📘 **Resumo geral:**
Neste curso, foram exploradas as principais funções de manipulação de datas nos bancos SQLite, PostgreSQL e SQL Server, abordando:
1) Obtenção da data/hora atual (NOW, CURRENT_TIMESTAMP, GETDATE)
2) Formatação e conversão de datas (STRFTIME, TO_CHAR, FORMAT)
3) Cálculos de diferença e intervalos (DATEDIFF, JULIANDAY, INTERVAL)
4) Extração de partes específicas (YEAR, EXTRACT)
5) Lógica condicional para status e vencimento (CASE WHEN)

Essas funções são fundamentais para relatórios temporais, análises de desempenho e controles financeiros baseados em períodos.

👨‍💻 Autor: Thiago Pedrazi
📅 Atualizado em: Outubro/2025
