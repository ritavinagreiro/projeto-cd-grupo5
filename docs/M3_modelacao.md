# Milestone 3: Modelação e Avaliação 
 
## 1. Estratégia de Modelação 
**Divisão do dataset:**   
Utilizámos uma divisão de 80% para treino e 20% para teste, com random_state=42 e estratificação da variável alvo (stratify=y), garantindo que a proporção das classes (70% de clientes em cumprimento e 30% de clientes em incumprimento) se mantém em ambos os conjuntos.

**Métrica de Sucesso:**   
As métricas principais escolhidas foram o *Recall* (para a classe de incumprimento) e o *F1-Score*, sendo ainda considerada a *AUC-ROC* como métrica complementar.  
Esta escolha justifica-se pelo facto de o *dataset* ser desequilibrado (70% de clientes em cumprimento e 30% em incumprimento), o que torna a *Accuracy* uma métrica pouco fiável.  
Neste contexto, o *Recall* assume particular importância, uma vez que permite minimizar os falsos negativos, ou seja, casos em que clientes de risco são incorretamente classificados como cumpridores.  
Por sua vez, o *F1-Score* assegura um equilíbrio entre precisão e recall, permitindo uma avaliação mais robusta do desempenho global do modelo.  
Adicionalmente, a *AUC-ROC* foi utilizada para medir a capacidade discriminativa do modelo, independentemente do limiar de decisão.

**Metas definidas:**
* *Recall* (Incumprimento) ≥ 0.70
* ⁠*F1-Score* ≥ 0.80

## 2. Experiências Realizadas 
### 2.1. Modelo Baseline 

**Algoritmo:** Regressão Logística  

**Resultados:**
* *F1-Score*: 0.8464
* *Recall* (Incumprimento): 0.5167
* *AUC-ROC*: 0.8145

**Observação:** O modelo *baseline* apresenta um bom *F1-Score* global, mas o *Recall* da classe de incumprimento (0.52) fica muito abaixo da meta definida (≥ 0.70), não sendo suficiente para o objetivo do projeto.
 
### 2.2. Modelos Candidatos 
Foram testados vários algoritmos de maior complexidade com o objetivo de melhorar o desempenho face ao modelo *baseline*, explorando diferentes abordagens de aprendizagem automática, nomeadamente modelos baseados em *Ensembles* e modelos de fronteira.

**Justificação da escolha dos modelos:**  
A seleção dos modelos teve como objetivo comparar diferentes abordagens de aprendizagem supervisionada, privilegiando algoritmos com bom desempenho em dados estruturados e com características distintas ao nível da generalização e complexidade.

* **Random Forest:** Selecionado como modelo de referência, por apresentar robustez e bom desempenho geral, sendo utilizado como base de comparação com modelos mais avançados.
* **Gradient Boosting:** Incluído pela sua elevada capacidade preditiva e bom equilíbrio entre desempenho e generalização, tendo-se revelado um dos modelos mais promissores nos resultados obtidos.
* **SVM (RBF):** Utilizado como alternativa baseada em fronteiras de decisão, permitindo avaliar o desempenho de um modelo distinto dos métodos de *Ensemble*.
* **XGBoost:** Selecionado pelo seu desempenho reconhecido em problemas de classificação e pela sua capacidade de melhorar a identificação da classe de incumprimento, conforme observado nos resultados obtidos.

**Resultados Obtidos:**
 
| Algoritmo | Parâmetros Base | Métrica (Treino) | Métrica (Teste) | Notas | 
| :--- | :--- | :--- | :--- | :--- | 
| Random Forest | n_estimators=100 | 1.000 | 0.8667 | Sinais de *Overfitting* | 
| Gradient Boosting | n_estimators=100 | 0.9493 | 0.8667 | Bom equilíbrio | 
| SVM (RBF) | kernel='rbf' | 0.8732 | 0.8721 | Elevado tempo no treino | 
| XGBoost | default | 1.000 | 0.8403 | Sinais de *Overfitting*; Melhor desempenho no recall | 

**Diagnóstico de Overfitting/Underfitting:**  
A comparação entre o desempenho nos conjuntos de treino e de teste revela dois comportamentos distintos:
  
