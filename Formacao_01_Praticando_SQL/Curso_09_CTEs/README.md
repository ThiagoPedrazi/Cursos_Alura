# 🧠 Curso 09 – Formação Praticando SQL: Common Table Expressions (CTEs)

Neste módulo, estudei sobre como utilizar **CTEs (Common Table Expressions)**, que permitem criar blocos de consulta temporários e nomeados para melhorar a **clareza, modularidade e reuso** do código SQL.  
A cláusula `WITH` ajuda a dividir consultas complexas em partes mais legíveis e organizadas.

---

## 🧩 Consultas e Explicações

```sql
-- 1️⃣ CTE simples: empréstimos com status pendente
WITH EmprestimosPendentes AS (
    SELECT Valor
    FROM TabelaEmprestimo
    WHERE Status = 0
)
SELECT SUM(Valor) AS TotalEmprestimosPendentes
FROM EmprestimosPendentes;

-- 2️⃣ CTE com filtro e junção: clientes com bom crédito
WITH ClientesBomCredito AS (
    SELECT sc.id_cliente, cl.Nome, sc.Pontuacao
    FROM TabelaScoreCredito sc
    JOIN TabelaClientes cl ON sc.id_cliente = cl.id_cliente
    WHERE sc.Pontuacao > 700
)
SELECT id_cliente, Nome, Pontuacao
FROM ClientesBomCredito;

-- 3️⃣ CTE com agregação: total de salários por departamento
WITH SalariosPorDepartamento AS (
    SELECT id_departamento, SUM(Salario) AS TotalSalarios
    FROM TabelaColaboradores
    GROUP BY id_departamento
)
SELECT id_departamento, TotalSalarios
FROM SalariosPorDepartamento;

-- 4️⃣ CTE com contagem: clientes agrupados por estado
WITH ClientesPorEstado AS (
    SELECT Estado, COUNT(*) AS QuantidadeClientes
    FROM TabelaClientes
    GROUP BY Estado
)
SELECT Estado, QuantidadeClientes
FROM ClientesPorEstado;

-- 5️⃣ Duas CTEs encadeadas: média de idade e clientes abaixo da média
WITH IdadesClientes AS (
    SELECT Nome, strftime('%Y', 'now') - strftime('%Y', DataNascimento) AS Idade
    FROM TabelaClientes
),
MediaIdade AS (
    SELECT AVG(Idade) AS IdadeMedia
    FROM IdadesClientes
)
SELECT ic.Nome, ic.Idade
FROM IdadesClientes ic
CROSS JOIN MediaIdade mi
WHERE ic.Idade < mi.IdadeMedia;

-- 6️⃣ CTE aninhada: clientes com múltiplas contas e seus empréstimos
WITH ClientesMultiplasContas AS (
    SELECT id_cliente
    FROM TabelaClienteConta
    GROUP BY id_cliente
    HAVING COUNT(id_conta) > 1
),
EmprestimosClientesMultiplasContas AS (
    SELECT e.id_emprestimo, e.id_cliente, e.Valor
    FROM TabelaEmprestimo e
    WHERE e.id_cliente IN (SELECT id_cliente FROM ClientesMultiplasContas)
)
SELECT id_emprestimo, id_cliente, Valor
FROM EmprestimosClientesMultiplasContas;

-- 7️⃣ CTE filtrando resultados agregados: pagamentos altos
WITH PagamentosPorEmprestimo AS (
    SELECT id_emprestimo, SUM(Valor) AS TotalPagamentos
    FROM TabelaPagamentos
    GROUP BY id_emprestimo
),
EmprestimosComPagamentosAltos AS (
    SELECT id_emprestimo, TotalPagamentos
    FROM PagamentosPorEmprestimo
    WHERE TotalPagamentos >= 1000
)
SELECT ep.id_emprestimo, ep.TotalPagamentos
FROM EmprestimosComPagamentosAltos ep;

-- 8️⃣ CTE para médias e filtros: departamentos com média salarial alta
WITH MediaSalariosPorDepartamento AS (
    SELECT id_departamento, AVG(Salario) AS MediaSalarial
    FROM TabelaColaboradores
    GROUP BY id_departamento
),
DepartamentosComSalarioAlto AS (
    SELECT id_departamento, MediaSalarial
    FROM MediaSalariosPorDepartamento
    WHERE MediaSalarial > 4500
)
SELECT id_departamento, MediaSalarial
FROM DepartamentosComSalarioAlto;

-- 9️⃣ Duas CTEs cruzadas: clientes com empréstimos pendentes e crédito baixo
WITH ClientesComEmprestimosPendentes AS (
    SELECT id_cliente
    FROM TabelaEmprestimo
    WHERE Status = 0
),
ClientesComCreditoBaixo AS (
    SELECT id_cliente
    FROM TabelaScoreCredito
    WHERE Pontuacao < 500
)
SELECT cl.Nome
FROM ClientesComEmprestimosPendentes ce
JOIN ClientesComCreditoBaixo cb ON ce.id_cliente = cb.id_cliente
JOIN TabelaClientes cl ON ce.id_cliente = cl.id_cliente;

-- 🔟 CTE final com cálculos compostos: contas recentes e saldo médio
WITH ContasAbertasRecentes AS (
    SELECT id_conta, Saldo
    FROM TabelaConta
    WHERE DataAbertura > '2023-01-01'
),
SaldoMedio AS (
    SELECT AVG(Saldo) AS MediaSaldo
    FROM ContasAbertasRecentes
)
SELECT COUNT(*) AS TotalContas, (SELECT MediaSaldo FROM SaldoMedio) AS MediaSaldo
FROM ContasAbertasRecentes;
```

📘 **Resumo geral**

As CTEs (WITH ... AS) são ideais para:
- Organizar consultas complexas sem criar tabelas temporárias permanentes.
- Reutilizar blocos dentro da mesma query.
- Melhorar legibilidade e manutenção de código SQL.

Tipos comuns:
- CTE simples (única)
- CTEs encadeadas (múltiplas)
- CTEs recursivas (para hierarquias — vistas em módulos avançados)

👨‍💻 *Autor:* **Thiago Pedrazi**  
📅 *Atualizado em:* **Outubro/2025**
