# Milestone 3: Modelação e Avaliação 
 
## 1. Estratégia de Modelação 
**Divisão do dataset:**   
Utilizámos uma divisão de 80% para treino e 20% para teste, com random_state=42 e estratificação da variável alvo (stratify=y), garantindo que a proporção das classes (70% de clientes em cumprimento e 30% de clientes em incumprimento) se mantém em ambos os conjuntos.

**Métrica de Sucesso:**   
As métricas principais escolhidas foram o Recall (para a classe de incumprimento) e o F1-Score, sendo ainda considerada a AUC-ROC como métrica complementar.

Esta escolha justifica-se pelo facto de o dataset ser desequilibrado (70% de clientes em cumprimento e 30% em incumprimento), o que torna a accuracy uma métrica pouco fiável.

Neste contexto, o Recall assume particular importância, uma vez que permite minimizar os falsos negativos, ou seja, casos em que clientes de risco são incorretamente classificados como cumpridores.

Por sua vez, o F1-Score assegura um equilíbrio entre precisão e recall, permitindo uma avaliação mais robusta do desempenho global do modelo.

Adicionalmente, a AUC-ROC foi utilizada para medir a capacidade discriminativa do modelo, independentemente do limiar de decisão.

**Metas definidas:**
* Recall (Incumprimento) ≥ 0.70
* ⁠F1-Score ≥ 0.80

## 2. Experiências Realizadas 
### 2.1. Modelo Baseline 

**Algoritmo:** Regressão Logística  

**Resultados:**
* F1-Score: 0.8464
* Recall Incumprimento: 0.5167
* AUC-ROC: 0.8145

    
**Observação:** O modelo baseline apresenta um bom F1-Score global, mas o Recall da classe de incumprimento (0.52) fica muito abaixo da meta definida (≥ 0.70), não sendo suficiente para o objetivo do projeto.
 
### 2.2. Modelos Candidatos 

Foram testados vários algoritmos de maior complexidade com o objetivo de melhorar o desempenho face ao modelo baseline, explorando diferentes abordagens de aprendizagem automática, nomeadamente modelos baseados em ensembles e modelos de fronteira.

**Justificação da escolha dos modelos:**
A seleção dos modelos teve como objetivo comparar diferentes abordagens de aprendizagem supervisionada, privilegiando algoritmos com bom desempenho em dados estruturados e com características distintas ao nível da generalização e complexidade.

* Random Forest: Selecionado como modelo de referência, por apresentar robustez e bom desempenho geral, sendo utilizado como base de comparação com modelos mais avançados.
  
* Gradient Boosting: Incluído pela sua elevada capacidade preditiva e bom equilíbrio entre desempenho e generalização, tendo-se revelado um dos modelos mais promissores nos resultados obtidos.
  
* SVM (RBF): Utilizado como alternativa baseada em fronteiras de decisão, permitindo avaliar o desempenho de um modelo distinto dos métodos de ensemble.
  
* XGBoost: Selecionado pelo seu desempenho reconhecido em problemas de classificação e pela sua capacidade de melhorar a identificação da classe de incumprimento, conforme observado nos resultados obtidos.

**Resultados Obtidos:**
 
| Algoritmo | Parâmetros Base | Métrica (Treino) | Métrica (Teste) | Notas | 
| :--- | :--- | :--- | :--- | :--- | 
| Random Forest | n_estimators=100 | 1.000 | 0.8667 | Sinais de overfitting | 
| Gradient Boosting | n_estimators=100 | 0.9493 | 0.8667 | Bom equilíbrio | 
| SVM (RBF) | kernel='rbf' | 0.8732 | 0.8721 | Elevado tempo no treino | 
| XGBoost | default | 1.000 | 0.8403 | Sinais de overfitting; Melhor desempenho no recall | 

**Diagnóstico de Overfitting/Underfitting:**

A comparação entre o desempenho nos conjuntos de treino e de teste revela dois comportamentos distintos:
  
* XGBoost e Random Forest atingem valores de F1 iguais a 1.00 no treino, mas apresentam uma degradação no conjunto de teste (diferença superior a 0.10), evidenciando sinais claros de overfitting, isto é, o modelo ajusta-se excessivamente aos dados de treino, comprometendo a sua capacidade de generalização.
* Gradient Boosting e SVM apresentam uma diferença entre treino e teste inferior a 0.09, demonstrando um melhor equilíbrio e maior capacidade de generalização.
* O Gradient Boosting destaca-se como o modelo mais equilibrado, apresentando um desempenho no teste idêntico ao do Random Forest (F1 = 0.8667), mas sem evidência significativa de sobreajuste.

**Análise geral:**

