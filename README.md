# Análise de Machine Learning - Doenças Cardíacas

## 1. Visão Geral

Este projeto consiste em uma análise de dados utilizando técnicas de aprendizado de máquina, desenvolvido como parte da Avaliação Formativa (AF) da disciplina de **Inteligência Artificial** (Semestre 2025-II).

O objetivo é aplicar algoritmos de **Classificação** e **Clusterização** sobre o dataset "Heart Disease" da UCI para, respectivamente, prever a presença de doenças cardíacas e identificar perfis de pacientes.

## 2. Tecnologias Utilizadas

A análise foi desenvolvida inteiramente em Python, utilizando as seguintes bibliotecas principais:
*   **uv:** Para gerenciamento de ambiente virtual e instalação de pacotes.
*   **pandas:** Para manipulação e análise de dados.
*   **scikit-learn:** Para implementação dos algoritmos de Machine Learning e pré-processamento.
*   **matplotlib** e **seaborn:** Para visualização de dados.
*   **Jupyter Notebook:** Como ambiente de desenvolvimento interativo.

## 3. Como Executar o Projeto Localmente

Para replicar a análise em seu ambiente local, siga os passos abaixo.

### Pré-requisitos

*   Python 3.10 ou superior instalado.
*   `pip` (geralmente já vem com o Python).

### Passo a Passo

**1. Clone o Repositório**
```bash
# git clone <URL_DO_SEU_REPOSITORIO>
cd <NOME_DA_PASTA_DO_PROJETO>
```

**2. Instale o `uv`**
`uv` é um instalador de pacotes rápido. Se você ainda não o tiver, instale-o com pip:
```bash
pip install uv
```

**3. Crie o Ambiente Virtual e Instale as Dependências**
Execute o comando abaixo no terminal, na raiz do projeto. Ele irá criar um ambiente virtual chamado `.venv` e instalar todas as bibliotecas necessárias.
```bash
uv venv && uv pip install pandas numpy ucimlrepo scikit-learn matplotlib seaborn notebook
```

**4. Inicie o Servidor Jupyter**
Após a instalação, inicie o servidor Jupyter usando o `uv` para garantir que ele execute dentro do ambiente virtual correto.
```bash
uv run jupyter notebook
```

**5. Abra o Notebook**
O comando acima deverá abrir uma aba no seu navegador. Clique no arquivo `analise_heart_disease.ipynb` para abri-lo.

Agora você pode executar todas as células do notebook para ver a análise completa.
