# 📊 Classificação de Score de Crédito
> **Trabalho Prático 1 - Aprendizado de Máquina**

![Python](https://img.shields.io/badge/Python-3.12-blue?style=for-the-badge&logo=python&logoColor=white)
![Scikit-Learn](https://img.shields.io/badge/scikit__learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
![Plotly](https://img.shields.io/badge/Plotly-3F4F75?style=for-the-badge&logo=plotly&logoColor=white)

## 📝 Descrição Geral

Este repositório contém o **Trabalho Prático 1** da disciplina de **Aprendizado de Máquina**. O objetivo principal foi desenvolver um sistema completo de Machine Learning, seguindo o fluxo de trabalho descrito no livro *"Mãos à Obra: Aprendizado de Máquina com Scikit-Learn, Keras e TensorFlow"* (Aurélien Géron).

O projeto foca em um problema de **Classificação**, onde o objetivo é prever o **Score de Crédito** (*Credit Score*) de clientes bancários, classificando-os em categorias como `Good`, `Standard` e `Poor`.

### 👥 Autores
* **Mateus Filipe Valentim**
* **Felipe Kitamoto Amaral**

---

## 🗂️ O Dataset

O conjunto de dados utilizado contém informações financeiras e comportamentais de clientes. O problema consiste em analisar esse histórico para determinar a credibilidade do cliente.

* **Fonte:** [Kaggle - Credit Score Classification](https://www.kaggle.com/) (Baseado em dados públicos)
* **Variáveis Principais:** `idade`, `salario_anual`, `num_cartoes`, `juros_emprestimo`, `dias_atraso`, `divida_total`, `historico_credito`, entre outras.
* **Variável Alvo (Target):** `score_credito` (Categórica: Good, Standard, Poor).

---

## 🚀 Etapas do Projeto

O desenvolvimento do projeto seguiu as etapas fundamentais de um pipeline de Data Science:

### 1. Seleção e Compreensão dos Dados
- Carregamento da base de dados `clientes.csv`.
- Identificação dos tipos de variáveis (numéricas e categóricas).
- Definição do problema de negócio: **Mitigação de risco de crédito**.

### 2. Análise Exploratória de Dados (EDA)
Utilizamos **Plotly** e **Seaborn** para entender a distribuição dos dados:
- **Histogramas:** Visualização da frequência das variáveis em relação ao Score.
- **Boxplots:** Identificação de outliers e dispersão de dados (ex: Idade vs Score).
- **Correlações:** Análise de dependência entre atributos.

### 3. Pré-processamento e Limpeza
Etapa crucial realizada no código:
- **Limpeza:** Remoção de colunas inteiramente vazias e linhas duplicadas.
- **Tratamento de Tipos:** Conversão de colunas numéricas que estavam como texto.
- **Engenharia de Atributos:** Agrupamento de dados por `id_cliente` para consolidar o histórico mensal em um perfil único (média para numéricos, último valor para categóricos).
- **Codificação:** - `LabelEncoder` para a variável alvo (`score_credito`).
    - `OneHotEncoder` / `OrdinalEncoder` para variáveis categóricas (ex: `profissao`, `mix_credito`).
- **Normalização:** Uso de `StandardScaler` e `RobustScaler` para colocar as variáveis na mesma escala.

### 4. Modelagem (Machine Learning)
Foram implementados e comparados os seguintes algoritmos de aprendizado supervisionado:

| Algoritmo | Justificativa de Escolha |
| :--- | :--- |
| **Random Forest** | Excelente para dados tabulares, robusto a outliers e capaz de capturar relações não lineares complexas. |
| **K-Nearest Neighbors (KNN)** | Algoritmo baseado em distância, simples e intuitivo para classificação baseada em similaridade de perfil. |
| **Decision Tree** | Modelo de fácil interpretação que serve como base comparativa para o Random Forest. |

### 5. Avaliação e Otimização
- **Métricas Utilizadas:** Acurácia, Precisão, Recall e F1-Score.
- **Validação:** Divisão treino/teste (`train_test_split`) e Validação Cruzada (`cross_val_score`).
- **Ajuste de Hiperparâmetros:** Utilização de `GridSearchCV` e `RandomizedSearchCV` para encontrar a melhor configuração dos modelos.

---

## 📊 Resultados e Discussão

Os modelos foram avaliados com base na capacidade de generalização.
- O **Random Forest** apresentou, em geral, o melhor desempenho devido à sua capacidade de *ensemble* (combinação de várias árvores), reduzindo o overfitting comparado a uma única Árvore de Decisão.
- O **KNN** mostrou-se sensível à escala dos dados, justificando o uso intenso de normalização no pré-processamento.

*(Insira aqui uma tabela ou print dos seus resultados finais de acurácia se desejar)*

---

## 🛠️ Como Executar o Projeto

### Pré-requisitos
Certifique-se de ter o Python instalado. As dependências podem ser instaladas via pip:

```bash
pip install pandas numpy openpyxl scikit-learn plotly matplotlib seaborn
