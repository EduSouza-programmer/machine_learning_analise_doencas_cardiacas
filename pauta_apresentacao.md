# Roteiro para Apresentação: Análise de Doenças Cardíacas

---

### 1. Introdução (Slide 1-2)

*   **Apresentação:** Meu nome é Eduardo Lima da Silva Souza e este é o projeto da disciplina de Inteligência Artificial.
*   **Objetivo Principal:** O objetivo deste trabalho foi aplicar técnicas de Machine Learning para duas tarefas principais em um dataset de doenças cardíacas:
    1.  **Classificação:** Prever se um paciente tem ou não uma doença cardíaca.
    2.  **Clusterização:** Identificar grupos naturais de pacientes com perfis clínicos semelhantes.
*   **Dataset Utilizado:** Foi utilizado o dataset "Heart Disease" do repositório da UCI, um conjunto de dados clássico para este tipo de problema, contendo 303 amostras e 13 atributos clínicos.

---

### 2. Análise Exploratória e Pré-processamento (Slide 3-4)

*   **Qualidade dos Dados:** A primeira análise mostrou que o dataset era de alta qualidade, mas com alguns valores ausentes em duas colunas (`ca` e `thal`).
*   **Tratamento:** Para não perder dados, optei por preencher os valores faltantes usando a **moda** (o valor mais frequente), uma estratégia adequada para variáveis categóricas.
*   **Principais Insights (Gráficos):**
    *   **Balanceamento:** O dataset está bem balanceado entre pacientes com (classe 1) e sem (classe 0) a doença, o que é ótimo para treinar os modelos.
    *   **Correlação:** A matriz de correlação mostrou que atributos como `cp` (tipo de dor no peito), `thalach` (frequência cardíaca máxima) e `slope` (inclinação do segmento ST) são os mais correlacionados com a presença da doença, indicando que seriam importantes para a previsão.

---

### 3. Modelagem de Classificação (Slide 5-7)

*   **Objetivo:** Treinar 3 algoritmos diferentes para classificar os pacientes.
*   **Preparação:** Os dados foram **normalizados** com `StandardScaler` para que todas as variáveis tivessem a mesma escala, o que melhora o desempenho de algoritmos como KNN e SVM.
*   **Algoritmos e Parâmetros:**
    1.  **Árvore de Decisão:** Escolhida pela sua interpretabilidade. Usei `max_depth=5` para evitar overfitting.
    2.  **K-Nearest Neighbors (KNN):** Um modelo simples e eficaz. Usei `n_neighbors=7`, um valor comum para balancear o modelo.
    3.  **Support Vector Machine (SVM):** Um modelo robusto. Usei o `kernel='rbf'` para capturar relações não lineares nos dados.
*   **Resultados (Métricas e Curva ROC):**
    *   Todos os modelos tiveram um bom desempenho, com acurácias acima de 77%.
    *   A **curva ROC** (gráfico que compara os modelos) mostrou que o **SVM foi o melhor classificador**, com uma **AUC (Área Sob a Curva) de 0.94**, indicando um excelente poder de discriminação entre as classes.

---

### 4. Modelagem de Clusterização (Slide 8-9)

*   **Objetivo:** Agrupar os pacientes sem usar os rótulos de doença, apenas com base em suas características clínicas.
*   **Algoritmos e Parâmetros:**
    1.  **K-Means:**
        *   Para encontrar o número ideal de clusters (`k`), utilizei o **Silhouette Score**. O gráfico mostrou que `k=2` foi a melhor escolha, sugerindo que os pacientes se dividem naturalmente em dois grandes perfis.
    2.  **DBSCAN:**
        *   Este algoritmo, baseado em densidade, não requer um número de clusters. Ele encontrou **1 cluster principal** e identificou **66 pacientes como ruído (outliers)**, o que pode ser útil para analisar casos atípicos.
*   **Visualização (PCA):**
    *   Como não podemos plotar 13 dimensões, usei **PCA** para reduzir os dados para 2D.
    *   Os gráficos mostraram visualmente os dois clusters formados pelo K-Means e o grande cluster com outliers do DBSCAN.

---

### 5. Conclusão (Slide 10)

*   **Classificação:** O modelo **SVM foi o mais eficaz** para prever a presença de doenças cardíacas, alcançando uma alta acurácia e AUC.
*   **Clusterização:** Os algoritmos de agrupamento conseguiram segmentar os pacientes em perfis distintos. O K-Means sugeriu **dois perfis principais**, enquanto o DBSCAN foi útil para **isolar pacientes com características atípicas**.
*   **Considerações Finais:** O trabalho demonstrou com sucesso a aplicação de diferentes técnicas de Machine Learning, cumprindo todos os objetivos propostos na avaliação.