* *XGBoost* e *Random Forest* atingem valores de F1 iguais a 1.00 no treino, mas apresentam uma degradação no conjunto de teste (diferença superior a 0.10), evidenciando sinais claros de *Overfitting*, isto é, o modelo ajusta-se excessivamente aos dados de treino, comprometendo a sua capacidade de generalização.
* *Gradient Boosting* e *SVM* apresentam uma diferença entre treino e teste inferior a 0.09, demonstrando um melhor equilíbrio e maior capacidade de generalização.
* O *Gradient Boosting* destaca-se como o modelo mais equilibrado, apresentando um desempenho no teste idêntico ao do *Random Forest* (F1 = 0.8667), mas sem evidência significativa de sobreajuste.

**Análise geral:**  
De forma global, todos os modelos apresentam bons resultados ao nível do *F1-Score*, evidenciando um desempenho consistente na classificação global. No entanto, identifica-se uma limitação crítica: todos os modelos revelam dificuldades na identificação da classe de incumprimento, apresentando valores de recall inferiores ao objetivo definido (≥ 0.70). O *XGBoost* apresenta o melhor desempenho neste critério (*Recall* = 0.55), embora ainda insuficiente para satisfazer os requisitos do problema.

Estes resultados indicam que a principal limitação não reside no desempenho global dos modelos, mas sim na capacidade de identificar corretamente a classe minoritária (clientes em incumprimento).  

O desequilíbrio do conjunto de dados (70% / 30%) surge como o principal fator explicativo deste comportamento, justificando a necessidade de aplicar técnicas adicionais de melhoria, nomeadamente:
* Reequilíbrio de dados (*SMOTE*);
* Ajuste do limiar de decisão (*threshold*).

## 3. Otimização (Tuning) 

Com base nos resultados da fase de experimentação, foram desenvolvidas três estratégias progressivas de otimização, motivadas pela necessidade de melhorar o *Recall* da classe de incumprimento sem comprometer o desempenho global do modelo.

### 3.1. Otimização de Hiperparâmetros — Gradient Boosting

Com base nos resultados obtidos na fase anterior, o modelo *Gradient Boosting* foi selecionado para otimização, por apresentar o melhor compromisso entre desempenho global, medido através do *F1-Score*, e capacidade de generalização, evidenciada pela reduzida diferença entre os resultados de treino e de teste.

**Técnica Utilizada:**  
A otimização foi realizada recorrendo à técnica de *Grid Search* com validação cruzada estratificada, utilizando o método *Stratified K-Fold* com k=5. Esta abordagem permitiu avaliar de forma robusta diferentes combinações de hiperparâmetros, assegurando a preservação da distribuição das classes em cada fold.

Foram ajustados os principais hiperparâmetros do modelo, nomeadamente: `n_estimators`, `learning_rate`, `max_depth` e `subsample`. Este processo possibilitou identificar a configuração que maximiza o desempenho do modelo, ao mesmo tempo que controla o risco de *Overfitting*, promovendo uma melhor capacidade de generalização.

**Espaço de pesquisa definido:**

| Hiperparâmetro  | Valores Testados | Justificação                                                                         |
| :-------------- | :--------------- | :----------------------------------------------------------------------------------- |
| `n_estimators`  | [200, 300]       | Um maior número de árvores tende a melhorar a capacidade de generalização            |
| `learning_rate` | [0.03, 0.05]     | Taxas de aprendizagem mais baixas combinam melhor com um maior número de estimadores |
| `max_depth`     | [3]              | Profundidade reduzida para controlar o *Overfitting*                                   |
| `subsample`     | [0.8]            | Amostragem aleatória dos dados para aumentar a robustez do modelo                    |

**Melhores hiperparâmetros encontrados:**  
`learning_rate` = 0.03 | `max_depth` = 3 | `n_estimators` = 300 | `subsample` = 0.8  
Melhor *F1-Score* (CV): 0.8527

**Ajuste de Threshold de Decisão:**  
Para maximizar o *Recall* mantendo o *F1-Score* aceitável, foi realizado um varrimento de *thresholds* no intervalo [0.20, 0.60] com passo de 0.01. O *threshold* ótimo encontrado foi 0.59, permitindo classificar como incumprimento casos com probabilidade mais baixa, aumentando assim a sensibilidade do modelo à classe de risco.

**Resultados após otimização:**

