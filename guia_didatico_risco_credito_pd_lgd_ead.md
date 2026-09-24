# 💳 Risco de Crédito com PD, LGD e EAD
### Um guia didático para quem está entrando na área de Ciência de Dados

> 🎯 **Objetivo deste material:** entender o problema de negócio antes de pensar no algoritmo.  
> Você não precisa vir da área financeira para começar a trabalhar com modelos de risco de crédito.

---

## 🧭 1. Comece por aqui: a ideia em 30 segundos

Em risco de crédito, queremos responder a três perguntas:

| Sigla | Pergunta em linguagem simples | O que estima |
|---|---|---|
| 🎲 **PD** | Qual a chance de o cliente entrar em uma situação grave de inadimplência? | Probabilidade |
| 💸 **LGD** | Se isso acontecer, qual percentual do dinheiro exposto será perdido? | Percentual de perda |
| 💰 **EAD** | Quanto dinheiro estará exposto quando isso acontecer? | Valor em dinheiro |

Depois combinamos os três:

> 🧮 **Perda Esperada (EL) = PD × LGD × EAD**

### 🧠 Regra para memorizar

**PD = chance** → **LGD = tamanho da perda** → **EAD = dinheiro exposto**

---

## 📚 2. Mini glossário: traduzindo o “bancariês”

Se você não vem da área financeira, volte a este quadro sempre que necessário.

| Termo | Tradução para quem está começando |
|---|---|
| **Crédito** | Dinheiro ou limite que uma instituição disponibiliza e espera receber de volta. |
| **Operação de crédito** | Um empréstimo, financiamento, cartão ou outra relação específica de crédito. |
| **Carteira de crédito** | Conjunto de operações de crédito que estamos analisando. |
| **Inadimplência** | O cliente deixou de cumprir uma obrigação de pagamento. |
| **Default** | O cliente atingiu a condição de inadimplência que foi definida como relevante para aquele modelo/projeto. |
| **Exposição** | Quanto dinheiro está sujeito ao risco naquela operação. |
| **Recuperação** | Quanto a instituição consegue receber após o default. |
| **Garantia** | Bem, direito ou mecanismo que pode ajudar a reduzir a perda. |
| **Score de crédito** | Uma pontuação relacionada ao risco de crédito segundo determinado modelo. |
| **Target / alvo** | Aquilo que o modelo de ML está tentando prever. |
| **Feature** | Variável usada pelo modelo para realizar a previsão. |
| **Calibração** | Verifica se as probabilidades previstas correspondem razoavelmente ao que ocorre na prática. |
| **Drift** | Mudança nos dados ou em suas relações ao longo do tempo. |

### 🚨 Atenção: default não significa simplesmente “atrasou um dia”

Para modelagem, **default precisa ter uma definição**.

Quando você ler:

> “O cliente entrou em default.”

traduza mentalmente como:

> **“O cliente atingiu a condição que o projeto definiu como evento de default.”**

Em um dataset, poderíamos ter:

```text
default = 1  → ocorreu default
default = 0  → não ocorreu default
```

Esse campo pode ser o **target** de um modelo de PD.

---

## 🎲 3. PD — Probability of Default

### ❓ O que queremos descobrir?

> **Qual é a probabilidade de ocorrer default?**

Imagine que o modelo produza:

> **PD = 8%**

Isso significa que, para aquele perfil/operação e horizonte considerado, a probabilidade estimada de default é **8%**.

### 🤖 Onde entra Machine Learning?

Podemos utilizar dados históricos como:

- renda;
- endividamento;
- score;
- atrasos anteriores;
- utilização do limite;
- tempo de relacionamento;
- características da operação.

O problema pode ser representado assim:

```text
Features do cliente/operação
            ↓
       Modelo de PD
            ↓
Probabilidade de default
            ↓
           8%
```

### 🧪 Algoritmos possíveis

Podemos testar, por exemplo:

- Regressão Logística;
- Random Forest;
- XGBoost;
- LightGBM;
- Redes Neurais.

> 💡 **Para Ciência de Dados:** PD é o que queremos estimar.  
> XGBoost, Regressão Logística etc. são ferramentas que podemos usar para estimá-la.

A **Regressão Logística** é uma referência clássica e pode funcionar como **baseline** para comparação com modelos mais complexos.

---

## 💸 4. LGD — Loss Given Default

### ❓ O que queremos descobrir?

> **Se o default ocorrer, qual percentual da exposição será perdido?**

Imagine:

