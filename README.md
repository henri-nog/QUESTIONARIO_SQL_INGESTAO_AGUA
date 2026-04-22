# 📊 PERGUNTAS SQL - APP DE INGESTÃO DE ÁGUA

Este documento contém 20 perguntas estratégicas para análise de dados do aplicativo.

---

## 👤 Usuários

1. Quantos usuários estão cadastrados no sistema?

```bash
SELECT COUNT(nome) FROM usuarios;
```

<!-- ```bash
``` -->
2. Qual o peso médio dos usuários?
```bash
SELECT SUM(peso)/COUNT(*) AS Peso_Media FROM usuarios;
```
3. Qual usuário possui a maior meta diária?
```bash
SELECT MAX(meta_diaria_ml) AS Maior_Meta_Diaria FROM usuarios;
```
4. Qual usuário possui a menor meta diária?
```bash
SELECT MIN(meta_diaria_ml) AS Maior_Meta_Diaria FROM usuarios;
```
---

## 💧 Consumo de água

5. Qual o total de água ingerido por cada usuário?
```bash
SELECT id, quantidade_ml AS Total_Agua_Por_Usuario FROM ingestao_agua;
```
6. Qual o total de água ingerido em um dia específico?
```bash
SELECT quantidade_ml AS Total_Agua_Por_Usuario FROM ingestao_agua WHERE id = '01cc2a4c-794d-4a98-8e4a-4abe3ee90e97';
```
7. Qual o usuário que mais bebeu água no período?
```bash
SELECT id, quantidade_ml
FROM ingestao_agua
WHERE quantidade_ml = (
    SELECT MAX(quantidade_ml) 
    FROM ingestao_agua
);
```
8. Qual o usuário que menos bebeu água no período?
```bash
SELECT id, quantidade_ml
FROM ingestao_agua
WHERE quantidade_ml = (
    SELECT MIN(quantidade_ml) 
    FROM ingestao_agua
);
```
9. Qual o consumo médio diário por usuário?
```bash
SELECT SUM(quantidade_ml)/COUNT(*) AS Consumo_Medio FROM ingestao_agua;
```
10. Qual o consumo médio por ingestão (copo)?
```bash
SELECT SUM(meta_ml)/COUNT(*) AS Media_Por_Ingestao_Copo FROM metas_diarias;
```
---

## 📅 Análise por dia

11. Quanto cada usuário bebeu por dia?
```bash
SELECT usuario_id, total_ml AS Usuario_Bebida_Por_Dia FROM resumo_diario_agua;
```
12. Qual foi o dia com maior consumo total de água?
```bash
SELECT data, total_ml 
FROM resumo_diario_agua 
WHERE total_ml = (
  SELECT MAX(total_ml)
  FROM resumo_diario_agua
);
```
13. Qual foi o dia com menor consumo total?
```bash
SELECT data, total_ml 
FROM resumo_diario_agua 
WHERE total_ml = (
  SELECT MIN(total_ml)
  FROM resumo_diario_agua
);
```
14. Quantos registros de ingestão existem por dia?
```bash
SELECT COUNT(usuario_id) AS Numero_Registros FROM resumo_diario_agua;
```
---

## 🎯 Metas

15. Qual usuário atingiu a meta diária em cada dia?
```bash
SELECT id, meta_ml FROM metas_diarias;
```
16. Quantos dias cada usuário bateu a meta?
```bash
SELECT id, meta_ml, data FROM metas_diarias;
```
17. Qual a porcentagem da meta atingida por dia por usuário?

18. Qual usuário tem melhor desempenho (mais dias com meta atingida)?
```bash
SELECT id, meta_ml 
FROM metas_diarias
WHERE meta_ml = (
  SELECT MAX(meta_ml)
  FROM metas_diarias
);
```
---

## 🧠 Inteligência / Produto

19. Em quais horários ocorre maior consumo de água?
```bash
SELECT MAX(quantidade_ml) AS Minimo_Consumo FROM ingestao_agua;

SELECT DISTINCT quantidade_ml, data_hora FROM ingestao_agua
WHERE quantidade_ml >= 400;
```
20. Qual o intervalo médio entre ingestões por usuário?