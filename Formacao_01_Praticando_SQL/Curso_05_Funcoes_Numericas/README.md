# 🧠 Curso 05 – Praticando SQL: Funções Numéricas  

Neste módulo, eu tive a oportunidade de poder praticar sobre **operações matemáticas e cálculos numéricos em SQL**, aplicando funções como `ROUND`, `CEIL`, `FLOOR`, `ABS`, `POWER` e `SQRT`.  
Essas funções são fundamentais para análises financeiras, cálculos de lucros, arredondamentos e projeções de crescimento.

---

## 🧩 Consultas e Explicações

```sql
-- 1️⃣ Calculando receitas e despesas mensais
SELECT Mes, 
       Ano,
       (Quantidade * PrecoUnitario) AS Receitas,
       (Quantidade * CustoUnitario) AS Despesas
FROM TabelaVendasMensais;

-- 2️⃣ Calculando o lucro bruto
SELECT Mes, 
       Ano,
       (Quantidade * PrecoUnitario) - (Quantidade * CustoUnitario) AS LucroBruto
FROM TabelaVendasMensais;

-- 3️⃣ Calculando a margem de lucro bruto (%)
SELECT Mes, 
       Ano,
       ROUND(100.0 * ((Quantidade * PrecoUnitario) - (Quantidade * CustoUnitario)) / 
             (Quantidade * PrecoUnitario), 1) AS MargemLucroBruto
FROM TabelaVendasMensais;

-- 4️⃣ Calculando o lucro líquido com dedução de 30% de impostos
SELECT Mes, 
       Ano,
       ROUND((Quantidade * PrecoUnitario) - (Quantidade * CustoUnitario) - (Quantidade * CustoUnitario) * 0.30, 2) AS LucroLiquido
FROM TabelaVendasMensais;

-- 5️⃣ Convertendo a quantidade vendida em número de caixas (arredondando para cima)
SELECT id_pedido,
       QuantidadeVendida,
       CEIL(QuantidadeVendida / 8.0) AS QtdCaixas
FROM TabelaPedidos;

-- 6️⃣ Calculando o preço total com desconto e arredondamento para baixo
SELECT id_pedido,
       QuantidadeVendida,
       PrecoUnitario,
       Desconto,
       FLOOR((PrecoUnitario * QuantidadeVendida) * (1 - Desconto)) AS PrecoTotal
FROM TabelaPedidos;

-- 7️⃣ Comparando vendas com a média histórica (diferença absoluta)
SELECT Mes,
       Ano,
       ABS(VendasMensais - MediaVendas5Anos) AS DiferencaAbsolutaVendas
FROM TabelaMetasVendasMensais;

-- 8️⃣ Projetando vendas para 5 anos à frente com taxa de crescimento
SELECT Ano,
       VendasBase,
       FLOOR(POWER(1 + TaxaCrescimento, 5) * VendasBase) AS VendasProjecao5Anos
FROM TabelaEstimativaCrescimento;

-- 9️⃣ Calculando distância entre cidades e status de entrega
SELECT id_pedido,
       CidadeCliente,
       ROUND(SQRT(POWER(Latitude - (-23.588161), 2) + POWER(Longitude - (-46.632344), 2)) * 111.19, 1) AS Distancia,
       CASE 
           WHEN ROUND(SQRT(POWER(Latitude - (-23.588161), 2) + POWER(Longitude - (-46.632344), 2)) * 111.19, 1) < 60 
           THEN 'Entrega gratuita'
           ELSE 'Cobrar entrega'
       END AS StatusEntrega
FROM TabelaPedidos;

-- 🔟 Calculando o custo de frete com base na distância e na quantidade vendida
SELECT id_pedido,
       CidadeCliente,
       ROUND(SQRT(POWER(Latitude - (-23.588161), 2) + POWER(Longitude - (-46.632344), 2)) * 111.19, 1) AS Distancia,
       CASE 
           WHEN ROUND(SQRT(POWER(Latitude - (-23.588161), 2) + POWER(Longitude - (-46.632344), 2)) * 111.19, 1) < 60 
           THEN 0
           ELSE CEIL(QuantidadeVendida / 8.0) * 50
       END AS Frete
FROM TabelaPedidos;
```


📘 **Resumo geral:**
Neste curso, foram exploradas as principais funções numéricas do SQL, aplicáveis em análises financeiras, operacionais e logísticas:
1) Operações aritméticas básicas (+, -, *, /);
2) Arredondamentos (ROUND, CEIL, FLOOR);
3) Cálculos absolutos (ABS);
4) Potências e raízes (POWER, SQRT);
5) Simulações financeiras e de distância com CASE WHEN.

Essas funções são amplamente utilizadas em relatórios de vendas, projeções e métricas de desempenho.

👨‍💻 *Autor:* **Thiago Pedrazi**
📅 *Atualizado em:* **Outubro/2025**
