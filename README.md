# Global-Solution---Cognitive-Computing-

Integrantes: 
Felipe Cardoso Scalesse Ferreira RM99062 
Carlos Augusto Gorgulho RM98456 
Pablo Rangel RM551548

# 🛰️ SPACE CONNECT — Previsão de Risco de Desastres com Dados de Satélite

> **Disciplina:** Cognitive Computing, Computer Vision and IoT Systems — FIAP 2026  
> **Prof.:** Arnaldo Viana

## Sobre o Projeto

Utilizamos dados de sensoriamento remoto por satélite (NDVI, temperatura, precipitação, focos de calor) para treinar modelos de Machine Learning capazes de prever o **nível de risco de desastre natural** (Baixo / Médio / Alto) em biomas brasileiros.

## Resultados

| Modelo | Acurácia | F1-Score |
|---|---|---|
| Decision Tree | 88.3% | 0.882 |
| **Random Forest** ⭐ | **91.2%** | **0.912** |
| Gradient Boosting | 89.6% | 0.894 |

## Estrutura

```
space_connect/
├── notebook_space_connect.ipynb   # Notebook completo (EDA + Modelos)
├── relatorio_space_connect.md     # Relatório técnico
├── data/
│   └── satellite_disaster_risk.csv  # Dataset
└── outputs/
    ├── fig1_eda.png               # Análise exploratória
    ├── fig2_modelos.png           # Avaliação dos modelos
    ├── fig3_painel.png            # Painel de resultados
    └── metrics.json               # Métricas exportadas
```

## Como Executar

```bash
pip install pandas numpy scikit-learn matplotlib seaborn jupyter
jupyter notebook notebook_space_connect.ipynb
```

## Fonte dos Dados

Dataset sintético baseado em padrões reais de:
- [INPE — Queimadas](https://queimadas.dgi.inpe.br)
- [NASA MODIS](https://modis.gsfc.nasa.gov)
- [NOAA Climate Data](https://www.ncdc.noaa.gov)