```text
Exposição no default      R$ 100.000
Valor recuperado        - R$  60.000
                         -----------
Perda                      R$  40.000
```

De forma simplificada:

> **LGD = 40.000 ÷ 100.000 = 40%**

Portanto:

> **LGD = 40%**

### 🧠 Tradução mental

Se ocorreu default e havia **R$ 100 mil expostos**, uma LGD de **40%** significa que a estimativa de perda corresponde a 40% dessa exposição, segundo a metodologia adotada.

### 🔍 O que pode influenciar a LGD?

- garantias;
- tipo de produto;
- características da operação;
- processo de cobrança e recuperação;
- perfil do cliente;
- histórico de recuperação.

```text
Características da operação
          +
Dados de recuperação
          ↓
     Modelo de LGD
          ↓
   Severidade da perda
          ↓
         40%
```

> ⚠️ **Importante:** este é um exemplo simplificado. Modelos reais de LGD podem considerar custos, tempo de recuperação e outros fatores.

---

## 💰 5. EAD — Exposure at Default

### ❓ Primeiro: o que significa “exposição”?

Em linguagem simples:

> **Exposição = quanto dinheiro está sujeito ao risco.**

Se o cliente deve R$ 30.000:

```text
Cliente deve R$ 30.000
        ↓
Há aproximadamente R$ 30.000
sujeitos ao risco de crédito
```

### ❓ Então o que é EAD?

**EAD — Exposure at Default** pergunta:

> **Quanto estará exposto no momento em que ocorrer o default?**

Isso é particularmente importante em produtos com limite disponível.

### 💳 Exemplo com cartão

```text
Limite total              R$ 50.000
Valor utilizado hoje      R$ 20.000
Limite ainda disponível   R$ 30.000
```

O cliente ainda pode utilizar parte dos R$ 30 mil disponíveis antes do default.

Suponha que o modelo estime:

> **EAD = R$ 35.000**

```text
Hoje
R$ 20.000 utilizados
        ↓
Cliente utiliza mais crédito
        ↓
Momento do default
R$ 35.000 expostos
        ↑
       EAD
```

Em algumas metodologias aparece também o **CCF (Credit Conversion Factor)**, relacionado à estimativa de quanto do limite ainda não utilizado pode se transformar em exposição.

---

## 🧩 6. Então são três modelos de ML?

### ✅ Normalmente, pensamos em modelos separados

Isso acontece porque **PD, LGD e EAD possuem objetivos diferentes**:

```text
                    DADOS
                      │
          ┌───────────┼───────────┐
          ↓           ↓           ↓
      Modelo PD   Modelo LGD   Modelo EAD
          ↓           ↓           ↓
         8%          35%       R$ 50.000
          │           │           │
          └───────────┼───────────┘
                      ↓
              PD × LGD × EAD
                      ↓
               Perda Esperada
```

### ⚠️ Mas “modelos diferentes” não significa “algoritmos diferentes”

Podemos ter:

```text
PD  → XGBoost
LGD → XGBoost
EAD → XGBoost
```

São **três modelos distintos**, mesmo usando o mesmo algoritmo, porque foram treinados para estimar alvos diferentes.

Também poderíamos ter:

```text
PD  → Regressão Logística
LGD → LightGBM
EAD → XGBoost
```

A escolha depende dos dados, do problema, do desempenho, da interpretabilidade, da governança e de outros requisitos.

---

## 🧮 7. Juntando tudo: Perda Esperada

Suponha que os modelos produzam:

| Componente | Resultado |
|---|---:|
| 🎲 PD | 8% |
| 💸 LGD | 35% |
| 💰 EAD | R$ 50.000 |

A relação é:

> **EL = PD × LGD × EAD**

Substituindo:

> **EL = 0,08 × 0,35 × 50.000**

Resultado:

> 💵 **EL = R$ 1.400**

### 🗣️ Traduzindo

- existe uma **probabilidade de 8%** de default;
- se ocorrer default, estima-se uma **perda de 35%** da exposição;
- estima-se que haverá **R$ 50 mil expostos**;
- combinando os três componentes, temos uma **perda esperada de R$ 1.400**.

> ⚠️ Isso **não significa** que exatamente R$ 1.400 será perdido naquela operação individual. É uma estimativa probabilística.

---

## 🛠️ 8. Não basta treinar três modelos e multiplicar

A fórmula é simples:

> **PD × LGD × EAD = EL**

Mas o trabalho de Ciência de Dados não termina nela.

