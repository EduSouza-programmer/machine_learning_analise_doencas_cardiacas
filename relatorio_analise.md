# Relatório de Análise de Machine Learning: Doenças Cardíacas

---

### **1. Introdução**

Este relatório detalha o processo de aplicação de técnicas de aprendizado de máquina para análise do dataset "Heart Disease", proveniente do repositório da UCI. O projeto foi desenvolvido como parte da avaliação formativa da disciplina de Inteligência Artificial.

**1.1. Objetivo**

O objetivo central do trabalho é duplo:
1.  **Classificação:** Desenvolver e avaliar modelos de aprendizado supervisionado capazes de prever a presença ou ausência de doença cardíaca em pacientes com base em um conjunto de atributos clínicos.
2.  **Clusterização:** Aplicar algoritmos de aprendizado não supervisionado para identificar agrupamentos naturais de pacientes, buscando perfis clínicos distintos que possam indicar diferentes níveis ou tipos de risco.

**1.2. Seleção e Descrição do Banco de Dados**

O dataset escolhido foi o **Heart Disease** da base de Cleveland, recomendado pela comunidade de Machine Learning para tarefas de classificação. Ele contém 303 registros (pacientes) e 13 atributos, além da variável alvo.

*   **Atributos Principais:** `age`, `sex`, `cp` (tipo de dor no peito), `trestbps` (pressão arterial em repouso), `chol` (colesterol), `thalach` (frequência cardíaca máxima), entre outros.
*   **Variável Alvo (`num`):** Indica a presença de doença cardíaca, variando de 0 (ausência) a 4. Para esta análise, o problema foi simplificado para uma classificação binária (0 para ausência, 1 para presença).

---

### **2. Metodologia**

**2.1. Pré-processamento dos Dados**

A primeira etapa foi uma análise da qualidade dos dados. O método `.info()` do Pandas revelou que as colunas `ca` e `thal` continham valores ausentes (4 e 2, respectivamente).

*   **Justificativa da Imputação:** Dada a pequena quantidade de dados faltantes, a remoção das linhas correspondentes poderia resultar em perda de informação relevante. Portanto, optou-se pela **imputação**, preenchendo os valores ausentes com a **moda** (valor mais frequente) de cada coluna. Essa estratégia é ideal para variáveis categóricas ou discretas, pois preserva a distribuição original dos dados.

**2.2. Análise Exploratória de Dados (EDA)**

Após o tratamento, foram geradas visualizações para extrair insights:
*   **Distribuição das Variáveis:** Histogramas mostraram a distribuição de cada atributo, ajudando a compreender suas características (e.g., distribuição normal para `age`, natureza categórica para `cp`).
*   **Balanceamento de Classes:** Um gráfico de contagem revelou que as classes (presença/ausência de doença) estavam razoavelmente balanceadas, o que é favorável para o treinamento de modelos de classificação.
*   **Matriz de Correlação:** Um heatmap de correlação foi gerado para visualizar a relação entre os atributos e a variável alvo. As variáveis com maior correlação (positiva ou negativa) com o alvo foram `cp`, `thalach`, `slope`, `exang` e `oldpeak`, indicando seu potencial preditivo.

**2.3. Algoritmos de Classificação**

Foram implementados três algoritmos de classificação, com os dados previamente escalonados usando `StandardScaler` para garantir que todas as features tivessem a mesma importância.

*   **Árvore de Decisão:**
    *   **Justificativa:** Escolhida por sua alta interpretabilidade e capacidade de ser visualizada.
    *   **Parâmetros:** `max_depth=5` foi definido para evitar que a árvore crescesse demais e se ajustasse excessivamente aos dados de treino (overfitting).
*   **K-Nearest Neighbors (KNN):**
    *   **Justificativa:** Um algoritmo simples e intuitivo, baseado na similaridade entre amostras.
    *   **Parâmetros:** `n_neighbors=7` foi escolhido como um valor padrão que geralmente oferece um bom equilíbrio entre viés e variância.
