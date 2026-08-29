# linear-regression-ME623
Modelagem estatística via Regressão Linear Múltipla (Stepwise) e diagnóstico de resíduos para avaliar o impacto de variáveis físico-químicas na qualidade de vinhos.
# 🍷 Estudo da Relação entre Propriedades Físico-Químicas e Qualidade de Vinhos

[![R](https://img.shields.io/badge/R-276DC3?style=flat-square&logo=r&logoColor=white)](https://www.r-project.org/)
[![Dataset: Wine Quality](https://img.shields.io/badge/Dataset-Wine--Quality-purple.svg?style=flat-square)](https://doi.org/10.24432/C56S3T)

Este repositório contém o projeto de modelagem estatística desenvolvido em **R**, focado em investigar como compostos químicos e propriedades físicas influenciam as notas de degustação (qualidade de 0 a 10) atribuídas aos vinhos tintos e brancos do conjunto de dados *Wine Quality* (UCI / Cortez et al., 2009).

> **Contexto:** Projeto desenvolvido para a disciplina **ME623 - Análise de Regressão Linear** (IMECC / UNICAMP).

---
## ✒️ Integrantes do Projeto
- Gustavo Coimbra de Souza Teixeira  
- Julia Folgueral 
- Luiz Fernando de Oliveira Pereira  
- Nicole de Barros Silva

## 📌 Informações do Projeto

- **Base de Dados:** Análise de 6.497 amostras (4.898 vinhos brancos e 1.599 vinhos tintos) e 11 variáveis físico-químicas.
- **Seleção Automática de Variáveis:** Comparação e convergência entre os algoritmos *Backward*, *Forward* e *Stepwise* baseados no Critério de Akaike (AIC).
- **Tratamento Metodológico Rigoroso:**
  - Diagnóstico e remoção de multicolinearidade severa na variável `density` (VIF = 22.26).
  - Correção de autocorrelação serial de primeira ordem (Durbin-Watson saltando de $DW = 1.64$ para $DW = 1.98$) via aleatorização do arranjo amostral.
  - Investigação de pontos influentes via Distância de Cook e *Leverage*.
  - Avaliação de transformações matemáticas via log-verossimilhança de Box-Cox ($\lambda \approx 0.75$).
- **Principais Pacotes Utilizados**
  - tidyverse
  - ggplot2
  - MASS
  - car
  - moderndive

---

## 🧪 Como a Química Explica a Qualidade? 

Em vez de depender apenas do paladar subjetivo de um sommelier, a modelagem estatística busca entender **quais elementos no laboratório químico determinam se um vinho será bem avaliado**:

### 1. 📈 Os Principais Impulsionadores 
* **Teor Alcoólico (`alcohol`):** Foi a variável mais relevante do modelo. Vinhos mais alcoólicos tendem a ser mais encorpados e mais bem avaliados sensorialmente.
* **Sulfatos (`sulphates`):** Atuam como conservantes e antioxidantes benéficos, contribuindo positivamente para a conservação e aroma.
* **Açúcar Residual e pH:** Apresentaram impactos positivos moderados na percepção de equilíbrio da bebida.

### 2. 📉 Os Principais Detratores
* **Acidez Volátil (`volatile.acidity`):** Forte redutor de nota. Representa ácidos indesejados (como o ácido acético/vinagre), indicando falhas no controle de fermentação ou oxidação.
* **Cloretos (`chlorides`):** Concentrações elevadas de sal prejudicam a experiência gustativa.
* **Dióxido de Enxofre Total (`total.sulfur.dioxide`):** O excesso gera odores intensos demais e gosto metálico.

### 3. ⚖️ O Ponto de Equilíbrio dos Vinhos (Não-Linearidade)
A análise de resíduos parciais revelou que conservantes como o dióxido de enxofre possuem um **ponto de saturação** (comportamento parabólico): a dosagem ideal protege a bebida, mas o excesso penaliza a avaliação final.

---

## 📊 Principais Resultados do Modelo

O modelo final obtido por Stepwise atingiu um $R^2$ ajustado de **0.29**, indicando que 29% da variação das notas é explicada diretamente pela química do vinho:

| Variável | Coeficiente ($\beta$) | Erro Padrão | Estatística $t$ | $p$-valor | Impacto Sensorial |
| :--- | :---: | :---: | :---: | :---: | :--- |
| **Intercepto** | $+2.198$ | $0.233$ | $9.421$ | $< 0.0001$ | Base inicial |
| **Álcool** | $+0.334$ | $0.009$ | $36.532$ | $< 0.0001$ | Encorpamento (+) |
| **Acidez Volátil** | $-1.520$ | $0.076$ | $-20.028$ | $< 0.0001$ | Sensação avinagrada (-) |
| **Sulfatos** | $+0.575$ | $0.074$ | $7.803$ | $< 0.0001$ | Estabilidade gustativa (+) |
| **Cloretos** | $-1.066$ | $0.329$ | $-3.243$ | $0.0012$ | Salinidade excessiva (-) |
| **Tipo (Branco)** | $-0.132$ | $0.043$ | $-3.034$ | $0.0024$ | Ajuste de base comparativo |

> **Nota Metodológica:** O $R^2$ de 29% é realista para o setor de alimentos e bebidas, onde fatores não tabelados (safra, temperatura de serviço, idade da videira e subjetividade humana) também pesam na decisão do avaliador.

---

## 🔍 Diagnóstico, Robustez e Próximos Passos

- **Independência dos Erros:** O agrupamento original dos vinhos por cor induzia autocorrelação residual ($DW = 1.64$); o reembaralhamento aleatório corrigiu o problema ($DW = 1.98$).
- **Multicolinearidade:** A exclusão da `density` (VIF de $22.26$) eliminou a redundância com álcool e açúcar, estabilizando os coeficientes.
- **Transformação de Box-Cox:** Com $\lambda \approx 0.75$ e o intervalo de 95% contendo o valor $1.0$, validou-se a manutenção da variável resposta na escala linear original, sem precisar fazer alterações mais drásticas.
- **Melhorias** Uma análise mais robusta seria ajustar modelos de **Regressão Ordinal** (como *Cumulative Link Models*), já que a qualidade é avaliada em notas inteiras discretas ($0$ a $10$), esses modelos tratam a variável resposta respeitando sua escala intrínseca de ranking, sem assumir continuidade nem forçar espaçamento idêntico entre notas.

---

