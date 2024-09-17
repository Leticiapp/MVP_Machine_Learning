# MVP de Machine Learning

## Descrição
Este projeto visa desenvolver um modelo de Machine Learning capaz de prever a potabilidade da água com base em suas características físico-químicas. O modelo utiliza um conjunto de dados contendo informações sobre diversos parâmetros da água, como pH, dureza, sólidos totais dissolvidos, entre outros, para determinar se uma amostra de água é segura para consumo humano.

## Objetivo
O principal objetivo deste projeto é construir um modelo preciso e confiável que possa auxiliar na identificação rápida e eficiente da potabilidade da água. Esse modelo pode ser útil para diversas aplicações, como:

* Monitoramento da qualidade da água em tempo real.
* Identificação de fontes de água potável em situações de emergência.
* Avaliação da eficácia de sistemas de tratamento de água.
* Tomada de decisões em políticas públicas relacionadas à água.

## Ferramentas e Tecnologias
O projeto utiliza as seguintes ferramentas e tecnologias:

* **Python:** Linguagem de programação utilizada para o desenvolvimento do modelo, análise de dados e visualização.
* **Bibliotecas Python:**
    * **Pandas:** Manipulação e análise de dados.
    * **NumPy:** Computação científica, especialmente para trabalhar com arrays multidimensionais.
    * **Scikit-learn:** Machine learning, incluindo algoritmos de classificação, métricas de avaliação e ferramentas de pré-processamento.
    * **Matplotlib:** Criação de gráficos e visualizações estáticas.
    * **Seaborn:** Visualizações estatísticas mais atraentes.
    * **Missingno:** Visualização de dados ausentes.
* **Google Colab:** Ambiente de desenvolvimento online para Python, que permite a execução do código e a criação do relatório em um único notebook.

## Conjunto de Dados
O conjunto de dados utilizado neste projeto foi obtido do Kaggle e contém informações sobre 3276 amostras de água, cada uma com 10 características físico-químicas:

* **pH:** Nível de acidez ou alcalinidade da água (medido em unidades de pH).
* **Dureza (Hardness):** Quantidade de minerais dissolvidos na água, principalmente cálcio e magnésio (medida em mg/L).
* **Sólidos Totais Dissolvidos (Solids):** Quantidade total de substâncias dissolvidas na água, incluindo minerais, sais e matéria orgânica (medida em ppm).
* **Cloraminas (Chloramines):** Desinfetantes utilizados no tratamento da água (medidos em ppm).
* **Sulfato (Sulfate):** Substância química encontrada naturalmente na água (medida em mg/L).
* **Condutividade (Conductivity):** Capacidade da água de conduzir corrente elétrica (medida em μS/cm).
* **Carbono Orgânico (Organic_carbon):** Quantidade de carbono presente em compostos orgânicos dissolvidos na água (medida em ppm).
* **Trihalometanos (Trihalomethanes):** Subprodutos da desinfecção da água com cloro (medidos em μg/L).
* **Turbidez (Turbidity):** Medida da clareza da água (medida em NTU).
* **Potabilidade (Potability):** Variável alvo que indica se a água é potável (1) ou não potável (0).

## Pré-processamento de Dados
O pré-processamento dos dados foi realizado para garantir a qualidade e a adequação do conjunto de dados para o treinamento do modelo de Machine Learning. As seguintes etapas foram realizadas:

* **Tratamento de Valores Ausentes (Missings):** Os valores ausentes nas colunas "pH", "Sulfate" e "Trihalomethanes" foram preenchidos com a mediana dos valores da mesma classe de potabilidade (0 ou 1).
* **Tratamento de Outliers:** Os outliers, identificados como valores três vezes maiores que o desvio padrão, foram substituídos pela mediana da mesma coluna, agrupados por classe de potabilidade.
* **Seleção de Atributos (Feature Selection):** Foram testadas três abordagens para a seleção de atributos:
    * **Todos os atributos:** Todos os 9 atributos foram utilizados no treinamento do modelo.
    * **SelectKBest:** Selecionou os 6 melhores atributos com base em testes estatísticos univariados (pontuação F).
    * **Eliminação Recursiva de Atributos (RFE):** Removeu iterativamente os atributos menos importantes, utilizando a Regressão Logística como estimador base, até restarem 6 atributos.

## Modelagem
Diversos modelos de Machine Learning foram avaliados para encontrar o que melhor se ajusta aos dados e produz as previsões mais precisas:

* **Modelos:**
    * Regressão Logística (LR)
    * K-Nearest Neighbors (KNN)
    * Árvore de Decisão (CART)
    * Naive Bayes (NB)
    * Support Vector Machine (SVM)
    * Stochastic Gradient Descent (SGD)
* **Ensembles:**
    * Bagging
    * Random Forest (RFC)
    * Gradient Boosting (GB)
    * Voting

## Validação Cruzada
Para avaliar o desempenho dos modelos e evitar o overfitting, foi utilizada a técnica de validação cruzada k-fold estratificada, com 10 folds (k = 10). A estratificação garante que cada fold tenha uma distribuição semelhante de amostras de água potável e não potável, proporcionando uma avaliação mais robusta do modelo.

## Pipelines, Padronização e Normalização
Para automatizar o processo de treinamento e avaliação dos modelos, foram utilizadas pipelines do Scikit-learn, que permitem encadear as etapas de pré-processamento e modelagem. Além disso, foram avaliados os efeitos da padronização (StandardScaler) e da normalização (MinMaxScaler) dos dados no desempenho dos modelos.

## Resultados e Seleção do Modelo Final
Os resultados da avaliação dos modelos indicaram que o **Gradient Boosting (GB) com os dados normalizados (MinMaxScaler)** apresentou o melhor desempenho, com uma acurácia média de 79,54% na validação cruzada. A otimização dos hiperparâmetros do modelo Gradient Boosting foi realizada utilizando o GridSearchCV, o que resultou nos seguintes parâmetros:

* `learning_rate`: 0.1
* `max_depth`: 3
* `n_estimators`: 200

## Conclusões
O projeto demonstrou a viabilidade da aplicação de técnicas de Machine Learning para prever a potabilidade da água com base em suas características físico-químicas. O modelo final, utilizando o algoritmo Gradient Boosting, apresentou uma acurácia promissora e pode servir como base para o desenvolvimento de ferramentas e aplicações que auxiliem na garantia da qualidade da água e na saúde pública.

## Limitações e Trabalhos Futuros
Apesar dos resultados promissores, o modelo possui algumas limitações:

* **Conjunto de dados limitado:** O modelo foi treinado com um conjunto de dados relativamente pequeno (3276 amostras), o que pode limitar sua capacidade de generalização.
* **Viés nos dados:** O conjunto de dados pode conter vieses que não foram completamente mitigados durante o pré-processamento, o que pode afetar a imparcialidade do modelo.

Para trabalhos futuros, algumas sugestões são:

* **Expandir o conjunto de dados:** Coletar dados adicionais de diferentes fontes para aumentar a diversidade e a representatividade do conjunto de dados.
* **Explorar outros algoritmos:** Avaliar o desempenho de outros algoritmos de Machine Learning, como redes neurais, para verificar se é possível obter uma acurácia ainda maior.
