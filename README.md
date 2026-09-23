# 📊 Análise de Risco de Crédito

Projeto de análise exploratória e experimentação de modelos de classificação sobre dados de risco de crédito. O fluxo é implementado em notebooks Jupyter e cobre a preparação dos dados, a análise estatística e a comparação entre Random Forest e XGBoost.

🚧 **Status:** em desenvolvimento. Estão previstas a evolução dos modelos de risco de crédito e a futura incorporação de análises relacionadas ao ciclo de mercado.

## 🎯 Objetivo

Investigar variáveis relacionadas a pessoas e empréstimos e classificar a variável de classificação de crédito a partir de dados tabulares de risco de crédito.

O projeto está organizado em duas etapas: tratamento/análise exploratória do dataset bruto e treinamento/avaliação dos modelos de machine learning.

## ✨ Funcionalidades

- Leitura do dataset bruto `credit_risk_dataset.csv`.
- Renomeação das colunas originais para nomes em português.
- Normalização de nomes e valores categóricos.
- Remoção de registros duplicados e valores ausentes.
- Inspeção de valores ausentes e cálculo da correlação de Pearson.
- Análise da distribuição da variável de status do empréstimo.
- Codificação de variáveis categóricas com `pandas.get_dummies`.
- Divisão estratificada dos dados em treino e teste, com `test_size=0.2` e `random_state=42`.
- Treinamento de Random Forest e XGBoost em pipelines com imputação pela mediana.
- Avaliação por matriz de confusão, relatório de classificação, acurácia, precisão, recall, F1-score e ROC-AUC multiclasse.
- Comparação dos modelos por ROC-AUC e inspeção das importâncias das variáveis.

## 🏗️ Fluxo de processamento

1. `analise-estatistica/analise-dados.ipynb` lê `data/01-raw/credit_risk_dataset.csv`, renomeia e normaliza as colunas, remove duplicidades e valores ausentes e realiza a análise exploratória.
2. O dataframe tratado deve ser exportado manualmente para `data/02-processed/risco-de-credito-tratados.csv`.
3. `modelos/ml-analise-sem-regressao-logistica.ipynb` lê o CSV tratado, transforma variáveis categóricas, separa treino e teste, treina os modelos e exibe as métricas e importâncias.

O segundo notebook considera a coluna de classificação de crédito como variável-alvo. Os modelos configurados utilizam 200 estimadores; o XGBoost usa `learning_rate=0.05`, `max_depth=4` e `eval_metric="logloss"`.

## 📁 Estrutura do projeto

```text
analise-risco-credito/
├── analise-estatistica/
│   └── analise-dados.ipynb
├── modelos/
│   └── ml-analise-sem-regressao-logistica.ipynb
├── data/
│   ├── 01-raw/
│   │   └── .gitkeep
│   └── 02-processed/
│       └── .gitkeep
├── .gitignore
├── .python-version
├── pyproject.toml
├── uv.lock
└── README.md
```

Os arquivos CSV são dados locais: o dataset bruto é ignorado pelo `.gitignore` e não está presente no estado versionado analisado.

## 📋 Pré-requisitos

- Python 3.14, conforme `.python-version` e `pyproject.toml` (`>=3.14`).
- `uv` ou `pip`.
- Jupyter Notebook para executar os notebooks.
- O arquivo de entrada `credit_risk_dataset.csv` em `data/01-raw/`.

Não há banco de dados, API, serviço externo, Docker, CI/CD ou variáveis de ambiente configurados no projeto.

## 📦 Instalação

### ⚡ Opção 1 — uv (recomendada)

Instale o `uv` seguindo a documentação oficial ou, no Windows PowerShell, execute:

```powershell
irm https://astral.sh/uv/install.ps1 | iex
```

No Linux/macOS:

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Na raiz do repositório, sincronize o ambiente:

```bash
uv sync
```

O `uv sync` cria o ambiente virtual `.venv`, instala as dependências declaradas em `pyproject.toml` e utiliza as versões registradas em `uv.lock`. O projeto não define grupos ou extras de desenvolvimento.

O Jupyter não está declarado como dependência do projeto. Para abrir os notebooks sem alterar o `pyproject.toml`, execute:

```bash
uv run --with jupyter notebook
```

Os comandos podem ser executados diretamente com `uv run`, sem ativar manualmente o ambiente:

```bash
uv run python --version
uv run --with jupyter notebook
```

Se quiser ativar o ambiente explicitamente:

Windows PowerShell:

```powershell
.venv\Scripts\Activate.ps1
```

Linux/macOS:

```bash
source .venv/bin/activate
```

Para adicionar uma dependência ao projeto durante o desenvolvimento, use:

```bash
uv add nome-do-pacote
```

### 🐍 Opção 2 — pip

Crie e ative um ambiente virtual:

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

Como não há `requirements.txt`, instale as dependências declaradas no projeto e o Jupyter:

```bash
python -m pip install "missingno>=0.5.2" "pandas>=3.0.3" "plotly>=6.7.0" "scikit-learn>=1.8.0" "seaborn>=0.13.2" "xgboost>=3.2.0" jupyter
```

## ▶️ Como executar

1. Coloque `credit_risk_dataset.csv` em `data/01-raw/`.
2. Abra `analise-estatistica/analise-dados.ipynb` e execute as células a partir do diretório `analise-estatistica/`, pois o notebook usa caminhos relativos.
3. Exporte manualmente o dataframe tratado para `data/02-processed/risco-de-credito-tratados.csv`.
4. Abra `modelos/ml-analise-sem-regressao-logistica.ipynb` e execute as células a partir do diretório `modelos/`.

Para iniciar o Jupyter com `uv`:

```bash
uv run --with jupyter notebook
```

Com `pip`, use:

```bash
jupyter notebook
```

## 🛠️ Tecnologias e dependências

- Python 3.14.
- Jupyter Notebook para os experimentos interativos.
- Pandas e NumPy para manipulação dos dados.
- Missingno para inspeção de valores ausentes.
- Matplotlib, Seaborn e Plotly para visualização.
- Scikit-learn para divisão dos dados, pipelines, imputação, Random Forest e métricas.
- XGBoost para o modelo de gradient boosting.
- uv para gerenciamento e lock das dependências.

As dependências diretas e suas versões mínimas estão em `pyproject.toml`; as versões resolvidas estão em `uv.lock`.

## ✅ Testes e resultados

Não há testes automatizados. A validação disponível ocorre durante a execução do notebook de modelos, que imprime as métricas, as matrizes de confusão, os relatórios de classificação, a tabela de comparação e as importâncias das variáveis.

O repositório não contém métricas ou gráficos persistidos como artefatos. Portanto, não são apresentados resultados numéricos fixos neste README.

## ⚠️ Limitações observadas

- Os datasets de entrada e saída não estão versionados.
- A exportação do CSV tratado é manual.
- Não há script ou CLI para automatizar o fluxo.
- Não há persistência de modelos, métricas ou gráficos.
- Não há testes automatizados nem pipeline de CI/CD.

## 🚀 Possíveis melhorias

- Automatizar a exportação do dataset tratado.
- Extrair as etapas de preparação e treinamento para scripts ou módulos reutilizáveis.
- Persistir modelos, métricas e visualizações.
- Adicionar testes automatizados e uma rotina de execução para as duas etapas.

## 👨‍💻 Autor

**Robert Melo**

🔗 LinkedIn: [linkedin.com/in/robertdemelo](https://www.linkedin.com/in/robertdemelo/)

🐍 Python | Pandas | Scikit-learn | XGBoost | Análise de Dados | Machine Learning
