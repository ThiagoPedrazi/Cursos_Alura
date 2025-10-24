# 🧠 Curso 06 – Praticando SQL: Funções de Agregação  

Neste módulo, eu tive a oportunidade de poder praticar sobre **resumir e consolidar informações numéricas** em consultas SQL usando funções como `SUM`, `AVG`, `MIN`, `MAX` e `COUNT`.  
Essas funções são fundamentais para gerar relatórios e análises de desempenho.

---

## 🧩 Consultas e Explicações

```sql
-- 1️⃣ Calculando o valor total de empréstimos
SELECT SUM(Valor) AS TotalEmprestimos
FROM TabelaEmprestimo;

-- 2️⃣ Calculando a média salarial dos colaboradores
SELECT AVG(Salario) AS MediaSalarial
FROM TabelaColaboradores;

-- 3️⃣ Identificando o maior valor de empréstimo
SELECT MAX(Valor) AS MaiorEmprestimo
FROM TabelaEmprestimo;

-- 4️⃣ Identificando o menor valor de empréstimo
SELECT MIN(Valor) AS MenorEmprestimo
FROM TabelaEmprestimo;

-- 5️⃣ Contando o número total de colaboradores
SELECT COUNT(*) AS TotalColaboradores
FROM TabelaColaboradores;

-- 6️⃣ Calculando a média dos empréstimos sem usar AVG()
SELECT SUM(Valor) / COUNT(*) AS MediaEmprestimos
FROM TabelaEmprestimo;

-- 7️⃣ Agrupando salários por departamento
SELECT id_departamento, SUM(Salario) AS TotalSalarios
FROM TabelaColaboradores
GROUP BY id_departamento;

-- 8️⃣ Exibindo tipos de empréstimos com valor total acima de 20.000
SELECT Tipo, SUM(Valor) AS TotalPorTipo
FROM TabelaEmprestimo
GROUP BY Tipo
HAVING SUM(Valor) > 20000;

-- 9️⃣ Resumo com total e quantidade de empréstimos por tipo
SELECT Tipo, SUM(Valor) AS TotalValor, COUNT(*) AS QuantidadeEmprestimos
FROM TabelaEmprestimo
GROUP BY Tipo;

-- 🔟 Consolidando múltiplas métricas em uma única consulta
SELECT 
    SUM(Valor) AS TotalEmprestimos,
    AVG(Valor) AS MediaEmprestimos,
    MAX(Valor) AS MaiorEmprestimo,
    MIN(Valor) AS MenorEmprestimo
FROM TabelaEmprestimo;
```

📘 **Resumo geral** 
Neste curso, foram aplicadas as principais funções de agregação do SQL:
- SUM() -> Soma os valores de uma coluna numérica
- AVG() -> Calcula a média aritmética
- MIN() -> Retorna o menor valor
- MAX() ->	Retorna o maior valor
- COUNT() -> Conta o número de registros
- GROUP BY -> Agrupa dados por uma ou mais colunas
- HAVING -> Filtra resultados após o agrupamento

Essas funções são amplamente usadas em dashboards, relatórios financeiros e análises de indicadores.

👨‍💻 *Autor:* **Thiago Pedrazi**  
📅 *Atualizado em:* **Outubro/2025**
