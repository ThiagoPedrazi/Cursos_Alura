# 🧠 Curso 08 – Praticando SQL: Combinando Dados com JOINs

Neste módulo, você aprende a **relacionar tabelas** para formar resultados mais ricos, usando `INNER JOIN`, `LEFT/RIGHT JOIN` e `FULL JOIN`, além de funções úteis como `COALESCE` e expressões `CASE`.  
Cada exemplo traz o **SQL e a explicação** do que é retornado.

> ⚠️ **Compatibilidade rápida**  
> - **SQLite**: não suporta `RIGHT` nem `FULL` nativamente (use `LEFT` + UNION/CTE como alternativa).  
> - **MySQL**: sem `FULL JOIN` nativo (use `LEFT`/`RIGHT` + `UNION`).  
> - **PostgreSQL / SQL Server**: suportam `INNER/LEFT/RIGHT/FULL`.

---

## 🧩 Consultas e Explicações

```sql
-- 1️⃣ INNER JOIN: apenas linhas com correspondência nas duas tabelas
SELECT c.NomeColaborador, d.NomeDepartamento
FROM TabelaColaboradores c
INNER JOIN TabelaDepartamento d ON c.id_departamento = d.id_departamento;

-- 2️⃣ LEFT JOIN: mantém todos os clientes, mesmo sem telefone
SELECT cl.id_cliente, cl.Nome, t.Telefone
FROM TabelaClientes cl
LEFT JOIN TabelaTelefones t ON cl.id_cliente = t.id_cliente;

-- 3️⃣ RIGHT JOIN: mantém todos os colaboradores, mesmo sem cliente associado
SELECT c.NomeColaborador, cl.Nome AS NomeCliente
FROM TabelaClientes cl
RIGHT JOIN TabelaColaboradores c ON cl.id_colaborador = c.id_colaborador;

-- 4️⃣ FULL JOIN: mostra tudo de ambos os lados (com e sem correspondência)
SELECT cl.Nome AS NomeCliente, e.Tipo AS TipoEmprestimo, e.Valor
FROM TabelaClientes cl
FULL JOIN TabelaEmprestimo e ON cl.id_cliente = e.id_cliente;

-- 5️⃣ Join em cadeia (multi-join): cliente → empréstimo → pagamentos
SELECT 
    cl.Nome AS NomeCliente, 
    e.Tipo AS TipoEmprestimo, 
    e.Valor AS ValorEmprestimo, 
    p.DataPagamento, 
    p.Valor AS ValorPago
FROM TabelaClientes cl
INNER JOIN TabelaEmprestimo e ON cl.id_cliente = e.id_cliente
INNER JOIN TabelaPagamentos p ON e.id_emprestimo = p.id_emprestimo;

-- 6️⃣ JOIN + agregação: total de empréstimos por cliente (apenas quem passou de 10k)
SELECT cl.Nome AS Cliente, SUM(emp.Valor) AS TotalEmprestimos
FROM TabelaClientes cl
JOIN TabelaEmprestimo emp ON cl.id_cliente = emp.id_cliente
GROUP BY cl.Nome
HAVING SUM(emp.Valor) > 10000;

-- 7️⃣ (Apoio) CASE: rotulando status booleano em texto
SELECT 
    Tipo AS TipoEmprestimo,
    Valor,
    CASE 
        WHEN Status THEN 'Ativo'
        ELSE 'Inativo'
    END AS Status
FROM TabelaEmprestimo;

-- 8️⃣ INNER JOIN em cadeia + filtro: trilha do cliente → colaborador → departamento
SELECT 
    cl.Nome AS NomeCliente,
    cl.Cidade,
    col.NomeColaborador,
    dep.NomeDepartamento
FROM TabelaClientes cl
INNER JOIN TabelaColaboradores col ON cl.id_colaborador = col.id_colaborador
INNER JOIN TabelaDepartamento dep ON col.id_departamento = dep.id_departamento
WHERE cl.Cidade = 'São Paulo';

-- 9️⃣ JOIN + subconsulta: empréstimos acima da média geral
SELECT 
    cl.Nome AS NomeCliente, 
    e.Valor AS ValorEmprestimo
FROM TabelaClientes cl
JOIN TabelaEmprestimo e ON cl.id_cliente = e.id_cliente
WHERE e.Valor > (SELECT AVG(Valor) FROM TabelaEmprestimo);

-- 🔟 FULL JOIN + COALESCE: preenchendo valores nulos com rótulos padrão
SELECT 
    COALESCE(c.NomeColaborador, 'Sem Colaborador') AS NomeColaborador,
    COALESCE(d.NomeDepartamento, 'Sem Departamento') AS NomeDepartamento,
    COALESCE(c.EmailColaborador, 'Não informado')   AS Email
FROM TabelaColaboradores c
FULL JOIN TabelaDepartamento d 
  ON c.id_departamento = d.id_departamento;
```

📘 **Resumo geral:**

INNER JOIN: só interseção (linhas com correspondência em ambas as tabelas).

LEFT JOIN / RIGHT JOIN: mantém todos de um lado, preenchendo o outro com NULL quando não há match.

FULL JOIN: retorna tudo de ambos os lados (com e sem match).

JOIN + GROUP BY/HAVING: resumos por grupo com filtros agregados.

JOIN + Subconsulta: comparações poderosas (ex.: acima da média).

Funções de apoio: COALESCE (trata NULL) e CASE (rotula condições).

Essas técnicas permitem criar relatórios ricos e consistentes, cobrindo do relacionamento básico à composição analítica com agregações e subconsultas.