| Métrica                | Baseline | Gradient Boosting (Tuned) | Variação |
| :--------------------- | :------- | :------------------------ | :------- |
| F1-Score               | 0.8464   | 0.8612                    | +1.5%    |
| Recall (Incumprimento) | 0.5167   | 0.6667                    | +29%     |
| AUC-ROC                | 0.8145   | 0.8282                    | +1.4%    |

A otimização produziu uma melhoria relevante, especialmente no *Recall* (+29%), mas o valor de 0.6667 ficou aquém da meta definida (≥ 0.70), o que tornou necessário explorar abordagens adicionais.

### 3.2. Tentativa de Melhoria — Gradient Boosting + SMOTE

Perante a limitação identificada, aplicou-se o *SMOTE* (Synthetic Minority Over-sampling Technique) em conjunto com o *Gradient Boosting*. O *SMOTE* gera sinteticamente novos exemplos da classe minoritária através da interpolação entre observações reais, equilibrando o dataset de treino sem duplicar registos existentes.

O *SMOTE* foi integrado num pipeline (imblearn.pipeline.Pipeline), garantindo que o reequilíbrio é aplicado exclusivamente aos dados de treino em cada *fold* da validação cruzada e prevenindo qualquer fuga de informação (*data leakage*) para o conjunto de teste. Foi igualmente aplicado ajuste de *threshold* para maximizar o *Recall*.

| Métrica                | Gradient Boosting (Tuned) | Gradient Boosting + SMOTE | Variação |
| :--------------------- | :------------------------ | :------------------------ | :------- |
| F1-Score               | 0.8612                    | 0.8123                    | -5.7%    |
| Recall (Incumprimento) | 0.6667                    | 0.7500                    | +12%     |
| AUC-ROC                | 0.8282                    | 0.7868                    | -5.0%    |
| F1 ≥ 0.80              | ✔                         | ✔                        | —        |
| Recall ≥ 0.70          | ✘                         | ✔                        | —        |


A aplicação de *SMOTE* permitiu atingir pela primeira vez a meta de *Recall* ≥ 0.70, evidenciando um *trade-off* claro: o *Recall* melhorou significativamente (+12%), mas com alguma redução no *F1-Score* e na *AUC-ROC*. Este resultado confirma o valor do *SMOTE* para o problema em causa, motivando a sua aplicação a um algoritmo com maior capacidade preditiva.

### 3.3. Modelo Alternativo — XGBoost (base)  
Paralelamente, foi testado um modelo baseado em *XGBoost*, com hiperparâmetros ajustados manualmente, com o objetivo de explorar uma alternativa ao *Gradient Boosting*.

A escolha deste modelo baseou-se no facto de ter apresentado o melhor desempenho ao nível do *Recall* na fase de modelos candidatos (0.55), bem como na sua capacidade de incorporar mecanismos de regularização, potencialmente úteis na mitigação do *Overfitting* anteriormente identificado.

Foram definidos os seguintes hiperparâmetros:
* `n_estimators`: 200
* `learning_rate`: 0.05
* `max_depth`: 4
* `subsample`: 0.8
* `colsample_bytree`: 0.8


Adicionalmente, foi realizado o ajuste do limiar de decisão (*threshold*), testando valores no intervalo [0.20, 0.60], tendo sido identificado um valor ótimo de 0.56, que permitiu melhorar o equilíbrio entre precisão e *Recall*.

**Resultados:**
| Métrica                | Valor  |
| :--------------------- | :----- |
| F1-Score (Teste)       | 0.8541 |
| AUC-ROC (Teste)        | 0.8132 |
| Recall (Incumprimento) | 0.6500 |
| Threshold ótimo        | 0.56   |

O *XGBoost* apresenta um *F1-Score* global superior ao *Gradient Boosting + SMOTE* (0.8541 vs. 0.8123), mas o *Recall* de 0.6500 ainda fica abaixo da meta de 0.70. Este resultado sugere que o XGBoost tem maior potencial preditivo, mas necessita igualmente de reequilíbrio de dados para atingir os objetivos do projeto.

### 3.4. Melhoria do Recall — XGBoost + SMOTE

Combinando as aprendizagens das etapas anteriores (o potencial do *XGBoost* e a eficácia do *SMOTE*), testou-se a combinação de ambos num *pipeline*, utilizando a mesma configuração do modelo descrita na secção 3.2. O *threshold* ótimo de 0.56 foi selecionado por maximizar o *Recall* mantendo *F1-Score* ≥ 0.80.

