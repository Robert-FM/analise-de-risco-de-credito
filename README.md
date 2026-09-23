# 📊 Análise de Risco de Crédito

Projeto em andamento para análise exploratória e classificação de risco de crédito a partir do dataset `credit_risk_dataset.csv`. O repositório contém um notebook de preparação/análise estatística e outro notebook para comparação de modelos de classificação.

## 🎯 Objetivo

Explorar variáveis relacionadas a pessoas e empréstimos, tratar os dados disponíveis e avaliar modelos de machine learning para classificação do risco de crédito.

## ✨ Funcionalidades implementadas

- Leitura do dataset de risco de crédito.
- Renomeação das colunas para nomes em português.
- Padronização de nomes e variáveis categóricas.
- Remoção de registros duplicados e valores ausentes.
- Análise de valores ausentes.
- Cálculo e visualização da matriz de correlação de Pearson.
- Cálculo da distribuição da variável de status do empréstimo.
- Codificação de variáveis categóricas com `pandas.get_dummies`.
- Separação dos dados em treino e teste, com estratificação.
- Treinamento e comparação de Random Forest e XGBoost.
- Avaliação com matriz de confusão, relatório de classificação, acurácia, precisão, recall, F1-Score e ROC-AUC.
- Análise da importância das variáveis nos modelos.

## 🛠️ Tecnologias utilizadas

- Python 3.14
- Jupyter Notebook
- Pandas e NumPy
- Matplotlib, Seaborn e Plotly
- Missingno
- Scikit-learn
- XGBoost
- uv para gerenciamento do ambiente e dependências

## 🏗️ Organização do projeto

O fluxo está organizado em duas etapas principais:

1. `analise-estatistica/analise-dados.ipynb`: leitura, limpeza, padronização e análise exploratória do dataset bruto.
2. `modelos/ml-analise-sem-regressao-logistica.ipynb`: leitura dos dados processados, preparação das variáveis, treinamento e avaliação dos modelos Random Forest e XGBoost.

## 📁 Estrutura do projeto

```text
analise-risco-credito/
├── analise-estatistica/
│   └── analise-dados.ipynb
├── data/
│   ├── 01-raw/
│   │   ├── .gitkeep
│   │   └── credit_risk_dataset.csv  # arquivo local, ignorado pelo Git
│   └── 02-processed/
│       └── .gitkeep
├── modelos/
│   └── ml-analise-sem-regressao-logistica.ipynb
├── .gitignore
├── .python-version
├── pyproject.toml
├── uv.lock
└── README.md
```

- `data/01-raw/`: dados brutos de entrada. O arquivo `credit_risk_dataset.csv` é utilizado localmente e está listado no `.gitignore` para não ser versionado.
- `data/02-processed/`: destino previsto para o dataset tratado.
- `analise-estatistica/`: notebook de análise e preparação dos dados.
- `modelos/`: notebook de treinamento e comparação dos modelos.

## 📋 Pré-requisitos

- Python 3.14, conforme `.python-version` e `pyproject.toml`.
- Jupyter Notebook ou outro ambiente compatível com notebooks `.ipynb`.
- `uv`, recomendado pelo projeto, ou `pip`.

## 📦 Instalação com uv

Com o `uv` instalado, sincronize o ambiente a partir do `pyproject.toml` e do `uv.lock`:

```bash
uv sync
```

O `uv` cria o ambiente virtual em `.venv`, instala as dependências declaradas em `pyproject.toml` e usa o `uv.lock` para manter as versões reproduzíveis. Execute esse comando a partir da raiz do repositório.

### Instalar o uv

Windows PowerShell:

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

Linux/macOS:

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Feche e abra o terminal novamente, se necessário, e confirme a instalação:

```bash
uv --version
```

### Criar e sincronizar o ambiente

Na pasta do projeto, rode:

```bash
uv sync
```

