# 📊 Análise de Risco de Crédito

Projeto de análise exploratória e experimentação de modelos de classificação para dados de risco de crédito. O fluxo é realizado em notebooks Jupyter e cobre a preparação dos dados, a análise estatística e a comparação entre Random Forest e XGBoost.

## 🎯 Objetivo

Investigar variáveis relacionadas a pessoas e empréstimos e avaliar modelos capazes de classificar o risco de crédito a partir da coluna `classificação_de_crédito`.

O projeto está em desenvolvimento e depende de arquivos CSV locais, que não estão versionados neste repositório.

## ✨ Funcionalidades

- Leitura do dataset bruto `credit_risk_dataset.csv`.
- Renomeação e padronização de colunas e variáveis categóricas.
- Remoção de duplicidades e valores ausentes.
- Inspeção de valores ausentes e correlação de Pearson.
- Análise da distribuição de `status_do_empréstimo`.
- Codificação de variáveis categóricas com `pandas.get_dummies`.
- Divisão estratificada dos dados em treino e teste.
- Treinamento de Random Forest e XGBoost usando pipelines com imputação pela mediana.
- Avaliação por matriz de confusão, relatório de classificação, acurácia, precisão, recall, F1-score e ROC-AUC multiclasse.
- Inspeção da importância das variáveis nos dois modelos.

## 🏗️ Organização do fluxo

1. `analise-estatistica/analise-dados.ipynb` lê o dataset bruto, renomeia colunas, remove duplicidades e valores ausentes, realiza análises exploratórias e prepara os dados.
2. `modelos/ml-analise-sem-regressao-logistica.ipynb` lê o CSV processado, codifica as variáveis, treina os modelos e imprime métricas e importâncias.

O segundo notebook espera `data/02-processed/risco-de-credito-tratados.csv`. O notebook de análise não exporta esse arquivo automaticamente; ele precisa ser gerado manualmente a partir do dataframe tratado.

## 📁 Estrutura do projeto

```text
analise-risco-credito/
├── analise-estatistica/
│   └── analise-dados.ipynb
├── modelos/
│   └── ml-analise-sem-regressao-logistica.ipynb
├── .gitignore
├── .python-version
├── pyproject.toml
├── uv.lock
└── README.md
```

Os notebooks usam `data/01-raw/` e `data/02-processed/`. Esses diretórios e CSVs não estão presentes no estado versionado analisado. O arquivo bruto é ignorado pelo `.gitignore`.

## 📋 Pré-requisitos

- Python 3.14, conforme `.python-version` e `pyproject.toml` (`>=3.14`).
- `uv` ou `pip`.
- Um ambiente capaz de executar notebooks Jupyter.
- Os arquivos CSV locais esperados pelos notebooks.

Não há banco de dados, serviço externo, Docker, API, pipeline de CI/CD ou variáveis de ambiente configurados.

## 📦 Instalação com uv

O projeto possui `pyproject.toml` e `uv.lock`. Na raiz do repositório:

```bash
uv sync
uv run python --version
```

Jupyter não está declarado no projeto. Para abrir os notebooks sem alterar os arquivos:

```bash
uv run --with jupyter notebook
```

## 🐍 Instalação com pip

```bash
python -m venv .venv
```

Windows PowerShell:

```powershell
.venv\Scripts\Activate.ps1
```

Linux/macOS:

```bash
source .venv/bin/activate
```

Como não há `requirements.txt`, instale as dependências declaradas no `pyproject.toml` e Jupyter:

```bash
python -m pip install "missingno>=0.5.2" "pandas>=3.0.3" "plotly>=6.7.0" "scikit-learn>=1.8.0" "seaborn>=0.13.2" "xgboost>=3.2.0" jupyter
```

## ▶️ Como executar

1. Crie `data/01-raw/` e coloque nela `credit_risk_dataset.csv`.
2. Abra `analise-estatistica/analise-dados.ipynb`.
3. Execute as células a partir do diretório do próprio notebook, pois os caminhos são relativos a ele.
4. Exporte o dataframe tratado para `data/02-processed/risco-de-credito-tratados.csv`.
5. Abra `modelos/ml-analise-sem-regressao-logistica.ipynb` e execute suas células a partir de `modelos/`.

Com `pip`, inicie o ambiente com `jupyter notebook`; com `uv`, use `uv run --with jupyter notebook`.

## 🧰 Tecnologias e dependências principais

- Python 3.14 e Jupyter Notebook.
- Pandas e NumPy para manipulação dos dados.
- Missingno para inspeção de valores ausentes.
- Matplotlib, Seaborn e Plotly para visualização.
- Scikit-learn para divisão dos dados, pipelines, imputação, Random Forest e métricas.
- XGBoost para o modelo XGBoost.
- uv para gerenciamento das dependências.

As versões mínimas estão em `pyproject.toml`; as versões resolvidas estão em `uv.lock`.

## ✅ Testes

Não há testes automatizados. A validação ocorre durante a execução dos notebooks, por meio das análises e métricas impressas.

## ⚠️ Limitações atuais

- Os datasets de entrada e saída não estão versionados.
- A exportação do CSV processado é manual.
- Não há script ou CLI para automatizar o fluxo.
- Métricas e gráficos não são persistidos como artefatos.
- Não há testes automatizados nem CI/CD.

## 🚀 Possíveis melhorias

- Automatizar a exportação do dataset tratado.
- Separar preparação e treinamento em módulos ou scripts reutilizáveis.
- Persistir métricas e gráficos.
- Adicionar testes e um fluxo automatizado para as duas etapas.

## 👨‍💻 Autor

**Robert Melo**

🔗 LinkedIn: [linkedin.com/in/robertdemelo](https://www.linkedin.com/in/robertdemelo/)

🐍 Python | Pandas | Scikit-learn | XGBoost | Análise de Dados | Machine Learning