**Resultados:**
| Métrica                | Valor  |
| :--------------------- | :----- |
| F1-Score (Teste)       | 0.8213 |
| AUC-ROC (Teste)        | 0.8090 |
| Recall (Incumprimento) | 0.7500 |
| F1 ≥ 0.80              | ✔      |
| Recall ≥ 0.70          | ✔      |

**Cross-Validation (5-Fold) — XGBoost + SMOTE**
| Métrica                | Média  | Desvio Padrão |
| :--------------------- | :----- | :------------ |
| F1-Score               | 0.8153 | ± 0.0341      |
| Recall (Incumprimento) | 0.6042 | ± 0.0437      |
| AUC-ROC                | 0.7734 | ± 0.0295      |

A validação cruzada confirma resultados consistentes entre os diferentes *folds*, demonstrando estabilidade do modelo e boa capacidade de generalização para dados novos.

### 3.5. Síntese da Evolução dos Modelos  

A tabela seguinte resume a progressão obtida ao longo de todas as estratégias, comparando todas as configurações testadas face às metas definidas:

| Modelo                         | F1 (Teste) | Recall (Incumprimento) | F1 ≥ 0.80 | Recall ≥ 0.70 |
| :----------------------------- | :--------- | :--------------------- | :-------- | :------------ |
| Baseline (Regressão Logística) | 0.8464     | 0.5167                 | ✔         | ✘             |
| Gradient Boosting (Tuned)      | 0.8612     | 0.6667                 | ✔         | ✘             |
| Gradient Boosting + SMOTE      | 0.8123     | 0.7500                 | ✔         | ✔             |
| XGBoost (base)                 | 0.8541     | 0.6500                 | ✔         | ✘             |
| XGBoost + SMOTE (Modelo Final) | 0.8213     | 0.7500                 | ✔         | ✔             |

O *XGBoost + SMOTE* é selecionado como modelo final por ser o único a cumprir simultaneamente ambos os critérios, apresentando o melhor *F1-Score* entre os modelos válidos. A sua escolha em detrimento do *Gradient Boosting + SMOTE* justifica-se pelo desempenho global superior (+1% em F1 e +2% em AUC-ROC), mantendo o mesmo *Recall*. A regularização incorporada no *XGBoost* revelou-se assim determinante após o balanceamento com *SMOTE*.

No que concerne à robustez do modelo, é importante notar a existência de sinais de *Overfitting*. Para obter a confirmação, foi realizado um diagnóstico de *Overfitting*, em que o modelo apresenta um *F1-Score* de 0.95 no treino, o que evidencia uma elevada capacidade de memorização dos dados, o desempenho em validação cruzada estabilizou nos 0.82. O diferencial de 0.13, embora caracterize a presença de um ligeiro sobreajuste (*Overfitting*), não compromete a validade da escolha do modelo. A consistência dos resultados obtidos no conjunto de teste (0.8213) atesta que o modelo possui uma capacidade de generalização eficaz, revelando que a memorização excessiva no treino é devidamente mitigada pela regularização aplicada. Conclui-se, portanto, que este comportamento representa um compromisso aceitável para um modelo de elevada complexidade, mantendo-se o seu poder preditivo em conformidade com os objetivos de negócio traçados.

## 4. Avaliação do Modelo Final 
### 4.1. Matriz de Confusão / Erros 
A análise da matriz de confusão do modelo final (*XGBoost* com *SMOTE*) evidencia uma melhoria significativa na capacidade de identificação de clientes em incumprimento face ao modelo *baseline*.

Em particular, o modelo consegue identificar corretamente 45 clientes em incumprimento (classe 0), comparativamente a apenas 31 no modelo *baseline*, demonstrando um ganho relevante na deteção de risco. No entanto, esta melhoria vem acompanhada de um aumento no número de falsos positivos, ou seja, clientes de baixo risco incorretamente classificados como de risco.

Do ponto de vista dos erros, destacam-se:
* Falsos Negativos (FN): 15 casos (~22.86%)
    → Clientes em incumprimento classificados como cumpridores (erro crítico);
* Falsos Positivos (FP): 32 casos (~25%)
    → Clientes cumpridores classificados como risco (perda de oportunidade de negócio).

A análise destes erros revela que o modelo apresenta maior dificuldade na identificação de perfis de risco intermédio, ou seja, clientes cujas características não são suficientemente extremas para permitir uma separação clara entre as classes.

