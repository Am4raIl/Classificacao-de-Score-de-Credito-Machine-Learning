# 📊 Classificação de Score de Crédito

> **Trabalho Prático 1 — Disciplina de Aprendizado de Máquina**

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.12-3776AB?style=for-the-badge&logo=python&logoColor=white" />
  <img src="https://img.shields.io/badge/scikit--learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white" />
  <img src="https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white" />
  <img src="https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white" />
  <img src="https://img.shields.io/badge/Plotly-3F4F75?style=for-the-badge&logo=plotly&logoColor=white" />
  <img src="https://img.shields.io/badge/Google%20Colab-F9AB00?style=for-the-badge&logo=googlecolab&logoColor=black" />
</p>

---

## 📝 Descrição Geral

Este repositório contém o **Trabalho Prático 1** da disciplina de **Aprendizado de Máquina**. O objetivo principal foi desenvolver um pipeline completo de Machine Learning, seguindo o fluxo de trabalho descrito no livro *"Mãos à Obra: Aprendizado de Máquina com Scikit-Learn, Keras e TensorFlow"* (Aurélien Géron).

O projeto aborda um problema de **classificação multiclasse**, onde o objetivo é prever o **Score de Crédito** de clientes bancários com base em seu histórico financeiro e comportamental, classificando-os em três categorias:

| Categoria | Descrição |
|:---:|:---|
| 🟢 `Good` | Cliente com boa saúde financeira e baixo risco |
| 🟡 `Standard` | Cliente com perfil financeiro intermediário |
| 🔴 `Poor` | Cliente com histórico de inadimplência e alto risco |

### 👥 Autores

- **Mateus Filipe Valentim**
- **Felipe Kitamoto Amaral**

---

### ▶️ Desenvolvimento no Google Colab

O projeto foi originalmente desenvolvido no **Google Colab**, utilizando a estrutura de notebooks (células de código e markdown). O arquivo `.py` disponível neste repositório é a exportação direta desse notebook.

## 🗂️ O Dataset

O conjunto de dados utilizado (`clientes.csv`) contém informações financeiras e comportamentais mensais de clientes bancários. O problema consiste em analisar esse histórico para determinar a credibilidade de cada cliente.