*   **Support Vector Machine (SVM):**
    *   **Justificativa:** Um modelo robusto e eficaz, especialmente com o uso de kernels para lidar com dados não linearmente separáveis.
    *   **Parâmetros:** O `kernel='rbf'` foi utilizado por sua flexibilidade em capturar relações complexas. `probability=True` foi ativado para permitir o cálculo da curva ROC.

**2.4. Algoritmos de Clusterização**

Foram aplicados dois algoritmos de agrupamento nos dados escalonados.

*   **K-Means:**
    *   **Justificativa:** É o algoritmo de clusterização mais utilizado devido à sua simplicidade e eficiência computacional.
    *   **Parâmetros:** O número de clusters (`k`) foi determinado objetivamente através do **Silhouette Score**. O valor de `k` que maximizou essa métrica foi **2**, sugerindo que os dados se dividem naturalmente em dois perfis principais.
*   **DBSCAN:**
    *   **Justificativa:** Um algoritmo baseado em densidade, que não requer a definição do número de clusters e é capaz de identificar outliers.
    *   **Parâmetros:** Foram utilizados `eps=2.5` (raio de vizinhança) e `min_samples=5` (número mínimo de pontos para formar um cluster), valores que se mostraram eficazes para encontrar uma estrutura de cluster densa.

---

### **3. Resultados**

**3.1. Avaliação de Desempenho da Classificação**

Os modelos foram avaliados usando as métricas exigidas e validação cruzada (k-fold com k=10).

| Modelo                 | Acurácia   | Sensibilidade (Recall) | Especificidade | AUC      | Acurácia (k-fold) |
| ---------------------- | ---------- | ---------------------- | -------------- | -------- | ----------------- |
| Árvore de Decisão      | 0.7705     | 0.8571                 | 0.6970         | 0.80     | 0.7312            |
| K-Nearest Neighbors    | 0.8525     | 0.8929                 | 0.8182         | 0.93     | 0.8138            |
| Support Vector Machine | **0.8689** | **0.8929**             | **0.8485**     | **0.94** | **0.8180**        |

*   **Curva ROC:** A comparação visual através da curva ROC confirmou que o **SVM** apresentou o melhor desempenho geral, com a maior Área Sob a Curva (AUC = 0.94).

**3.2. Avaliação de Desempenho da Clusterização**

*   **K-Means:** O Silhouette Score máximo foi obtido com **k=2**, indicando uma boa separação dos dados em dois grupos.
*   **DBSCAN:** O algoritmo identificou **1 cluster principal** e marcou **66 pontos como ruído (outliers)**, sugerindo que uma parte significativa dos pacientes possui perfis clínicos que se desviam do padrão principal.

---

### **4. Discussão e Conclusões**

**4.1. Discussão**

Na tarefa de **classificação**, o **Support Vector Machine (SVM)** se destacou como o modelo mais performático, superando o KNN e a Árvore de Decisão em quase todas as métricas, especialmente na AUC. Isso sugere que a capacidade do kernel RBF de encontrar uma fronteira de decisão não linear foi vantajosa para este conjunto de dados.

Na **clusterização**, os dois algoritmos ofereceram perspectivas diferentes. O **K-Means** dividiu os pacientes em dois grupos distintos, que poderiam ser investigados para entender se representam, por exemplo, "baixo risco" vs. "alto risco". Já o **DBSCAN** foi eficaz em isolar os casos atípicos, que podem corresponder a perfis de pacientes raros ou com comorbidades específicas.

**4.2. Conclusão**

O projeto cumpriu com sucesso todos os requisitos da avaliação. Foram aplicadas e avaliadas múltiplas técnicas de aprendizado de máquina, desde o pré-processamento dos dados até a interpretação dos resultados. A análise demonstrou que é possível construir modelos preditivos eficazes para o diagnóstico de doenças cardíacas e também identificar perfis de pacientes através de métodos não supervisionados, fornecendo insights valiosos a partir de dados clínicos.