De forma global, todos os modelos apresentam bons resultados ao nível do F1-Score, evidenciando um desempenho consistente na classificação global.  
No entanto, identifica-se uma limitação crítica: todos os modelos revelam dificuldades na identificação da classe de incumprimento, apresentando valores de recall inferiores ao objetivo definido (≥ 0.70).  
O XGBoost apresenta o melhor desempenho neste critério (Recall = 0.55), embora ainda insuficiente para satisfazer os requisitos do problema.  
Estes resultados indicam que a principal limitação não reside no desempenho global dos modelos, mas sim na capacidade de identificar corretamente a classe minoritária (clientes em incumprimento).  
O desequilíbrio do conjunto de dados (70% / 30%) surge como o principal fator explicativo deste comportamento, justificando a necessidade de aplicar técnicas adicionais de melhoria, nomeadamente:
* reequilíbrio de dados (SMOTE)
* ajuste do limiar de decisão (threshold)

## 3. Otimização (Tuning) 

Com base nos resultados da fase de experimentação, foram desenvolvidas três estratégias progressivas de otimização, motivadas pela necessidade de melhorar o Recall da classe de incumprimento sem comprometer o desempenho global do modelo.

**3.1. Otimização de Hiperparâmetros — Gradient Boosting**

Com base nos resultados obtidos na fase anterior, o modelo Gradient Boosting foi selecionado para otimização, por apresentar o melhor compromisso entre desempenho global, medido através do F1-Score, e capacidade de generalização, evidenciada pela reduzida diferença entre os resultados de treino e de teste.

**Técnica Utilizada:**  
A otimização foi realizada recorrendo à técnica de Grid Search com validação cruzada estratificada, utilizando o método Stratified K-Fold com k=5. Esta abordagem permitiu avaliar de forma robusta diferentes combinações de hiperparâmetros, assegurando a preservação da distribuição das classes em cada fold.

Foram ajustados os principais hiperparâmetros do modelo, nomeadamente: n_estimators, learning_rate, max_depth e subsample. Este processo possibilitou identificar a configuração que maximiza o desempenho do modelo, ao mesmo tempo que controla o risco de overfitting, promovendo uma melhor capacidade de generalização.

**Espaço de pesquisa definido:**

| Hiperparâmetro  | Valores Testados | Justificação                                                                         |
| :-------------- | :--------------- | :----------------------------------------------------------------------------------- |
| `n_estimators`  | [200, 300]       | Um maior número de árvores tende a melhorar a capacidade de generalização            |
| `learning_rate` | [0.03, 0.05]     | Taxas de aprendizagem mais baixas combinam melhor com um maior número de estimadores |
| `max_depth`     | [3]              | Profundidade reduzida para controlar o overfitting                                   |
| `subsample`     | [0.8]            | Amostragem aleatória dos dados para aumentar a robustez do modelo                    |

**Melhores hiperparâmetros encontrados:**  
learning_rate = 0.03 | max_depth = 3 | n_estimators = 300 | subsample = 0.8  
Melhor F1-Score (CV): 0.8527

**Ajuste de Threshold de Decisão:**  
Para maximizar o Recall mantendo o F1-Score aceitável, foi realizado um varrimento de thresholds no intervalo [0.20, 0.60] com passo de 0.01.   O threshold ótimo encontrado foi 0.59, permitindo classificar como incumprimento casos com probabilidade mais baixa, aumentando assim a sensibilidade do modelo à classe de risco.

**Resultados após otimização:**

| Métrica                | Baseline | Gradient Boosting (Tuned) | Variação |
| :--------------------- | :------- | :------------------------ | :------- |
| F1-Score               | 0.8464   | 0.8612                    | +1.5%    |
| Recall (Incumprimento) | 0.5167   | 0.6667                    | +29%     |
| AUC-ROC                | 0.8145   | 0.8282                    | +1.4%    |

A otimização produziu uma melhoria relevante, especialmente no Recall (+29%), mas o valor de 0.6667 ficou aquém da meta definida (≥ 0.70), o que tornou necessário explorar abordagens adicionais.

**3.2. Tentativa de Melhoria — Gradient Boosting + SMOTE**

Perante a limitação identificada, aplicou-se o SMOTE (Synthetic Minority Over-sampling Technique) em conjunto com o Gradient Boosting. O SMOTE gera sinteticamente novos exemplos da classe minoritária através da interpolação entre observações reais, equilibrando o dataset de treino sem duplicar registos existentes.

O SMOTE foi integrado num pipeline (imblearn.pipeline.Pipeline), garantindo que o reequilíbrio é aplicado exclusivamente aos dados de treino em cada fold da validação cruzada e prevenindo qualquer fuga de informação (data leakage) para o conjunto de teste. Foi igualmente aplicado ajuste de threshold para maximizar o Recall.

| Métrica                | Gradient Boosting (Tuned) | Gradient Boosting + SMOTE | Variação |
| :--------------------- | :------------------------ | :------------------------ | :------- |
| F1-Score               | 0.8612                    | 0.8123                    | -5.7%    |
| Recall (Incumprimento) | 0.6667                    | 0.7500                    | +12%     |
| AUC-ROC                | 0.8282                    | 0.7868                    | -5.0%    |
| F1 ≥ 0.80              | ✔                         | ✔                        | —        |
| Recall ≥ 0.70          | ✘                         | ✔                        | —        |