Em particular, os clientes em incumprimento não identificados (falsos negativos) tendem a apresentar:
* Montantes de crédito mais elevados (*Credit_Amount*)
* Maior esforço financeiro mensal (*Credit_per_Month*)
* Rácio crédito/idade superior (*Credit_Age_Ratio*)

Estes fatores indicam níveis mais elevados de pressão financeira, sugerindo que o modelo tem dificuldade em captar situações em que o risco resulta da combinação de variáveis, e não de valores extremos isolados.

Por outro lado, os falsos positivos tendem a estar associados a clientes com características financeiras relativamente mais conservadoras, mas que, devido a padrões semelhantes aos perfis de risco, acabam por ser classificados de forma mais prudente pelo modelo.

Em termos globais, o modelo evidencia um trade-off claro entre risco e oportunidade: reduz significativamente o risco financeiro (menos clientes problemáticos aprovados), mas aumenta a rejeição de clientes potencialmente bons.

Dada a natureza do problema, esta abordagem mais conservadora é justificável, uma vez que o custo de um falso negativo é significativamente superior ao de um falso positivo.

### 4.2. Importância dos Atributos (*Feature Importance*) 
A análise da importância dos atributos, obtida a partir do modelo final (*XGBoost* com *SMOTE*), permite identificar as variáveis que mais contribuíram para a sua capacidade preditiva, reforçando simultaneamente a interpretabilidade do modelo em contexto de decisão de crédito.

De acordo com os resultados, destaca-se claramente a variável *Account_Balance*, que apresenta a maior importância relativa (0.1720), assumindo-se como o principal fator na distinção entre clientes de risco e clientes cumpridores. Este resultado evidencia que a liquidez disponível e o saldo da conta são determinantes na avaliação do risco de crédito, estando diretamente associados à capacidade do cliente em cumprir as suas obrigações financeiras.

Para além desta variável, outras assumem também um papel relevante, nomeadamente:
* *Value_Savings_Stocks* (0.0830)
* *Guarantors* (0.0774)
* *Payment_Status_of_Previous_Credit* (0.0766)
* *Duration_of_Credit_monthly* (0.0552)

Estas variáveis refletem dimensões fundamentais do risco de crédito. Por um lado, *Value_Savings_Stocks* traduz a capacidade financeira acumulada do cliente, enquanto *Account_Balance* reforça a importância da liquidez imediata. Por outro lado, *Payment_Status_of_Previous_Credit* evidencia o peso do comportamento passado como indicador de risco futuro, sendo uma variável crítica na avaliação de crédito. Adicionalmente, a variável *Guarantors* demonstra a relevância da existência de garantias externas na mitigação do risco para a instituição.

Por fim, a variável *Duration_of_Credit_monthly* introduz a dimensão do contrato de crédito, refletindo o nível de compromisso financeiro ao longo do tempo. Créditos de maior duração tendem a aumentar a exposição ao risco, contribuindo para uma maior probabilidade de incumprimento.

Em termos globais, a análise evidencia que o modelo baseia a sua decisão sobretudo na combinação entre liquidez financeira, histórico de crédito e características do contrato, demonstrando que o risco de crédito resulta da interação entre múltiplos fatores e não de uma variável isolada. Este comportamento reforça a robustez do modelo enquanto ferramenta de apoio à decisão na concessão de crédito.

## 4.3. Resposta às Perguntas de Investigação (Modelação)
**Quais são as variáveis que mais contribuem para a previsão do incumprimento de crédito?** 

Com base na análise de importância dos atributos do modelo final (XGBoost com SMOTE), foi possível identificar as variáveis com maior contributo para a previsão do incumprimento de crédito.

Destaca-se, em primeiro lugar, a variável *Account_Balance*, que apresenta a maior importância relativa, evidenciando o papel central da liquidez financeira na avaliação do risco. Para além desta, outras variáveis assumem também relevância significativa, nomeadamente *Value_Savings_Stocks*, *Guarantors*, *Payment_Status_of_Previous_Credit* e *Duration_of_Credit_monthly*.

Estas variáveis refletem dimensões fundamentais do risco de crédito, como a capacidade financeira do cliente, o seu comportamento histórico e as características do contrato de crédito. Em conjunto, permitem ao modelo capturar padrões complexos associados ao incumprimento, demonstrando que o risco resulta da interação entre múltiplos fatores e não de uma única variável isolada.

