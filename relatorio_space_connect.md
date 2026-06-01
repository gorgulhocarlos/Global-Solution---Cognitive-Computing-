# 🛰️ SPACE CONNECT
## Previsão de Risco de Desastres Naturais com Dados de Satélite
### Relatório Técnico — Cognitive Computing, Computer Vision and IoT Systems

**Prof.:** Arnaldo Viana | **FIAP 2026**

---

## 1. Problema

Desastres naturais como secas severas, incêndios florestais e inundações causam, em média, **R$ 10 bilhões em prejuízos anuais no Brasil** e afetam milhões de pessoas. A identificação precoce de regiões em risco é um dos maiores desafios da gestão de desastres.

Satélites de observação da Terra coletam continuamente dados críticos:
- **NDVI** (Normalized Difference Vegetation Index) — índice de saúde da vegetação
- **LST** (Land Surface Temperature) — temperatura da superfície terrestre
- **Focos de calor** — detecção de incêndios em tempo quase real
- **Dados pluviométricos** e anomalias climáticas

**Pergunta central:** *Como usar esses dados de satélite para prever o nível de risco de desastre por região com antecedência suficiente para ações preventivas?*

---

## 2. Metodologia

### 2.1 Base de Dados

Dataset sintético gerado com base em padrões reais de sensoriamento remoto, inspirado nas seguintes fontes públicas:

| Fonte | Dados |
|---|---|
| [INPE — Queimadas](https://queimadas.dgi.inpe.br) | Focos de calor por bioma |
| [NASA MODIS](https://modis.gsfc.nasa.gov) | NDVI, temperatura superficial |
| [NOAA Climate](https://www.ncdc.noaa.gov) | Precipitação, umidade, anomalias |

**Estrutura:** 1.200 registros × 11 variáveis, cobrindo 6 biomas brasileiros (Amazônia, Cerrado, Pantanal, Caatinga, Mata Atlântica, Pampa).

### 2.2 Variáveis

| Feature | Tipo | Descrição |
|---|---|---|
| `temperatura_media_C` | Numérica | Temperatura média mensal (°C) |
| `anomalia_temperatura_C` | Numérica | Desvio em relação à média histórica |
| `precipitacao_mm` | Numérica | Precipitação acumulada no mês (mm) |
| `umidade_relativa_pct` | Numérica | Umidade relativa do ar (%) |
| `ndvi_satelite` | Numérica | Índice de Vegetação (0–1, via satélite) |
| `cobertura_nuvens_pct` | Numérica | Cobertura de nuvens (%, satélite) |
| `indice_seca` | Numérica | Índice de Seca (Palmer simplificado) |
| `focos_queimadas_satelite` | Numérica | Focos de calor detectados (satélite) |
| `regiao` | Categórica | Bioma/região geográfica |
| `mes` | Numérica | Mês do ano (codificado ciclicamente) |
| `risco_desastre` | **Target** | 0=Baixo, 1=Médio, 2=Alto |

### 2.3 Pré-processamento

- Label Encoding para variável `regiao`
- Encoding cíclico do mês: `sin(2π·mês/12)` e `cos(2π·mês/12)` (preserva ciclicidade)
- Divisão treino/teste: 80%/20%, estratificada por classe
- Validação cruzada: **StratifiedKFold (5 folds)**

### 2.4 Modelos Treinados

| Modelo | Justificativa |
|---|---|
| Decision Tree | Baseline interpretável |
| **Random Forest** | Ensemble robusto, lida bem com dados mistos |
| Gradient Boosting | Boosting sequencial, excelente em dados tabulares |

---

## 3. Resultados

### 3.1 Comparação de Modelos

| Modelo | Acurácia | F1-Score (Weighted) | CV F1 (5-fold) |
|---|---|---|---|
| Decision Tree | 88,3% | 0.882 | 0.870 ± 0.019 |
| **Random Forest** | **91,2%** | **0.912** | **0.897 ± 0.025** |
| Gradient Boosting | 89,6% | 0.894 | 0.899 ± 0.015 |

### 3.2 Melhor Modelo: Random Forest

```
              precision    recall  f1-score   support

       Baixo       0.95      0.97      0.96       181
       Médio       0.70      0.72      0.71        36
        Alto       0.95      0.78      0.86        23

    accuracy                           0.91       240
   macro avg       0.87      0.82      0.84       240
weighted avg       0.91      0.91      0.91       240
```

### 3.3 Features Mais Importantes

As 3 variáveis mais relevantes para a predição foram:
1. **NDVI (Satélite)** — estado de saúde da vegetação
2. **Índice de Seca** — acumulado de déficit hídrico
3. **Focos de Queimadas (Satélite)** — detecção direta de incêndios

Todas as três são derivadas diretamente de sensores espaciais, validando a premissa do projeto.

---

## 4. Conclusão

A solução demonstrou que **dados de satélite, combinados com algoritmos de Machine Learning, podem prever o risco de desastres naturais com 91% de acurácia**. O modelo Random Forest apresentou o melhor equilíbrio entre precisão e generalização.

### Conexão com Space Connect

Esta solução integra **tecnologia espacial** (satélites de observação) com **inteligência artificial** para impactar diretamente a segurança de populações em solo. Satélites como o CBERS-4A (brasileiro), Landsat 8/9 (NASA) e Sentinel-2 (ESA) já fornecem os dados necessários de forma gratuita.

### Trabalhos Futuros

- Integração com dados reais via API da NASA / INPE
- Incorporar imagens de satélite para Visão Computacional (detecção de queimadas via NDVI)
- Modelo de séries temporais (LSTM) para prever tendências mensais
- Dashboard em tempo real com alertas automáticos

---

*Disciplina: Cognitive Computing, Computer Vision and IoT Systems — FIAP 2026*
