# 🧠 Curso 04 – Praticando SQL: Funções de Data  

Neste módulo, eu tive a oportunidade de aprender sobre manipulação e formatação de datas utilizando funções nativas de bancos de dados.  
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