```text
📦 Dados históricos
        ↓
🧹 Preparação dos dados
        ↓
🔎 Análise exploratória
        ↓
🧱 Feature Engineering
        ↓
🤖 Treinamento dos modelos
        ↓
🧪 Validação
        ↓
🎯 Calibração e estabilidade
        ↓
🎲 PD + 💸 LGD + 💰 EAD
        ↓
🧮 Perda Esperada
        ↓
📡 Monitoramento
```

Um erro importante em qualquer componente pode afetar a estimativa final.

---

## 📊 9. Como avaliar um modelo de PD?

Aqui entram conceitos bastante relevantes para vagas de Ciência de Dados em risco.

### 📈 ROC-AUC

Avalia a capacidade do modelo de **discriminar** clientes que entram em default daqueles que não entram.

- **AUC = 0,50:** discriminação equivalente ao acaso;
- valores maiores indicam maior capacidade de discriminação.

> 💡 **AUC não responde tudo.** Um modelo pode ordenar muito bem os clientes e ainda produzir probabilidades mal calibradas.

### 📐 Gini

Na definição usual derivada da ROC:

> **Gini = 2 × AUC − 1**

Exemplo:

> AUC = 0,80  
> Gini = 2 × 0,80 − 1 = **0,60**

### ↔️ KS

O **Kolmogorov-Smirnov (KS)** é usado para analisar a separação entre as distribuições de bons e maus clientes.

### 🎯 Calibração

Imagine que o modelo atribua aproximadamente **10% de PD** a um grande grupo de operações semelhantes.

A pergunta é:

> **Na prática, a frequência observada de default nesse grupo é compatível com aproximadamente 10%?**

Essa é a ideia intuitiva de calibração.

### 🧠 Uma distinção importante

**Discriminação** pergunta:

> “O modelo consegue ordenar clientes de menor para maior risco?”

**Calibração** pergunta:

> “As probabilidades previstas correspondem razoavelmente às frequências observadas?”

São problemas diferentes.

---

## 🔎 10. Explicabilidade com SHAP

Suponha que um XGBoost produza:

> **PD = 8,7%**

Naturalmente surge a pergunta:

> **Por que o modelo chegou a essa previsão?**

O SHAP pode ajudar a investigar quais variáveis contribuíram para aumentar ou reduzir a saída do modelo.

```text
Atrasos anteriores       → aumenta o risco
Alto endividamento       → aumenta o risco
Uso elevado do limite    → aumenta o risco
Tempo de relacionamento  → reduz o risco
```

> ⚠️ **SHAP explica o comportamento do modelo; não prova causalidade.**

Além disso, valores SHAP não devem ser automaticamente interpretados como pontos percentuais de PD. A interpretação depende da escala e da configuração do explicador.

---

## 👨‍💻 11. Onde entra o Cientista de Dados?

Um projeto de risco de crédito pode exigir várias competências:

| Etapa | Conhecimentos |
|---|---|
| 🗄️ Extração | SQL |
| 🧹 Tratamento | Python / Pandas |
| 🔎 EDA | Estatística e visualização |
| 🧱 Features | Feature Engineering |
| 🎲 PD | Classificação e probabilidades |
| 💸 LGD | Modelagem da severidade da perda |
| 💰 EAD | Modelagem da exposição |
| 🤖 ML | Regressão Logística, XGBoost, LightGBM etc. |
| 🧪 Validação | ROC-AUC, KS, Gini, calibração |
| 🔎 Explicabilidade | SHAP |
| ⚙️ Produção | Pipelines / MLOps |
| 📡 Monitoramento | Performance, estabilidade e drift |

### 🌊 O que é drift?

O modelo aprende utilizando dados de determinado período.

Depois, podem mudar:

- perfil dos clientes;
- produtos;
- comportamento de consumo;
- cenário econômico;
- relação entre as variáveis.

**Drift** é uma forma de descrever essas mudanças nos dados ou em suas relações.

Por isso, trabalhar com risco de crédito envolve:

> 🧠 **Estatística + 🤖 Machine Learning + 💼 Conhecimento de Negócio**

---

## 🚀 12. Exemplo de projeto para estudar e colocar no portfólio

Uma sequência interessante seria:

