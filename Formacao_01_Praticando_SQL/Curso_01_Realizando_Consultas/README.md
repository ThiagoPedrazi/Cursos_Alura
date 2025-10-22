# 🧠 Curso 01 – Praticando SQL: Realizando Consultas  

Este módulo apresenta consultas SQL fundamentais utilizando as cláusulas **SELECT**, **WHERE**, **AND**, **OR**, **IN**, **BETWEEN**, **LIKE**, **NOT** e **DISTINCT**.  
Cada exemplo abaixo contém um trecho de código SQL e um breve resumo explicativo sobre sua função.

---

## 🟩 1. Selecionando funcionários com salário acima de R$4500 e do departamento D03
```sql
SELECT NomeColaborador, Salario, id_departamento
FROM TabelaColaboradores
WHERE Salario > 4500 AND id_departamento = 'D03';

SELECT Nome, DataNascimento, Estado
FROM TabelaClientes
WHERE DataNascimento < '1990-01-01' OR Estado = 'SP';