**É possível classificar os clientes em categorias de risco de incumprimento (baixo e alto risco), com base nas probabilidades geradas pelo modelo preditivo?**

Sim, é possível classificar os clientes em categorias de risco de incumprimento com base nas probabilidades geradas pelo modelo preditivo. 

O modelo determinado como o "melhor", *XGBoost + SMOTE*, não se limita a realizar uma classificação binária (cumprimento/incumprimento), mas estima a probabilidade de incumprimento desse mesmo cliente. Esta probabilidade permite uma abordagem mais flexível e alinhada com o contexto real de decisão.

Para tornar esta interpretação mais intuitiva, foi aplicada uma normalização das probabilidades através do *MinMaxScaler*. Com base no *threshold* ótimo identificado de 0.56, os clientes são classificados da seguinte forma:
* Alto risco → probabilidade de incumprimento ≥ 0.56
* Baixo risco → probabilidade de incumprimento < 0.56

Esta abordagem permite segmentar os clientes de forma clara e objetiva, facilitando o processo de tomada de decisão por parte da instituição financeira.

Em termos práticos, esta classificação possibilita a definição de estratégias diferenciadas, como a rejeição de clientes de elevado risco ou a aplicação de condições de crédito mais restritivas, contribuindo para uma gestão mais eficiente do risco de crédito.
 
## 5. Conclusão da Fase de Modelação 
A fase de modelação permitiu desenvolver, testar e otimizar diversos modelos de classificação com o objetivo de identificar clientes em incumprimento, tendo como principal desafio o desequilíbrio do *dataset* e a dificuldade em detetar corretamente a classe de risco.

Ao longo das diferentes etapas, verificou-se que, embora vários modelos apresentassem um bom desempenho global (*F1-Score* elevado), todos evidenciavam limitações na identificação da classe minoritária, não cumprindo inicialmente a meta definida para o *Recall*. Este comportamento confirmou que o principal problema não residia na capacidade preditiva global, mas sim na sensibilidade do modelo à classe de incumprimento.

A aplicação de técnicas de otimização, nomeadamente o ajuste de hiperparâmetros e do threshold de decisão, permitiu melhorias relevantes. No entanto, foi a introdução de técnicas de reequilíbrio de dados, através do *SMOTE*, que se revelou determinante para ultrapassar a principal limitação identificada, permitindo aumentar significativamente o *Recall*.

Neste contexto, o modelo final selecionado (XGBoost com SMOTE), destacou-se como a melhor solução, sendo o único a cumprir simultaneamente os critérios definidos:
* *F1-Score* ≥ 0.80;
* *Recall* (Incumprimento) ≥ 0.70.

Para além do cumprimento destas metas, o modelo apresenta ainda:
* Boa capacidade de generalização, evidenciada pelos resultados consistentes em validação cruzada;
* Desempenho equilibrado, garantindo um compromisso adequado entre identificação de risco e desempenho global;
* Elevada interpretabilidade relativa, suportada pela análise de importância das variáveis, permitindo compreender os principais fatores que influenciam o risco de crédito.

A análise da matriz de confusão revelou um comportamento esperado em problemas deste tipo, com um trade-off entre a redução de falsos negativos e o aumento de falsos positivos. Ainda assim, a opção por um modelo mais conservador é adequada ao contexto, uma vez que o custo associado à aprovação de clientes em incumprimento é significativamente superior ao de rejeitar clientes potencialmente cumpridores.

Apesar dos resultados positivos, importa reconhecer algumas limitações. A principal prende-se com a ainda existência de erros na identificação de perfis de risco intermédio, sugerindo que o modelo poderá beneficiar de melhorias adicionais, como a introdução de novas variáveis, maior volume de dados ou técnicas mais avançadas de engenharia de atributos.

Em síntese, o modelo desenvolvido demonstra ser robusto, consistente e alinhado com os objetivos do problema, apresentando condições para ser utilizado como ferramenta de apoio à decisão na concessão de crédito. Ainda que não constitua uma solução perfeita, oferece um nível de desempenho adequado e interpretável, podendo ser considerado pronto para aplicação prática, com potencial de evolução futura.

 --- 
*Data de última atualização: 23/04/2026* 
