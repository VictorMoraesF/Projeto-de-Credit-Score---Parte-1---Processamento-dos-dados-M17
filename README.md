# 📊 Projeto de Análise Exploratória e Classificação de Credit Score

Este projeto consiste em uma análise exploratória de dados (EDA) e preparação de uma base de clientes com o objetivo de estruturar e tratar variáveis socioeconômicas para futuros modelos preditivos de **Score de Crédito**. 

O projeto passa por todas as etapas essenciais de um pipeline de Ciência de Dados: análise univariada e bivariada, tratamento de dados nulos, encoding de variáveis categóricas, análise de correlação linear e balanceamento de classes.

---

## ⚙️ Funcionalidades e Etapas do Projeto

### 1. Análise Univariada & Categórica Automatizada
* Implementação de rotinas automatizadas (loops `for` e `subplots` dinâmicos) para analisar a distribuição de frequência relativa (%) e absoluta de todas as variáveis categóricas do dataset sem repetição de código.

### 2. Análise Bivariada & Insights de Negócio
Investigação profunda das relações entre variáveis para responder a hipóteses críticas de negócio, respondidas através de visualizações customizadas (`seaborn`):
* **Idade vs. Status Civil:** Distribuição comparativa utilizando *Boxplots*.
* **Score de Crédito vs. Escolaridade:** Análise de dispersão e densidade de comportamento utilizando *Strip Plots* e *Bar Plots* com intervalo de confiança.
* **Idade vs. Salário:** Análise de tendência e evolução de carreira por meio de *Scatter Plots* com linhas de regressão linear.
* **Salário vs. Score de Crédito:** Identificação de padrões de dispersão entre renda e comportamento de crédito.
* **Score de Crédito vs. Casa Própria:** Análise de volumetria e probabilidade de risco utilizando gráficos de barras empilhadas e agrupadas (*Grouped Countplots*).

### 3. Engenharia de Recursos (Feature Engineering & Encoding)
Tratamento e conversão de textos para formatos assimiláveis por algoritmos de Machine Learning:
* **Label Encoding:** Aplicado a variáveis binárias (`Gender`, `Marital Status` e `Home Ownership`).
* **Mapeamento Ordinal Manual:** Aplicado à variável alvo (`Credit Score`: *Low* -> 0, *Average* -> 1, *High* -> 2) para preservar a hierarquia de risco de crédito.
* **One-Hot Encoding:** Aplicado à variável categórica nominal de múltiplos níveis (`Education`), expandindo-a em colunas binárias (`get_dummies`).
* Exclusão segura de colunas categóricas redundantes após o processamento.

### 4. Análise de Correlação Multivariada
* Geração de matrizes de correlação de Pearson antes e depois do tratamento de dados.
* Visualização por mapas de calor (*Heatmaps*) identificando padrões ocultos fortes, como a fortíssima correlação negativa de **-0.85** entre moradia de aluguel (`Home Ownership`) e o Score de Crédito.

### 5. Particionamento e Mitigação de Vazamento de Dados (Data Leakage)
* Separação rigorosa da base de dados em **Treino (80%)** e **Teste (20%)** utilizando `train_test_split`.
* Tratamento de dados nulos da coluna de idade (`Age`) realizado de forma segura: calculando a mediana estritamente no conjunto de treino e aplicando a mesma métrica na base de teste para evitar vazamento de dados.

### 6. Detecção e Mitigação de Desbalanceamento de Classes
* Identificação de severo desbalanceamento de classes na variável alvo (68.9% da base composta por perfis de crédito *High*).
* Implementação de técnica de **Oversampling com reposição** (Amostragem Aleatória) aplicada **exclusivamente na base de treino**, igualando a representatividade de todas as classes preditoras antes da modelagem.

---

## 🛠️ Tecnologias Utilizadas

* **Python 3**
* **Pandas**: Manipulação, limpeza e engenharia de dados.
* **Matplotlib** & **Seaborn**: Visualização de dados avançada e estilização de gráficos.
* **Scikit-Learn**: Divisão de dados (`train_test_split`) e preprocessamento (`LabelEncoder`).

---

## 📊 Estrutura dos Dados Tratados

Após o pipeline de processamento, as variáveis do modelo passaram a ter a seguinte estrutura numérica:

| Nome da Coluna | Tipo de Dado | Descrição |
| :--- | :--- | :--- |
| `Age` | float | Idade do cliente (tratada com imputação de mediana). |
| `Income` | float | Renda anual/salário convertida em formato decimal contínuo. |
| `Number of Children` | int | Quantidade de filhos declarados. |
| `Gender_Encoded` | int (0 ou 1) | Gênero codificado (Ex: `Female` = 0, `Male` = 1). |
| `Marital Status_Encoded` | int (0 ou 1) | Estado civil codificado (Ex: `Married` = 0, `Single` = 1). |
| `Home Ownership_Encoded` | int (0 ou 1) | Situação de moradia codificada (Ex: `Owned` = 0, `Rented` = 1). |
| `Edu_Associate's Degree` | int (0 ou 1) | Indicador binário de nível técnico. |
| `Edu_Bachelor's Degree` | int (0 ou 1) | Indicador binário de nível superior. |
| `Edu_Doctorate` | int (0 ou 1) | Indicador binário de doutorado. |
| `Edu_High School Diploma` | int (0 ou 1) | Indicador binário de ensino médio concluído. |
| `Edu_Master's Degree` | int (0 ou 1) | Indicador binário de mestrado. |
| **`Credit_Score_Encoded`** | **int (0, 1 ou 2)** | **Variável Alvo (Target)**: `0` (Low), `1` (Average), `2` (High). |

---

## 📈 Principais Descobertas & Insights de Crédito

1. **Patrimônio Imobiliário dita o Score:** A posse de casa própria (`Home Ownership`) apresentou correlação de **-0.85** com scores menores, validando que clientes que pagam aluguel são estatisticamente mapeados em faixas de score mais baixas na amostra estudada.
2. **Escolaridade e Renda:** A titulação acadêmica de Mestrado (`Master's Degree`) foi a classe que apresentou a maior média salarial, superando inclusive os portadores de Doutorado nesta base.
3. **Casamento e Estabilidade:** Clientes casados possuem forte correlação com a aquisição de imóveis próprios e maior número de filhos, o que indiretamente correlaciona-se com perfis de menor risco financeiro.

---

## 🚀 Como Executar o Projeto

1. Clone o repositório:
   ```bash
   git clone [https://github.com/seu-usuario/seu-repositorio.git](https://github.com/seu-usuario/seu-repositorio.git)