- **Fonte:** [Kaggle — Credit Score Classification](https://www.kaggle.com/)
- **Granularidade original:** Dados mensais por cliente (múltiplos registros por `id_cliente`)
- **Variável Alvo:** `score_credito` — categórica com 3 classes: `Good`, `Standard`, `Poor`

### Principais Variáveis

| Variável | Tipo | Descrição |
|:---|:---:|:---|
| `id_cliente` | Numérica | Identificador único do cliente |
| `mes` | Numérica | Mês de referência do registro |
| `idade` | Numérica | Idade do cliente |
| `salario_anual` | Numérica | Renda anual |
| `num_cartoes` | Numérica | Quantidade de cartões de crédito |
| `juros_emprestimo` | Numérica | Taxa de juros aplicada |
| `dias_atraso` | Numérica | Dias de atraso no pagamento |
| `divida_total` | Numérica | Valor total de dívidas |
| `historico_credito` | Numérica | Tempo de histórico de crédito |
| `taxa_uso_credito` | Numérica | Percentual de crédito utilizado |
| `profissao` | Categórica | Ocupação profissional |
| `mix_credito` | Ordinal | Qualidade do mix de crédito (`Ruim`, `Normal`, `Bom`) |
| `comportamento_pagamento` | Ordinal | Padrão de pagamento extraído do comportamento |

---

## 🚀 Etapas do Pipeline

O desenvolvimento seguiu as etapas fundamentais de um projeto de Data Science:

```
clientes.csv
     │
     ▼
┌─────────────────────┐
│  1. Carregamento e  │
│     Inspeção        │
└────────┬────────────┘
         │
         ▼
┌─────────────────────┐
│  2. Limpeza e       │
│     Agregação       │
└────────┬────────────┘
         │
         ▼
┌─────────────────────┐
│  3. EDA — Histog.   │
│     Boxplots, Corr. │
└────────┬────────────┘
         │
         ▼
┌─────────────────────┐
│  4. Pré-Proc.       │
│  Encoding + Scaling │
└────────┬────────────┘
         │
         ▼
┌─────────────────────┐
│  5. Modelagem       │
│  RF / KNN / Árvore  │
└────────┬────────────┘
         │
         ▼
┌─────────────────────┐
│  6. Avaliação       │
│  TTS / CV / Grid    │
└────────┬────────────┘
         │
         ▼
┌─────────────────────┐
│  7. Matriz de       │
│     Confusão        │
└─────────────────────┘
```

---

### 1. 🔍 Carregamento e Inspeção

- Leitura do arquivo `clientes.csv` com encoding `latin`.
- Exibição das primeiras linhas, informações de tipos e estatísticas descritivas.
- Identificação de colunas numéricas e categóricas.

---

### 2. 🧹 Limpeza e Agregação

Como os dados são mensais (múltiplas linhas por cliente), foi necessário consolidar o histórico em **um perfil único por cliente** antes da modelagem:

- Remoção de colunas inteiramente vazias e linhas duplicadas.
- Conversão de colunas numéricas erroneamente tipadas como texto.
- **Agrupamento por `id_cliente`:**
  - Variáveis numéricas → **média** dos meses
  - Variáveis categóricas → **último valor** registrado
- Exportação do resultado em `.csv` para Excel e LibreOffice.

---

### 3. 📈 Análise Exploratória de Dados (EDA)

Visualizações geradas para entender o comportamento das variáveis em relação ao Score:

- **Histogramas interativos (Plotly):** Distribuição de cada variável segmentada por Score de Crédito.
- **Boxplots interativos (Plotly):** Dispersão e outliers das variáveis numéricas por categoria.
- **Correlação de Pearson (Seaborn):** Relação entre variáveis numéricas e o Score (codificado como 0/1/2).
- **V de Cramér (Seaborn):** Força de associação entre variáveis categóricas e o Score de Crédito.

---

### 4. ⚙️ Pré-processamento

Todo o pré-processamento foi encapsulado em um `ColumnTransformer` integrado aos Pipelines, garantindo que nenhum vazamento de dados (*data leakage*) ocorra entre treino e teste.

| Tipo de Variável | Técnica Aplicada | Variáveis |
|:---|:---|:---|
| Categórica Nominal | `OneHotEncoder` | `profissao` |
| Categórica Ordinal | `OrdinalEncoder` | `mix_credito`, `comportamento_pagamento`, `comportamento_gasto` |
| Numérica | `RobustScaler` | Todas as demais numéricas |

> **Por que `RobustScaler`?** Por ser resistente a outliers — utiliza a mediana e o IQR em vez da média e desvio padrão, sendo mais adequado para dados financeiros com distribuições assimétricas.

**Engenharia de Atributo:** A coluna `comportamento_pagamento` foi desmembrada via `str.extract` em duas colunas — `comportamento_gasto` (`baixo`/`alto`) e `comportamento_pagamento` (`baixo`/`medio`/`alto`) — antes do encoding ordinal.

---

### 5. 🤖 Modelagem

Foram implementados três algoritmos de classificação, cada um encapsulado em seu próprio **Pipeline**:

#### 🌳 Random Forest
```python
RandomForestClassifier(
    n_estimators=300, max_depth=15,
    min_samples_split=5, min_samples_leaf=2,
    max_features='sqrt', bootstrap=True,
    class_weight='balanced', random_state=42
)
```
> Ensemble de árvores de decisão que reduz overfitting por meio de bagging. O parâmetro `class_weight='balanced'` compensa o eventual desbalanceamento entre as classes.

#### 📍 K-Nearest Neighbors (KNN)
```python
KNeighborsClassifier(
    n_neighbors=9, weights='distance',
    metric='minkowski', p=2
)
```
> Classifica uma nova amostra com base nos `k` vizinhos mais próximos. O peso `distance` dá maior influência a vizinhos mais próximos, mitigando o ruído de pontos distantes.

#### 🌿 Árvore de Decisão
```python
DecisionTreeClassifier(
    max_depth=15, min_samples_split=5,
    min_samples_leaf=2, criterion='gini',
    class_weight='balanced', random_state=42
)
```
> Modelo interpretável que serve como baseline e contraponto ao Random Forest. Mais suscetível a overfitting sem restrições adequadas de profundidade.

---

### 6. 📐 Avaliação e Otimização

Os modelos foram avaliados com três estratégias progressivas:

#### 6.1 Train-Test Split (80/20)
Divisão aleatória estratificada para preservar a proporção das classes entre os conjuntos.

**Métricas avaliadas:**

| Métrica | Descrição |
|:---|:---|
| **Acurácia** | Proporção de previsões corretas sobre o total |
| **Precisão** | Dos classificados como positivos, quantos realmente são |
| **Recall** | Dos que realmente são positivos, quantos foram identificados |
| **F1-Score** | Média harmônica entre Precisão e Recall |

> Todas as métricas foram calculadas com `average='weighted'` para lidar com o desbalanceamento entre classes.

#### 6.2 Validação Cruzada (Cross-Validation)
`StratifiedKFold` com 5 folds para uma estimativa mais robusta e com menor variância. Os resultados são reportados como **média ± desvio padrão** entre os folds.

#### 6.3 Otimização com Grid Search
`GridSearchCV` com `StratifiedKFold` de 2 folds para encontrar a melhor combinação de hiperparâmetros para cada modelo.

<details>
<summary>📋 Espaço de busca — Random Forest</summary>

```python
{
    'n_estimators':      [500, 700],
    'max_depth':         [15, None],
    'min_samples_split': [2, 5],
    'min_samples_leaf':  [2, 4],
    'max_features':      ['log2', 'sqrt'],
    'class_weight':      ['balanced'],
    'bootstrap':         [True]
}
```
</details>

<details>
<summary>📋 Espaço de busca — KNN</summary>

```python
{
    'n_neighbors': [7, 9, 11],
    'weights':     ['uniform', 'distance'],
    'p':           [2],
    'metric':      ['minkowski', 'manhattan']
}
```
</details>

<details>
<summary>📋 Espaço de busca — Árvore de Decisão</summary>

```python
{
    'criterion':         ['gini', 'entropy', 'log_loss'],
    'max_depth':         [None, 20, 15],
    'min_samples_split': [2, 5, 20],
    'min_samples_leaf':  [2, 4, 8],
    'max_features':      ['sqrt', 'log2'],
    'class_weight':      ['balanced'],
    'splitter':          ['best', 'random']
}
```
</details>

---

### 7. 🔲 Matriz de Confusão

Após o Grid Search, foram geradas matrizes de confusão para cada modelo otimizado, permitindo analisar visualmente os erros de classificação entre as três classes (`Poor`, `Standard`, `Good`).

---

## 💡 Discussão dos Resultados

- O **Random Forest** apresentou o melhor desempenho geral, beneficiando-se do ensemble de múltiplas árvores e da robustez a overfitting proporcionada pelo bagging e pela aleatoriedade na seleção de features.
- O **KNN** mostrou-se sensível à escala das variáveis, reforçando a importância do `RobustScaler` no pré-processamento.
- A **Árvore de Decisão** isolada apresentou maior variância entre os folds de cross-validation, evidenciando sua tendência ao overfitting em comparação com o ensemble.
- A estratégia de **agregar os dados mensais por `id_cliente` antes da divisão treino/teste** foi essencial para evitar *data leakage* entre registros do mesmo cliente.

---

## 🛠️ Como Executar

### Pré-requisitos

- Python >= 3.10
- Arquivo `clientes.csv` na raiz do projeto

### Instalação das Dependências

```bash
pip install pandas numpy openpyxl scikit-learn plotly matplotlib seaborn
```

### 💻 Execução Local

1. Clone o repositório:
   ```bash
   git clone https://github.com/Am4raIl/Classificacao-de-Score-de-Credito-Machine-Learning.git
   cd Classificacao-de-Score-de-Credito-Machine-Learning
   ```
2. Instale as dependências:
   ```bash
   pip install pandas numpy openpyxl scikit-learn plotly matplotlib seaborn
   ```
3. Coloque o arquivo `clientes.csv` na mesma pasta do script e execute:
   ```bash
   python "trabalho_prático_1_de_aprendizado_de_máquina_mateus_filipe_valentim_felipe_kitamoto_amaral.py"
   ```

---

## 📁 Estrutura do Repositório

```
📦 Classificacao-de-Score-de-Credito-Machine-Learning/
├── 📄 trabalho_prático_1_de_aprendizado_de_máquina_mateus_filipe_valentim_felipe_kitamoto_amaral.py
├── 📄 clientes.csv                    # Dataset de entrada (necessário para execução)
├── 📄 clientes_agrupado_excel.csv     # Dataset agregado (decimal com ponto — Excel)
├── 📄 clientes_agrupado_libre.csv     # Dataset agregado (decimal com vírgula — LibreOffice)
└── 📄 README.md
```

---

## 📚 Referências

- GÉRON, Aurélien. *Mãos à Obra: Aprendizado de Máquina com Scikit-Learn, Keras e TensorFlow*. 2ª ed. O'Reilly, 2019.
- [Documentação do scikit-learn](https://scikit-learn.org/stable/)
- [Dataset — Kaggle: Credit Score Classification](https://www.kaggle.com/)

---

<p align="center">Desenvolvido por <strong>Mateus Filipe Valentim</strong> e <strong>Felipe Kitamoto Amaral</strong></p>
