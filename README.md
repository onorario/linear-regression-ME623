# linear-regression-ME623
Modelagem estatística via Regressão Linear Múltipla (Stepwise) e diagnóstico de resíduos para avaliar o impacto de variáveis físico-químicas na qualidade de vinhos.
# 🍷 Estudo da Relação entre Propriedades Físico-Químicas e Qualidade de Vinhos

[![R](https://img.shields.io/badge/R-276DC3?style=flat-square&logo=r&logoColor=white)](https://www.r-project.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)](LICENSE)
[![Dataset: Wine Quality](https://img.shields.io/badge/Dataset-Wine--Quality-purple.svg?style=flat-square)](https://doi.org/10.24432/C56S3T)

Este repositório contém o projeto de modelagem estatística desenvolvido em **R**, focado em investigar como compostos químicos e propriedades físicas influenciam as notas de degustação (qualidade de 0 a 10) atribuídas aos vinhos tintos e brancos do conjunto de dados *Wine Quality* (UCI / Cortez et al., 2009).

> **Contexto:** Projeto desenvolvido para a disciplina **ME623 - Análise de Regressão Linear** (IMECC / UNICAMP).

---

## 📌 Destaques do Projeto

- **Base de Dados Robusta:** Análise de 6.497 amostras (4.898 vinhos brancos e 1.599 vinhos tintos) e 11 variáveis físico-químicas.
- **Seleção Automática de Variáveis:** Comparação e convergência entre os algoritmos *Backward*, *Forward* e *Stepwise* baseados no Critério de Akaike (AIC).
- **Tratamento Metodológico Rigoroso:**
  - Diagnóstico e remoção de multicolinearidade severa na variável `density` (VIF = 22.26).
  - Correção de autocorrelação serial de primeira ordem (Durbin-Watson saltando de $DW = 1.64$ para $DW = 1.98$) via aleatorização do arranjo amostral.
  - Investigação de pontos influentes via Distância de Cook e *Leverage*.
  - Avaliação de transformações matemáticas via log-verossimilhança de Box-Cox ($\lambda \approx 0.75$).

---

## 🧪 Como a Química Explica a Qualidade? (Visão Geral Didática)

Em vez de depender apenas do paladar subjetivo de um sommelier, a modelagem estatística busca entender **quais elementos no laboratório químico determinam se um vinho será bem avaliado**:
