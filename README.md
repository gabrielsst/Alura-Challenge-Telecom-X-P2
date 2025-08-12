# 📊 Telecom X - Parte 2 — Previsão de Churn

## 🎯 Propósito do Projeto
Este projeto tem como objetivo prever a evasão (*churn*) de clientes de uma operadora de telecomunicações com base em variáveis relevantes, como tipo de contrato, tempo de permanência, serviços contratados e formas de pagamento.  
A análise visa identificar fatores críticos que influenciam a saída dos clientes, permitindo a criação de estratégias de retenção mais eficazes.

---

## 📂 Estrutura do Projeto
```
Telecom_X_P2/
│
├── Challenge_Telecom_X_P2.ipynb   # Notebook principal com todo o fluxo de análise e modelagem
├── df_cleaned.csv                  # Base de dados tratada e limpa
├── visualizations/                 # (Opcional) Pasta com gráficos gerados na EDA
└── README.md                       # Documentação do projeto
```

---

## 🛠️ Preparação dos Dados

### 1. Classificação das Variáveis
- **Categóricas Binárias:** `gender`, `Partner`, `Dependents`, `PhoneService`, `PaperlessBilling`, `Churn`, etc.  
- **Categóricas Não Binárias:** `InternetService`, `Contract`, `PaymentMethod`, etc.  
- **Numéricas:** `tenure`, `Charges.Monthly`, `Charges.Total`, `Contas_Diarias`, etc.

### 2. Etapas de Pré-Processamento
1. **Remoção de colunas irrelevantes:** `customerID` (identificador único).
2. **Codificação:**
   - Variáveis binárias convertidas para 0 e 1.
   - Variáveis categóricas não binárias transformadas via *One-Hot Encoding*.
3. **Balanceamento de classes:**
   - *Undersampling* da classe majoritária para reduzir desbalanceamento entre clientes que evadiram e os que permaneceram.
4. **Normalização:**
   - *StandardScaler* aplicado aos dados para a Regressão Logística (não necessário para Random Forest).

### 3. Separação Treino/Teste
- Conjuntos separados em treino e teste para avaliação justa do desempenho.

---

## 📈 Modelagem e Justificativas
Foram utilizados dois modelos principais:
1. **Regressão Logística:** Pela interpretabilidade e adequação a problemas binários.
2. **Random Forest:** Pela robustez, capacidade de lidar com não linearidades e menor necessidade de pré-processamento.

Normalização foi aplicada apenas para a Regressão Logística devido à sensibilidade deste modelo à escala dos dados.

---

## 📊 Análise Exploratória de Dados (EDA) — Exemplos de Insights
- **Tenure**: Clientes mais novos tendem a evadir mais.
- **Contract**: Contratos mensais têm maior taxa de churn.
- **InternetService (Fiber Optic)**: Associado a maior evasão.
- **Serviços como Online Security e Tech Support**: Ausência aumenta o risco de churn.
- **PaymentMethod (Electronic Check)**: Ligado a maior taxa de evasão.

Exemplos de gráficos gerados:
- Matriz de correlação para identificar variáveis mais relacionadas ao churn.
- Histogramas e *countplots* para variáveis categóricas e numéricas.
- Comparações de churn entre diferentes tipos de contrato.

---

## 🚀 Como Executar o Projeto no Google Colab

### 1. Abrir o Notebook
Faça o upload do arquivo `Challenge_Telecom_X_P2.ipynb` e do dataset `df_cleaned.csv` para o Google Colab.

### 2. Instalar e Importar Bibliotecas
No início do notebook, execute o seguinte código para instalar (caso não estejam no ambiente) e importar todas as bibliotecas necessárias:

```python
# Instalação das bibliotecas (caso não estejam no Colab)
!pip install pandas numpy scikit-learn seaborn matplotlib

# Importação das bibliotecas
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt

from sklearn.preprocessing import OneHotEncoder, StandardScaler
from sklearn.utils import resample
from sklearn.linear_model import LogisticRegression
from sklearn.ensemble import RandomForestClassifier
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score, precision_score, recall_score, f1_score, confusion_matrix, classification_report
```

### 3. Carregar o Dataset
```python
df = pd.read_csv("df_cleaned.csv")
df.head()
```

### 4. Executar as Células do Notebook
Basta seguir a execução célula a célula para reproduzir todo o fluxo de análise e modelagem.

---

## 📌 Próximos Passos
- Realizar ajuste fino de hiperparâmetros.
- Testar outros algoritmos (XGBoost, LightGBM).
- Criar dashboards interativos para stakeholders.
- Implementar estratégias de retenção baseadas nos insights.