```text
1. 📦 Dataset de crédito
        ↓
2. 🔎 EDA e tratamento
        ↓
3. 🧱 Feature Engineering
        ↓
4. 📉 Regressão Logística como baseline
        ↓
5. 🤖 XGBoost / LightGBM
        ↓
6. ⚖️ Comparação dos modelos
        ↓
7. 📊 ROC-AUC + KS + Gini
        ↓
8. 🎯 Calibração
        ↓
9. 🔎 Explicabilidade com SHAP
        ↓
10. 🎲 Estimativa de PD
        ↓
11. 💸 Modelagem de LGD
        ↓
12. 💰 Modelagem de EAD
        ↓
13. 🧮 PD × LGD × EAD
        ↓
14. 💵 Perda Esperada
        ↓
15. 📡 Monitoramento
```

Esse projeto demonstra não apenas que você sabe treinar um algoritmo, mas que entende **o problema de negócio que o modelo precisa resolver**.

---

## 👩‍💼 13. Uma história completa para fixar

Imagine uma cliente chamada **Ana**.

### 🎲 Passo 1 — PD

O modelo estima:

> **PD = 10%**

Tradução:

> Existe uma probabilidade estimada de 10% de Ana atingir a condição definida como default no horizonte considerado.

### 💰 Passo 2 — EAD

Se o default ocorrer, o modelo estima:

> **EAD = R$ 50.000**

Tradução:

> No momento do default, estima-se que haverá R$ 50 mil expostos.

### 💸 Passo 3 — LGD

O modelo estima:

> **LGD = 40%**

Tradução:

> Se ocorrer default, estima-se uma perda correspondente a 40% da exposição.

### 🧮 Passo 4 — Perda Esperada

> **EL = 0,10 × 0,40 × 50.000**

> 💵 **EL = R$ 2.000**

Visualmente:

```text
🎲 Qual a chance de ocorrer default?
              ↓
            PD = 10%

💰 Se ocorrer, quanto estará exposto?
              ↓
        EAD = R$ 50.000

💸 Da exposição, quanto se espera perder?
              ↓
           LGD = 40%

              ↓
🧮 10% × 40% × R$ 50.000

              ↓
💵 PERDA ESPERADA = R$ 2.000
```

> ⚠️ Os R$ 2.000 representam uma **estimativa probabilística de perda esperada**, e não uma afirmação de que Ana deixará de pagar exatamente esse valor.

---

## 🗺️ 14. Mapa mental para ler uma vaga de Cientista de Dados

Quando aparecerem termos de risco de crédito em uma vaga, tente pensar nesta sequência:

```text
💼 PROBLEMA DE NEGÓCIO
        ↓
Risco de o cliente não pagar
        ↓
💳 CONCEITOS DE RISCO
        ↓
PD + LGD + EAD
        ↓
📦 PROBLEMA DE DADOS
        ↓
Target + Features + População + Período
        ↓
🤖 MODELAGEM
        ↓
Regressão Logística / XGBoost / LightGBM
        ↓
📊 AVALIAÇÃO
        ↓
AUC + KS + Gini + Calibração + Estabilidade
        ↓
🔎 EXPLICAÇÃO
        ↓
SHAP / análise das variáveis
        ↓
⚙️ PRODUÇÃO E MONITORAMENTO
```

### 🔑 Antes de perguntar “qual algoritmo usar?”, pergunte:

1. **O que o negócio quer estimar?**
2. **Qual é o target do modelo?**
3. **Quais features estavam disponíveis antes do evento que queremos prever?**
4. **Como avaliar se a previsão é útil e confiável?**
5. **Como monitorar o modelo depois de colocado em uso?**

---

## 🧠 15. Resumo final para memorizar

| Conceito | Tradução mental | Resultado |
|---|---|---:|
| 🎲 **PD** | Qual a chance de ocorrer default? | % |
| 💸 **LGD** | Se ocorrer, qual percentual será perdido? | % |
| 💰 **EAD** | Quanto estará exposto quando ocorrer? | R$ |
| 💵 **EL** | Qual é a perda esperada? | R$ |

### 🧮 Fórmula central

> **EL = PD × LGD × EAD**

### 🤖 E onde entra a IA?

```text
                 🤖 MACHINE LEARNING
                         │
             ┌───────────┼───────────┐
             ↓           ↓           ↓
          🎲 PD        💸 LGD      💰 EAD
             │           │           │
             └───────────┼───────────┘
                         ↓
                 💵 PERDA ESPERADA
```

> 🔑 **Frase-chave:** PD, LGD e EAD definem **o que queremos estimar** no risco de crédito. Regressão Logística, XGBoost, LightGBM e outros modelos estatísticos/de Machine Learning são **ferramentas que podemos utilizar para realizar essas estimativas**.