O comando seleciona a versão de Python indicada em `.python-version` quando ela está disponível, cria `.venv` automaticamente e instala todas as dependências do projeto. No uso normal, não é necessário executar `pip install`.

Para atualizar as versões permitidas pelas restrições do `pyproject.toml`, faça isso explicitamente:

```bash
uv lock
uv sync
```

### Verificar a instalação

```bash
uv run python --version
uv run python -c "import pandas, sklearn, xgboost; print('Dependências carregadas com sucesso')"
```

### Executar os notebooks

O `uv run` executa o comando dentro do ambiente do projeto sem exigir ativação manual:

```bash
uv run jupyter notebook
```

Se preferir ativar o ambiente:

Windows PowerShell:

```powershell
.venv\Scripts\Activate.ps1
jupyter notebook
```

Linux/macOS:

```bash
source .venv/bin/activate
jupyter notebook
```

Se o ambiente não aparecer como kernel no Jupyter, registre-o com:

```bash
uv run python -m ipykernel install --user --name analise-risco-credito --display-name "Python (analise-risco-credito)"
```

## 🐍 Instalação com pip

Como o projeto não possui `requirements.txt`, crie e ative um ambiente virtual e instale o projeto a partir do `pyproject.toml`:

```bash
python -m venv .venv
```

Windows PowerShell:

```powershell
.venv\Scripts\Activate.ps1
python -m pip install -e .
```

Linux/macOS:

```bash
source .venv/bin/activate
python -m pip install -e .
```

## ▶️ Como executar

O projeto não possui um script de entrada ou uma CLI. A execução é feita pelos notebooks:

1. Abra `analise-estatistica/analise-dados.ipynb`.
2. Disponibilize localmente o arquivo `data/01-raw/credit_risk_dataset.csv`. Esse arquivo não é enviado ao repositório porque está ignorado pelo Git.
3. Execute as células para carregar e tratar o dataset.
4. Salve o dataframe tratado em `data/02-processed/risco-de-credito-tratados.csv` antes de executar o notebook de modelos.
5. Abra `modelos/ml-analise-sem-regressao-logistica.ipynb` e execute suas células.

Os caminhos relativos usados nos notebooks pressupõem que cada notebook seja executado a partir do seu próprio diretório.

## 📊 Modelos e avaliação

O notebook de modelos implementa Random Forest e XGBoost. Os modelos são comparados usando acurácia, precisão ponderada, recall ponderado, F1-Score ponderado e ROC-AUC multiclasse. Também são exibidas matrizes de confusão, relatórios de classificação e as quinze variáveis mais importantes.

## ⚠️ Estado atual e limitações

- O projeto está em andamento.
- O arquivo `data/01-raw/credit_risk_dataset.csv` é um dataset local e está ignorado pelo Git; ele precisa ser obtido e colocado manualmente nessa pasta para reproduzir a análise.
- O diretório `data/02-processed/` está presente, mas o arquivo `risco-de-credito-tratados.csv` ainda não está disponível; ele precisa ser gerado antes da execução do notebook de modelos.
- Não há scripts Python independentes, testes automatizados, API, aplicação web ou pipeline de CI/CD no repositório atual.
- Os resultados numéricos dos modelos são impressos durante a execução e não estão registrados em arquivos ou documentação.

## 🚀 Próximos passos

- Incorporar ao notebook a exportação do dataset tratado.
- Registrar métricas e gráficos gerados.
- Adicionar testes para preparação dos dados e avaliação dos modelos.
- Criar um pipeline reprodutível para executar as etapas sem depender exclusivamente da execução manual dos notebooks.
- Avaliar o uso do modelo em um processo de risco de crédito e em diferentes etapas do ciclo de crédito.

## 👨‍💻 Autor

**Robert Melo**

🔗 LinkedIn: [linkedin.com/in/robertdemelo](https://www.linkedin.com/in/robertdemelo/)

🐍 Python | Pandas | Scikit-learn | XGBoost | Análise de Dados | Machine Learning
