# 🧠 Curso 01 – Formação Praticando SQL: Realizando Consultas  

Este módulo apresenta os conceitos fundamentais de **consultas SQL**, utilizando as cláusulas **SELECT**, **FROM**, **WHERE**, **ORDER BY** e **LIMIT**.  
Esses comandos formam a base de qualquer análise de dados em bancos relacionais.  
Cada exemplo abaixo mostra o código SQL e uma breve explicação.

---

## 🧩 Consultas e Explicações

```sql
-- 1️⃣ Exibindo todos os registros da tabela de clientes
SELECT * 
FROM TabelaClientes;

-- 2️⃣ Exibindo apenas o nome e o cargo dos colaboradores
SELECT NomeColaborador, Cargo
FROM TabelaColaboradores;

-- 3️⃣ Exibindo apenas empréstimos ativos (status verdadeiro)
SELECT * 
FROM TabelaEmprestimo
WHERE Status = TRUE;

-- 4️⃣ Exibindo clientes que moram no estado de São Paulo
SELECT Nome, Estado 
FROM TabelaClientes
WHERE Estado = 'SP';

-- 5️⃣ Exibindo colaboradores com salário acima de R$5000
SELECT NomeColaborador, Salario 
FROM TabelaColaboradores
WHERE Salario > 5000;

-- 6️⃣ Exibindo empréstimos com valor igual ou superior a 10.000
SELECT * 
FROM TabelaEmprestimo
WHERE Valor >= 10000;

-- 7️⃣ Ordenando colaboradores em ordem alfabética
SELECT NomeColaborador, Cargo 
FROM TabelaColaboradores
ORDER BY NomeColaborador;

-- 8️⃣ Exibindo apenas os 5 primeiros registros de colaboradores
SELECT * 
FROM TabelaColaboradores
LIMIT 5;

-- 9️⃣ Listando empréstimos do maior para o menor valor
SELECT * 
FROM TabelaEmprestimo
ORDER BY Valor DESC;

-- 🔟 Exibindo os 2 colaboradores com maiores salários
SELECT * 
FROM TabelaColaboradores
WHERE Salario >= 5000
ORDER BY id_colaborador DESC
LIMIT 2;
```

📘 **Resumo geral**

Neste curso, eu estudei as principais cláusulas do SQL:
- SELECT / FROM → escolher tabelas e colunas.
- WHERE → filtrar registros com base em condições.
- ORDER BY → ordenar resultados.
- LIMIT → restringir a quantidade de linhas retornadas.

Esses são os fundamentos essenciais de qualquer consulta SQL.

👨‍💻 *Autor:* **Thiago Pedrazi**  
📅 *Atualizado em:* **Outubro/2025**