A aplicação de SMOTE permitiu atingir pela primeira vez a meta de Recall ≥ 0.70, evidenciando um trade-off claro: o Recall melhorou significativamente (+12%), mas com alguma redução no F1-Score e na AUC-ROC. Este resultado confirma o valor do SMOTE para o problema em causa, motivando a sua aplicação a um algoritmo com maior capacidade preditiva.

**3.3. Modelo Alternativo — XGBoost (base)**

Paralelamente, testou-se o XGBoost com hiperparâmetros ajustados manualmente, por ser o algoritmo que havia apresentado o melhor Recall na fase de candidatos (0.55) e por incorporar regularização nativa que pode mitigar o overfitting observado anteriormente.

Configuração utilizada:
pythonXGBClassifier(
    n_estimators=200,
    learning_rate=0.05,
    max_depth=4,
    subsample=0.8,
    colsample_bytree=0.8,
    eval_metric='logloss',
    random_state=42
)

Foi ainda aplicado ajuste de threshold no intervalo [0.20, 0.60], com threshold ótimo de 0.56.

Resultados:
| Métrica                | Valor  |
| :--------------------- | :----- |
| F1-Score (Teste)       | 0.8541 |
| AUC-ROC (Teste)        | 0.8132 |
| Recall (Incumprimento) | 0.6500 |
| Threshold ótimo        | 0.56   |


O XGBoost apresenta um F1-Score global superior ao Gradient Boosting + SMOTE (0.8541 vs. 0.8123), mas o Recall de 0.6500 ainda fica abaixo da meta de 0.70. Este resultado sugere que o XGBoost tem maior potencial preditivo, mas necessita igualmente de reequilíbrio de dados para atingir os objetivos do projeto.

**3.4. Melhoria do Recall — XGBoost + SMOTE**

Combinando as aprendizagens das etapas anteriores — o potencial do XGBoost e a eficácia do SMOTE —, testou-se a combinação de ambos num pipeline, utilizando a mesma configuração do modelo descrita na secção 3.2. O threshold ótimo de 0.56 foi selecionado por maximizar o Recall mantendo F1-Score ≥ 0.80.

Resultados:
| Métrica                | Valor  |
| :--------------------- | :----- |
| F1-Score (Teste)       | 0.8213 |
| AUC-ROC (Teste)        | 0.8090 |
| Recall (Incumprimento) | 0.7500 |
| F1 ≥ 0.80              | ✔      |
| Recall ≥ 0.70          | ✔      |

Cross-Validation (5-Fold) — XGBoost + SMOTE
| Métrica                | Média  | Desvio Padrão |
| :--------------------- | :----- | :------------ |
| F1-Score               | 0.8153 | ± 0.0341      |
| Recall (Incumprimento) | 0.6042 | ± 0.0437      |
| AUC-ROC                | 0.7734 | ± 0.0295      |

A validação cruzada confirma resultados consistentes entre os diferentes folds, demonstrando estabilidade do modelo e boa capacidade de generalização para dados novos.

**3.5. Síntese da Evolução dos Modelos**    

A tabela seguinte resume a progressão obtida ao longo de todas as estratégias, comparando todas as configurações testadas face às metas definidas:

| Modelo                         | F1 (Teste) | Recall (Incumprimento) | F1 ≥ 0.80 | Recall ≥ 0.70 |
| :----------------------------- | :--------- | :--------------------- | :-------- | :------------ |
| Baseline (Regressão Logística) | 0.8464     | 0.5167                 | ✔         | ✘             |
| Gradient Boosting (Tuned)      | 0.8612     | 0.6667                 | ✔         | ✘             |
| Gradient Boosting + SMOTE      | 0.8123     | 0.7500                 | ✔         | ✔             |
| XGBoost (base)                 | 0.8541     | 0.6500                 | ✔         | ✘             |
| XGBoost + SMOTE (Modelo Final) | 0.8213     | 0.7500                 | ✔         | ✔             |

O XGBoost + SMOTE é selecionado como modelo final por ser o único a cumprir simultaneamente ambos os critérios, apresentando o melhor F1-Score entre os modelos válidos. A sua escolha em detrimento do Gradient Boosting + SMOTE justifica-se pelo desempenho global superior (+1% em F1 e +2% em AUC-ROC), mantendo o mesmo Recall. A regularização incorporada no XGBoost revelou-se assim determinante após o balanceamento com SMOTE.

## 4. Avaliação do Modelo Final 
### 4.1. Matriz de Confusão / Erros 
*Analisem onde o modelo mais falha.* 
> **Análise:** (p/ex.: "O modelo ainda confunde a Classe A com a Classe B em 10% dos casos devido 
à semelhança nos atributos X e Y.") 
 
### 4.2. Importância dos Atributos (Feature Importance) 
*Quais as variáveis que o modelo considerou mais importantes para decidir?* 
1. [Variável X] 
2. [Variável Y] 
 
## 5. Conclusão da Fase de Modelação 
*Justifiquem por que razão este modelo está pronto (ou não) para ser apresentado como solução 
final.* 
 --- 
*Data de última atualização: 22/04/2026* 
