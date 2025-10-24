# 🧠 Curso 02 – Formação Praticando SQL: Operadores Lógicos  

Neste módulo, eu tive a oportunidade de poder praticar sobre o uso dos **operadores lógicos e de filtragem** nas consultas SQL, como **AND**, **OR**, **NOT**, **IN**, **BETWEEN**, **LIKE** e **DISTINCT**, fundamentais para criar consultas mais precisas e eficientes.  
Cada exemplo abaixo apresenta o código SQL e um resumo explicativo.

---

## 🧩 Consultas e Explicações

```sql
-- 1️⃣ Funcionários com salário acima de R$4500 e do departamento D03
SELECT NomeColaborador, Salario, id_departamento
FROM TabelaColaboradores
WHERE Salario > 4500 AND id_departamento = 'D03';

-- 2️⃣ Clientes nascidos antes de 1990 ou residentes em SP
SELECT Nome, DataNascimento, Estado
FROM TabelaClientes
WHERE DataNascimento < '1990-01-01' OR Estado = 'SP';

-- 3️⃣ Empréstimos realizados entre janeiro e março de 2023
SELECT id_emprestimo, DataInicio, Tipo, Valor
FROM TabelaEmprestimo
WHERE DataInicio BETWEEN '2023-01-01' AND '2023-03-31';

-- 4️⃣ Clientes maiores de idade
SELECT Nome, DataNascimento, CPF
FROM TabelaClientes
WHERE NOT (YEAR(CURDATE()) - YEAR(DataNascimento) < 18);

-- 5️⃣ Empréstimos do tipo Pessoal ou Imobiliário
SELECT id_emprestimo, Tipo, Valor
FROM TabelaEmprestimo
WHERE Tipo IN ('Pessoal', 'Imobiliário');

-- 6️⃣ Empréstimos entre 10 mil e 50 mil dos tipos Consignado ou Automóvel
SELECT id_emprestimo, Tipo, Valor
FROM TabelaEmprestimo
WHERE Valor BETWEEN 10000 AND 50000 AND Tipo IN ('Consignado', 'Automóvel');

-- 7️⃣ Listando estados únicos da tabela de clientes
SELECT DISTINCT Estado
FROM TabelaClientes;

-- 8️⃣ Clientes de RJ ou Salvador com CPF iniciando em 6
SELECT Nome, CPF, Cidade, Estado
FROM TabelaClientes
WHERE (Cidade = 'Rio de Janeiro' OR Cidade = 'Salvador') AND CPF LIKE '6%';

-- 9️⃣ Pagamentos entre R$500 e R$1000 realizados em 2023
SELECT id_pagamento, DataPagamento, Valor, Status
FROM TabelaPagamentos
WHERE DataPagamento BETWEEN '2023-01-01' AND '2023-12-31'
  AND Valor BETWEEN 500 AND 1000;

-- 🔟 Clientes com pontuação menor ou igual a 700
SELECT id_cliente, Pontuacao, Fonte
FROM TabelaScoreCredito
WHERE NOT (Pontuacao > 700);
```

📘 **Resumo geral:**
Neste curso, foram aplicadas diversas técnicas de filtragem usando operadores lógicos (AND, OR, NOT), listas (IN), intervalos (BETWEEN) e buscas por padrão (LIKE), além da eliminação de duplicidades com DISTINCT.

Esses recursos formam a base para consultas SQL robustas e expressivas em bancos relacionais.

👨‍💻 *Autor:* **Thiago Pedrazi**  
📅 *Atualizado em:* **Outubro/2025**
