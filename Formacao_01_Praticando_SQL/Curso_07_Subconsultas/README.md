# 🧠 Curso 07 – Praticando SQL: Entendendo Subconsultas  

Neste módulo foram exploradas as subconsultas (ou subqueries), permitindo que uma consulta SQL dependa do resultado de outra, seja em cláusulas SELECT, WHERE, FROM ou HAVING.
Essas estruturas tornam possível realizar comparações, cálculos e verificações complexas dentro de uma única query.

---

## 🧩 Consultas e Explicações

```sql

-- 1️⃣ Média salarial por departamento
SELECT 
    NomeDepartamento,
    (SELECT AVG(Salario) 
     FROM TabelaColaboradores 
     WHERE TabelaColaboradores.id_departamento = TabelaDepartamento.id_departamento) AS SalarioMedio
FROM TabelaDepartamento;

-- 2️⃣ Clientes com empréstimos acima da média geral
SELECT 
    Nome,
    Valor
FROM TabelaClientes
JOIN TabelaEmprestimo ON TabelaClientes.id_cliente = TabelaEmprestimo.id_cliente
WHERE Valor > (SELECT AVG(Valor) FROM TabelaEmprestimo);

-- 3️⃣ Total de empréstimos ativos por cidade
SELECT 
    Cidade, 
    COUNT(*) AS TotalEmprestimosAtivos
FROM TabelaClientes
JOIN TabelaEmprestimo ON TabelaClientes.id_cliente = TabelaEmprestimo.id_cliente
WHERE Status = 1
GROUP BY Cidade;

-- 4️⃣ Clientes com todos os empréstimos pagos
SELECT 
    Nome, 
    Email, 
    Valor
FROM TabelaClientes
JOIN TabelaEmprestimo ON TabelaClientes.id_cliente = TabelaEmprestimo.id_cliente
WHERE NOT EXISTS (
    SELECT 1 
    FROM TabelaPagamentos 
    WHERE TabelaPagamentos.id_emprestimo = TabelaEmprestimo.id_emprestimo AND Status != 'Pago'
);

-- 5️⃣ Clientes com pontuação de crédito acima da média
SELECT 
    Nome, 
    Pontuacao
FROM TabelaClientes
JOIN TabelaScoreCredito ON TabelaClientes.id_cliente = TabelaScoreCredito.id_cliente
WHERE Pontuacao > (SELECT AVG(Pontuacao) FROM TabelaScoreCredito);

-- 6️⃣ Maior salário por departamento
SELECT 
    NomeDepartamento,
    (SELECT MAX(Salario) 
     FROM TabelaColaboradores 
     WHERE TabelaColaboradores.id_departamento = TabelaDepartamento.id_departamento) AS MaiorSalario
FROM TabelaDepartamento;

-- 7️⃣ Clientes que possuem empréstimos ativos
SELECT 
    Nome
FROM 
    TabelaClientes c
WHERE 
    EXISTS (
        SELECT 1 
        FROM TabelaEmprestimo e 
        WHERE e.id_cliente = c.id_cliente AND e.Status = 1
    );

-- 8️⃣ Média de pagamentos pagos por tipo de empréstimo
SELECT 
    Tipo, 
    (SELECT AVG(Valor) 
     FROM TabelaPagamentos 
     WHERE TabelaPagamentos.id_emprestimo = TabelaEmprestimo.id_emprestimo AND Status = 'Pago') AS MediaPagamentos
FROM TabelaEmprestimo;

-- 9️⃣ Consultando múltiplos campos via subconsultas
SELECT 
    Nome, 
    (SELECT NumeroConta 
     FROM TabelaConta 
     WHERE TabelaConta.id_conta = TabelaClienteConta.id_conta) AS NumeroConta, 
    (SELECT TipoConta 
     FROM TabelaConta 
     WHERE TabelaConta.id_conta = TabelaClienteConta.id_conta) AS TipoConta, 
    (SELECT Saldo 
     FROM TabelaConta 
     WHERE TabelaConta.id_conta = TabelaClienteConta.id_conta) AS Saldo
FROM TabelaClientes
JOIN TabelaClienteConta ON TabelaClientes.id_cliente = TabelaClienteConta.id_cliente;

-- 🔟 Soma total de empréstimos por cidade usando subconsultas aninhadas
SELECT 
    c.Cidade,
    (SELECT SUM(e.Valor) 
     FROM TabelaEmprestimo e 
     WHERE e.id_cliente IN (
         SELECT cl.id_cliente 
         FROM TabelaClientes cl 
         WHERE cl.Cidade = c.Cidade
     )) AS ValorTotalEmprestimos
FROM TabelaClientes c
GROUP BY c.Cidade;
```

📘 **Resumo geral**:
Neste curso foram exploradas as subconsultas (subqueries) em vários contextos:
- Subconsultas no SELECT para cálculos dinâmicos (média, máximo, soma).
- Subconsultas no WHERE para comparações condicionais.
- Uso de EXISTS e NOT EXISTS para verificar a existência (ou ausência) de registros relacionados.
- Subconsultas aninhadas, que permitem cálculos complexos e cruzamentos entre múltiplas tabelas.

Essas técnicas são fundamentais para construir consultas SQL avançadas e flexíveis, capazes de responder perguntas de negócio com mais precisão e organização.

👨‍💻 *Autor:* **Thiago Pedrazi**  
📅 *Atualizado em:* **Outubro/2025**
