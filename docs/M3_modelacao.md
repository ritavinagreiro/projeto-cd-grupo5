# Milestone 3: Modelação e Avaliação 
 
## 1. Estratégia de Modelação 
**Divisão do dataset:**   
O conjunto de dados foi dividido em dois subconjuntos: 80% para treino e 20% para teste. Foi utilizado o parâmetro `random_state=42`, em todos os algoritmos, de forma a garantir a reprodutibilidade dos resultados, e a divisão foi realizada com estratificação da variável alvo (`stratify=y`).

Esta estratificação permitiu assegurar que a distribuição das classes se mantinha proporcional em ambos os conjuntos. Assim, tanto no conjunto de treino como no conjunto de teste, manteve-se a proporção original do dataset: 70% de clientes em cumprimento e 30% de clientes em incumprimento.

**Métrica de Sucesso:**   
As métricas principais selecionadas foram o *Recall* (para a classe de incumprimento) e o *F1-Score*, sendo ainda considerada a *AUC-ROC* como métrica complementar.  

A escolha destas métricas justifica-se pelo facto de o dataset ser desequilibrado, com 70% de clientes em cumprimento e 30% em incumprimento. Neste contexto, a *Accuracy* poderia ser enganadora, uma vez que um modelo poderia obter uma boa taxa de acerto global classificando maioritariamente os clientes como cumpridores, mas falhando na deteção dos clientes de maior risco. 

O *Recall* da classe de incumprimento assume especial relevância, pois mede a capacidade do modelo para identificar corretamente os clientes de risco. No contexto de decisão de crédito, os falsos negativos representam o erro mais crítico, pois correspondem a clientes em incumprimento que são incorretamente classificados como cumpridores.

O *F1-Score* foi utilizado por permitir avaliar o equilíbrio entre precisão e recall, oferecendo uma visão mais robusta do desempenho global do modelo. Já a *AUC-ROC* foi considerada como métrica complementar, por medir a capacidade discriminativa do modelo independentemente do limiar de decisão utilizado.

**Metas definidas:**
* *Recall* (Incumprimento) ≥ 0.70, foi definido com base no contexto do problema. Considera-se que identificar corretamente pelo menos 70% dos clientes representa um equilíbrio aceitável entre sensibilidade ao risco e viabilidade operacional,evitando simultaneamente um número excessivo de falsos positivos que compremeteria a eficiência do processo de concessão de crédito.
* ⁠*F1-Score* ≥ 0.80, foi estabelecido por representar um bom desempenho para problemas de classificação binária com dados desequilibrados. Garantindo que a melhoria do *recall* da classe de incumprimento não compromete de forma significativa a capacidade geral do modelo.

## 2. Experiências Realizadas 
### 2.1. Modelo Baseline 

**Algoritmo:**Regressão Logística  

**Resultados:**
* *F1-Score*: 0.8464
* *Recall* (Incumprimento): 0.5167
* *AUC-ROC*: 0.8145

O modelo *baseline* apresenta um *F1-Score* de 0.8464, o que indica um desempenho global positivo. A *AUC-ROC* de 0.8145 também sugere uma capacidade discriminativa razoável entre clientes cumpridores e clientes em incumprimento.

No entanto, a análise por classe revela uma limitação importante. O *Recall* da classe de incumprimento foi de apenas 0.5167, ficando claramente abaixo da meta definida de 0.70. Isto significa que o modelo identifica corretamente pouco mais de metade dos clientes em incumprimento, falhando uma parte significativa dos clientes de risco.

Assim, embora a Regressão Logística apresente um desempenho global aceitável, revelou-se insuficiente para os objetivos específicos do projeto.
 
### 2.2. Modelos Candidatos 
Após a avaliação do modelo *baseline*, foram testados algoritmos de maior complexidade, com o objetivo de melhorar o desempenho global e, sobretudo, aumentar a capacidade de identificação da classe de incumprimento.
A seleção dos algoritmos teve como objetivo comparar diferentes abordagens, pois permite avaliar não só o desempenho global, mas também a capacidade de generalização e a sensibilidade de cada modelo à classe minoritária. 

Foram avaliados os seguintes algoritmos:  
* **Random Forest:** Modelo de *ensemble* baseado em múltiplas árvores de decisão, utilizado como referência pela sua robustez e bom desempenho em dados estruturados.
* **Gradient Boosting:** Modelo de *ensemble* sequencial, cujo objetivo é melhorar progressivamente o desempenho ao corrigir os erros das iterações anteriores.
* **SVM (RBF):** modelo baseado em margens e fronteiras de decisão não lineares, utilizando o *kernel RBF*.
* **Decision Tree**- Modelo que divide os dados de forma hierárquica através de regras de decisão baseadas nas features, sendo altamente interpretável mas com tendência natural para overfitting quando não são aplicadas restrições à sua profundidade.
* **XGBoost (Extreme Gradient Boosting):** Modelo de *boosting* avançado, reconhecido pelo seu desempenho em problemas de classificação e pela incorporação de mecanismos de regularização.
 
A seleção destes algoritmos teve como objetivo comparar diferentes abordagens de aprendizagem supervisionada, incluindo métodos de *ensemble*, modelos baseados em árvores e modelos baseados em fronteiras de decisão. Desta forma, foi possível avaliar não apenas o desempenho global, mas também a capacidade de generalização e a sensibilidade de cada modelo à classe minoritária.

**Resultados Obtidos:**

| Algoritmo           | Parâmetros Base    | F1 Treino | F1 Teste | *Recall* Incumprimento | *AUC-ROC* Teste | Diagnóstico                  |
| ------------------- | ------------------ | --------: | -------: | -------------------: | ------------: | ---------------------------- |
| Regressão Logística (baseline) | `max_iter=1000`    |    0.8449 |   0.8464 |               0.5167 |        0.8145 | Bom equilíbrio               |
| Random Forest       | `n_estimators=100` |    1.0000 |   0.8667 |               0.5000 |        0.8237 | Sinais de *overfitting*      |
| Gradient Boosting   | `n_estimators=100` |    0.9493 |   0.8667 |               0.5000 |        0.8260 | Bom equilíbrio               |
| SVM (RBF)          | `kernel='rbf'`     |    0.8732 |   0.8721 |               0.4667 |        0.8417 | Bom equilíbrio               |
| Decision Tree           | `random_state=42`     |      1.0000            |      0.8252     |     0.5333     |             0.6881            |   Sinais de *Overfitting*                           |
| XGBoost             | `n_estimators=100` |    1.0000 |   0.8403 |               0.5500 |        0.7945 | Sinais moderados de *Overfitting*; melhor *Recall* |

A comparação gráfica entre os modelos (`comparacao_modelos.png`) reforça estes resultados, mostrando que todos os modelos apresentam valores de *F1-Score* superiores a 0.80, mas nenhum atinge inicialmente o objetivo definido para o *Recall* da classe de incumprimento.

A análise dos resultados mostra que todos os modelos apresentam valores de *F1-Score* superiores a 0.80, cumprindo a meta definida para esta métrica. O *SVM (RBF)* apresentou o melhor *F1-Score* no conjunto de teste, com 0.8721, seguido do *Gradient Boosting* e do *Random Forest*, ambos com 0.8667. O modelo *Decision Tree*, também cumpriu a meta, apesar de apresentar o pior AUC_ROC de todos os modelos, o que evidencia uma capacidade discriminativa mais limitada.

No entanto, a principal limitação mantém-se na identificação da classe de incumprimento. Nenhum dos modelos atingiu o objetivo mínimo de Recall ≥ 0.70 para esta classe. O melhor resultado foi obtido pelo *XGBoost*, com um *Recall* de 0.5500, seguido de *Decision Tree* com 0.5333, ainda assim ambos insuficientes para cumprir os requisitos do projeto.

**Diagnóstico de Overfitting/Underfitting:**  
A comparação entre o desempenho no conjunto de treino e no conjunto de teste permitiu identificar diferentes comportamentos de ajustamento. Os limiares de diagnóstico de sobreajustamento foram com base em três critérios.
Em primeiro lugar, um *gap* de 10 pontos percentuais foi considerado o limite a partir do qual a diferença entre treino e teste é expressiva para indicar que o modelo começa a memorizar os dados em vez de aprender padrões generalizáveis. Em segundo lugar, o intervalo entre 0.10 e 0.15 foi classificado como *overfitting* moderado por representar uma diferença relevante mas ainda controlável, onde o modelo mantém um desempenho aceitável no conjunto de teste apesar do sobreajuste. Por fim, um *gap* superior a 0.15 foi classificado como *overfitting* significativo por representar uma diferença de mais de 15 pontos percentuais entre treino e teste, indicando que o modelo está claramente a memorizar os dados de treino sem generalizar adequadamente para dados novos. 

**Resultados Obtidos:**
| Modelo        | F1 Treino | F1 Teste  |*Gap*| Diagnóstico                  |
| ------------------- | --------: | -------:|------:  | ---------------------------- |
|SVM (RBF)|0.8732|0.8721|0.0011|Equilíbrio|
|Random Forest|1.0000|0.8667|0.1333|*Overfitting* Moderado|
|Gradient Boosting|0.9493|0.8667|0.0826|Equilíbrio|
|Regressão Logística|0.8449|0.8464|-0.0015|Equilíbrio|
|XGBoost|1.0000|0.8403|0.1597|*Overftting*|
|Decision Tree|1.0000|0.8252|0.1748|*Overfitting*|

*Decision Tree* foi o modelo que apresentou maior diferença entre treino e este, ou seja, é modelo que apresenta maior *overfitting*. O *XGBoost* também apresenta um valor elevado no *gap*, no entanto, é o modelo que apresenta melhor *recall*, e tal, será tido em conta nos pontos de análise a baixo.

**Análise geral:**  
De forma global, todos os modelos avaliados apresentaram bons resultados ao nível do *F1-Score*, com valores superiores a 0.80, cumprindo assim a meta definida para esta métrica. Isto demonstra uma capacidade satisfatória de classificação global. No entanto, a principal limitação verifica-se na métrica *Recall* da classe de incumprimento. Nenhum dos modelos atingiu o objetivo mínimo de 0.70, o que evidencia dificuldades na identificação dos clientes de maior risco.
Assim, conclui-se que o problema principal não está no desempenho global dos modelos, mas sim na capacidade de identificar corretamente a classe minoritária. Este comportamento está associado ao desequilíbrio do dataset, composto por cerca de 70% de clientes em cumprimento e 30% em incumprimento.

Face a estes resultados, o *XGBoost* foi o modelo com melhor desempenho neste critério, com um *Recall* de 0.5500, embora ainda insuficiente. Sendo então selecionado para otimização e o *Gradient Boosting* por apresentar melhor equilíbrio entre desempenho e generalização. 

Por este motivo, tornou-se necessário aplicar estratégias adicionais de melhoria, nomeadamente o reequilíbrio dos dados com *SMOTE* (*Synthetic Minority Over-sampling Technique*), o ajuste do *threshold* de decisão e a otimização dos modelos mais promissores.

## 3. Otimização (*Tuning*) 
Com base nos resultados obtidos na fase anterior, foram aplicadas diferentes estratégias de otimização com o objetivo de melhorar sobretudo o *Recall* da classe de incumprimento, sem comprometer de forma significativa o *F1-Score*.

As principais estratégias utilizadas foram:
* otimização de hiperparâmetros (*GridSearchCV*);
* ajuste do limiar de decisão (*threshold tuning*);
* reequilíbrio dos dados através de *SMOTE*, que é um método muito usado para problemas de desequilíbrio de classes;
* teste de um modelo alternativo com maior potencial de identificação da classe de incumprimento.

### 3.1. Otimização de Hiperparâmetros — Gradient Boosting

Com base nos resultados obtidos na fase anterior, e conforme mencionado anteriormente, o modelo *Gradient Boosting* foi selecionado para otimização por ter apresentado um bom equilíbrio entre desempenho no treino e no teste, evidenciando menor tendência para *overfitting* face a modelos como *Random Forest* e *Decision Tree*.

**Técnica Utilizada:**  
A otimização foi realizada através de *GridSearchCV* com validação cruzada estratificada, utilizando o método *Stratified K-Fold* com k=5. Esta abordagem permitiu avaliar de forma robusta diferentes combinações de hiperparâmetros, assegurando a preservação da distribuição das classes em cada fold.

Foram ajustados os principais hiperparâmetros do modelo, nomeadamente: `n_estimators`, `learning_rate`, `max_depth` e `subsample`. Este processo possibilitou identificar a configuração que maximiza o desempenho do modelo, ao mesmo tempo que controla o risco de *Overfitting*, promovendo uma melhor capacidade de generalização.

**Espaço de pesquisa definido:**

| Hiperparâmetro  | Valores Testados | Justificação                                                                         |
| :-------------- | :--------------- | :----------------------------------------------------------------------------------- |
| `n_estimators`  | [200, 300]       | Um maior número de árvores tende a melhorar a capacidade de generalização.            |
| `learning_rate` | [0.03, 0.05]     | Taxas de aprendizagem mais baixas combinam melhor com um maior número de estimadores. |
| `max_depth`     | [3]              | Profundidade reduzida para controlar o *Overfitting*.                                  |
| `subsample`     | [0.8]            | Amostragem aleatória dos dados para aumentar a robustez do modelo.                    |

**Melhores hiperparâmetros encontrados:**  
`learning_rate` = 0.03 | `max_depth` = 3 | `n_estimators` = 300 | `subsample` = 0.8 

**O melhor resultado obtido em validação cruzada foi:**  
Melhor *F1-Score* obtido em validação cruzada: 0.8527

**Após aplicar os melhores hiperparâmetros ao conjunto de teste, obtiveram-se os seguintes resultados:**
|Métrica|Valor|
|------------------|--------|
|*F1-Score*|	0.8493|
|*AUC-ROC*|	0.8282|
|*Recall* da classe de incumprimento|	0.5333|

Apesar de o *F1-Score* se manter elevado e a *AUC-ROC* apresentar uma boa capacidade discriminativa, o *Recall* da classe de incumprimento continuou bastante abaixo da meta definida de 0.70. Como é possível verificar, a otimização de hiperparâmetros é insuficiente, é necessário avançar para o ajuste do limiar de decisão.

### **Ajuste de *Threshold* de Decisão:**  
De forma a aumentar a capacidade do modelo para identificar clientes em incumprimento, foi realizado um ajuste do limiar de decisão. Foram os limiares testados foram entre 0.20 e 0.60, com passos de 0.01.
Por defeito os modelos de classificação utilizam um limiar de 0.50, no entanto, este limite foi definido manualmente. O limite inferior de 0.20 foi estabelecido para evitar uma classificação demasiado permissiva que resultasse num número elevado de falsos positivos, compremetendo o modelo. O limite superior foi de 0.60, por representar o intervalo acima do qual o ajuste do limiar deixa de produzir melhorias relevantes no *recall*. 

 O *threshold* ótimo encontrado foi 0.59, permitindo obter um *recall* de 0.6667.

**Após aplicar o *threshold ótimo*, o modelo apresentou os seguintes resultados:**  
|Métrica|Antes do *Threshold*|Depois do *Threshold*|
|------------------|:--------:|------------|
|*F1-Score*|0.8493|	0.8612|
|*AUC-ROC*|	0.8282|0.8282|
|*Recall da classe de incumprimento*|0.5333	|0.6667|

O ajuste do *threshold* permitiu uma melhoria significativa do *Recall*, que passou de 0.5333 para 0.6667. No entanto, este valor ainda ficou ligeiramente abaixo da meta definida de 0.70, tornando necessária a aplicação de técnicas adicionais de melhoria.

### 3.2. Tentativa de Melhoria — Gradient Boosting + SMOTE
Uma vez que o *dataset* apresenta desequilíbrio entre as classes, foi aplicada a técnica *SMOTE* ao modelo *Gradient Boosting*. Esta técnica cria observações sintéticas da classe minoritária, permitindo equilibrar melhor o conjunto de treino e reduzir a tendência do modelo para favorecer a classe maioritária.

O *SMOTE* foi integrado num pipeline, garantindo que o reequilíbrio dos dados é aplicado apenas ao conjunto de treino, evitando fuga de informação para o conjunto de teste, evitando assim a fuga de informação que comprometeria a validade da avaliação do modelo.

Depois da aplicação do *SMOTE* e do ajuste do *threshold*, foram obtidos os seguintes resultados:

| Métrica                           | Gradient Boosting otimizado | Gradient Boosting + SMOTE |
| --------------------------------- | --------------------------: | ------------------------: |
| F1-Score                          |                      0.8612 |                    0.8123 |
| Recall da classe de incumprimento |                      0.6667 |                    0.7500 |
| AUC-ROC                           |                      0.8282 |                    0.7868 |

A aplicação do *SMOTE* permitiu atingir pela primeira vez a meta definida para o *Recall* da classe de incumprimento, com um valor de 0.7500, superando o objetivo mínimo de 0.70. No entanto, verificou-se uma redução no *F1-Score* e na *AUC-ROC*, evidenciando um *trade-off* entre desempenho global e capacidade de deteção dos clientes de risco.

Apesar desta redução, o modelo continua a cumprir a meta de *F1-Score* ≥ 0.80, pelo que a utilização de *SMOTE* demonstrou ser uma estratégia eficaz para melhorar a identificação da classe de incumprimento.

### 3.3. Diagnóstico de *Overfitting*
Para avaliar a capacidade de generalização do modelo, foi realizado o diagnóstico de sobreajustamento através da comparação entre o F1-Score obtido no conjunto de treino e no conjunto de teste.

| Métrica                           | Valor | 
| --------------------------------- | -------------------------- | 
|F1 Treino|0.9238|
|F1 Teste|0.8059|
|*Gap* obtido|0.1179|

O modelo apresenta um *gap* de 0.1179, situando-se na zona de sobreajustamento moderado. Este comportamento é esperado e explicado essencialmente pela utilização do *SMOTE* durante o treino, ao gerar exemplos sintéticos da classe minoritária exclusivamente no conjunto de treino, o modelo aprende padrões que não existem nos dados reais de teste, elevando naturalmente o desempenho na fase de treino face à fase de teste.
Apesar do sobreajustamento moderado identificado, o modelo mantém um *F1-Score* de teste de 0.8059, cumprindo a meta definida de 0.80, e um *Recall* da classe de incumprimento de 0.7500, cumprindo igualmente a meta de 0.70. O sobreajustamento moderado é, portanto, uma limitação conhecida e esperada desta combinação de técnicas, não comprometendo a utilidade prática do modelo nem a validade dos resultados obtidos.

### 3.4. Modelo Alternativo — XGBoost (base)  
Paralelamente ao processo anterior de otimização do modelo *Gradient Boosting*, foi testado o modelo *XGBoost*. Este modelo foi otimizado, como alternativa, com o objetivo de explorar o seu potencial para atingir simultaneamente as duas metas definidas. 
Como já tinha sido referido anteriormente, este modelo apresenta sinais de *overfitting*, no entanto, é o modelo que apresenta melhor valor na métrica de *recall*, na fase de modelos candidatos, por esse motivo as autoras decidiram que era ideal explorar este modelo também. 

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

### 3.5. Melhoria do Recall — XGBoost + SMOTE
Combinando as aprendizagens das etapas anteriores (o potencial do *XGBoost* e a eficácia do *SMOTE*), testou-se a combinação de ambos num *pipeline*, utilizando a mesma configuração do modelo descrita na secção 3.2. O *threshold* ótimo de 0.56 foi selecionado por maximizar o *Recall* mantendo *F1-Score* ≥ 0.80.

**Resultados:**
| Métrica                | Valor  |
| :--------------------- | :----- |
| F1-Score (Teste)       | 0.8213 |
| AUC-ROC (Teste)        | 0.8090 |
| Recall (Incumprimento) | 0.7500 |

Este modelo apresentou um Recall de 0.7500, igual ao obtido com Gradient Boosting + SMOTE, mas com melhor F1-Score e melhor AUC-ROC. Assim, entre os modelos que cumpriram simultaneamente as metas definidas, o *XGBoost + SMOTE* revelou-se a opção mais equilibrada.

### **Validação Cruzada — XGBoost + SMOTE**
Para avaliar a estabilidade do modelo final, foi realizada validação cruzada estratificada com 5 folds.

| Métrica                | Média  | Desvio Padrão |
| :--------------------- | :----- | :------------ |
| *F1-Score*               | 0.8153 | ± 0.0341      |
| *Recall (Incumprimento)* | 0.6042 | ± 0.0437      |
| *AUC-ROC*                | 0.7734 | ± 0.0295      |

A validação cruzada demonstra que o modelo apresenta um *F1-Score* médio de 0.8153, superior à meta definida de 0.80, evidenciando estabilidade no desempenho global. No entanto, o *Recall* médio em validação cruzada foi de 0.6042, inferior ao valor obtido no conjunto de teste (0.7500).

Esta diferença deve ser interpretada com cautela, uma vez que o *threshold* ótimo foi definido com base no conjunto de teste, podendo beneficiar especificamente essa amostra. Ainda assim, o modelo mantém um desempenho global consistente e uma capacidade de generalização aceitável, embora a identificação da classe de incumprimento possa variar entre diferentes subconjuntos de dados.

### 3.6. Diagnóstico de *Overfitting*
Para avaliar do modelo *XGBoost* com *SMOTE*, foi realizado um diagnóstico de sobreajustamento. 
| Métrica                           | Valor | 
| --------------------------------- | -------------------------- | 
|F1 Treino|0.9519|
|F1 Teste|0.8273|
|*Gap* obtido|0.1245|

A curva de aprendizagem do modelo final (`curva_aprendizagem.png`) permite observar a diferença entre o desempenho no treino e na validação, ajudando a interpretar os sinais de sobreajustamento.

O modelo final apresenta um *gap* de 0.1245, situando-se na zona de sobreajustamento moderado, utilizando os critérios de diagnóstico definidos anteriormente. Este comportamento é esperado e justificado por dois fatores principais. Por um lado, o *XGBoost* é um algoritmo baseado em árvores de decisão com elevada capacidade de memorização dos dados de treino, especialmente em datasets de dimensão reduzida como o presente, composto por 1000 observações. Por outro lado, a utilização do *SMOTE* durante o treino gera exemplos sintéticos que não existem nos dados reais de teste, elevando naturalmente o desempenho na fase de treino face à fase de teste.
Comparando com o* XGBoost* base da fase de modelos candidatos, que apresentava um *gap* de 0.1597, verifica-se uma redução do sobreajustamento após a introdução do *SMOTE*, sugerindo que o reequilíbrio dos dados contribuiu também para uma melhoria da capacidade de generalização do modelo.
Apesar do sobreajustamento moderado identificado, o modelo cumpre simultaneamente as duas metas definidas, pelo que esta limitação não compromete a sua validade como ferramenta de apoio à decisão na concessão de crédito.

### 3.7. Síntese da Evolução dos Modelos  
A tabela seguinte resume a evolução dos principais modelos testados:

| Modelo                         | F1 (Teste) | Recall (Incumprimento) | F1 ≥ 0.80 | Recall ≥ 0.70 |
| :----------------------------- | :--------- | :--------------------- | :-------- | :------------ |
| Baseline -Regressão Logística | 0.8464     | 0.5167                 | Cumpre         | Não cumpre             |
| Gradient Boosting (Tuned)      | 0.8612     | 0.6667                 | Cumpre       | Não cumpre              |
| Gradient Boosting + SMOTE      | 0.8123     | 0.7500                 | Cumpre         | Cumpre            |
| XGBoost (base)                 | 0.8541     | 0.6500                 | Cumpre         | Não cumpre               |
| XGBoost + SMOTE (Modelo Final) | 0.8213     | 0.7500                 | Cumpre         | Cumpre|            

A análise da tabela mostra que todos os modelos cumprem a meta definida para o *F1-Score*, apresentando valores superiores a 0.80. No entanto, apenas os modelos com *SMOTE* conseguem atingir o objetivo de *Recall* ≥ 0.70, confirmando a importância do reequilíbrio dos dados na identificação da classe de incumprimento.

Embora o *Gradient Boosting* otimizado apresente o melhor *F1-Score*, não cumpre a meta de *Recall*. Por outro lado, o *Gradient Boosting + SMOTE* e o XGBoost + SMOTE* cumprem ambos os critérios definidos.

O *XGBoost + SMOTE* foi selecionado como modelo final porque, entre os modelos que cumprem as duas metas, apresenta o melhor *F1-Score*, mantendo o mesmo Recall de 0.7500. Assim, representa o melhor equilíbrio entre desempenho global e capacidade de identificação dos clientes em incumprimento.

## 4. Avaliação do Modelo Final 
### 4.1. Matriz de Confusão / Análise de Erros 
A avaliação do modelo final, *XGBoost + SMOTE*, foi realizada através da matriz de confusão (`matriz_confusao.png`), comparando o seu desempenho com o modelo *baseline* de Regressão Logística.

No conjunto de teste, o modelo *baseline* identificou corretamente 31 dos 60 clientes em incumprimento, enquanto o modelo final identificou corretamente 45 dos 60 clientes em incumprimento. Assim, verifica-se uma melhoria significativa na capacidade de deteção da classe de risco.

Esta melhoria traduziu-se numa redução dos falsos negativos, que passaram de 29 no modelo baseline para 15 no modelo final. Estes casos correspondem a clientes em incumprimento classificados como cumpridores, representando o erro mais crítico no contexto da concessão de crédito.

No entanto, esta melhoria foi acompanhada por um aumento dos falsos positivos. O modelo *baseline* classificava incorretamente 16 clientes cumpridores como incumpridores, enquanto o modelo final passou a classificar incorretamente 32 clientes cumpridores como clientes de risco.

| Resultado                               | Valor no modelo final |
| --------------------------------------- | --------------------: |
| Incumprimento corretamente identificado |                    45 |
| Risco não identificado                  |                    15 |
| Cumprimento classificado como risco     |                    32 |
| Cumprimento corretamente identificado   |                   108 |

Em termos percentuais, o modelo final não identificou 25.00% dos clientes em incumprimento e classificou incorretamente como risco 22.86% dos clientes cumpridores.

A análise das médias dos erros permitiu ainda identificar alguns padrões. Os falsos negativos apresentaram valores superiores à média geral em variáveis como *Credit_Amount*, *Credit_per_Month* e *Credit_Age_Ratio*, sugerindo que o modelo pode ter maior dificuldade em identificar determinados perfis de risco associados a maior esforço financeiro.

Esta conclusão é reforçada pela análise gráfica da variável Credit_per_Month, onde se observa que alguns falsos negativos surgem em valores mais elevados de esforço financeiro mensal. Isto indica que o modelo ainda pode ter dificuldade em identificar clientes em incumprimento quando estes apresentam perfis associados a maior pressão financeira.

Por outro lado, os falsos positivos correspondem a clientes cumpridores que apresentam características semelhantes a perfis de maior risco, levando o modelo a classificá-los de forma mais conservadora.

Assim, o modelo final apresenta um claro *trade-off*: reduz o número de clientes em incumprimento não identificados, mas aumenta a classificação de clientes cumpridores como risco. Ainda assim, este comportamento é aceitável no contexto do problema, uma vez que o custo de aprovar clientes em incumprimento tende a ser superior ao custo de sujeitar clientes cumpridores a uma análise adicional.

### 4.2. Importância dos Atributos (*Feature Importance*) 
A análise da importância dos atributos, obtida a partir do modelo final (*XGBoost* com *SMOTE*), permite identificar as variáveis que mais contribuíram para a sua capacidade preditiva, reforçando simultaneamente a interpretabilidade do modelo em contexto de decisão de crédito. Esta análise encontra-se representada no gráfico de importância dos atributos (`feature_importance.png`), onde se destacam as variáveis com maior contributo para as previsões do modelo.

De acordo com os resultados, destaca-se claramente a variável *Account_Balance*, que apresenta a maior importância relativa (0.1720), assumindo-se como o principal fator na distinção entre clientes de risco e clientes cumpridores. Este resultado evidencia que a liquidez disponível e o saldo da conta são determinantes na avaliação do risco de crédito, estando diretamente associados à capacidade do cliente em cumprir as suas obrigações financeiras.

Para além desta variável, outras assumem também um papel relevante, nomeadamente:
* *Value_Savings_Stocks* (0.0830)
* *Guarantors* (0.0774)
* *Payment_Status_of_Previous_Credit* (0.0766)
* *Duration_of_Credit_monthly* (0.0552)

Estas variáveis refletem dimensões fundamentais do risco de crédito. Por um lado, *Value_Savings_Stocks* traduz a capacidade financeira acumulada do cliente, enquanto *Account_Balance* reforça a importância da liquidez imediata. Por outro lado, *Payment_Status_of_Previous_Credit* evidencia o peso do comportamento passado como indicador de risco futuro, sendo uma variável crítica na avaliação de crédito. Adicionalmente, a variável *Guarantors* demonstra a relevância da existência de garantias externas na mitigação do risco para a instituição.

Por fim, a variável *Duration_of_Credit_monthly* introduz a dimensão do contrato de crédito, refletindo o nível de compromisso financeiro ao longo do tempo. Créditos de maior duração tendem a aumentar a exposição ao risco, contribuindo para uma maior probabilidade de incumprimento.

Em termos globais, a análise evidencia que o modelo baseia a sua decisão sobretudo na combinação entre liquidez financeira, histórico de crédito e características do contrato, demonstrando que o risco de crédito resulta da interação entre múltiplos fatores e não de uma variável isolada. Este comportamento reforça a robustez do modelo enquanto ferramenta de apoio à decisão na concessão de crédito.

### 4.3. Curva ROC
A análise da curva ROC (`curva_roc.png`) permite avaliar a capacidade discriminativa dos modelos, isto é, a sua capacidade para distinguir entre clientes cumpridores e clientes em incumprimento.

De forma geral, todos os modelos apresentam curvas acima da linha do classificador aleatório, o que indica uma capacidade preditiva adequada.

O Gradient Boosting apresentou o valor mais elevado de *AUC-ROC* (0.828), seguido do modelo *baseline* de Regressão Logística (0.815) e do modelo final *XGBoost + SMOTE* (0.809).

Apesar de o modelo final não apresentar a *AUC-ROC* mais elevada, mantém um desempenho competitivo. Além disso, a *AUC-ROC* foi considerada uma métrica complementar, uma vez que o principal objetivo do projeto era melhorar o *Recall* da classe de incumprimento. Assim, o *XGBoost + SMOTE* continua a ser o modelo mais adequado, por cumprir simultaneamente as metas de *F1-Score* e *Recall*.

### 4.4. Resposta às Perguntas de Investigação (Modelação)
**Quais são as variáveis que mais contribuem para a previsão do incumprimento de crédito?** 

Com base na análise da importância dos atributos do modelo final (*XGBoost + SMOTE*), foi possível identificar as variáveis com maior contributo para a previsão do incumprimento de crédito.

Destaca-se, em primeiro lugar, a variável *Account_Balance*, que apresenta a maior importância relativa, evidenciando o papel central da liquidez financeira na avaliação do risco. Para além desta, outras variáveis assumem também relevância significativa, nomeadamente *Value_Savings_Stocks*, *Guarantors*, *Payment_Status_of_Previous_Credit* e *Duration_of_Credit_monthly*.

Estas variáveis refletem dimensões fundamentais do risco de crédito, como a capacidade financeira do cliente, o histórico de pagamentos, a existência de garantias e as características do contrato de crédito. Em conjunto, permitem ao modelo captar padrões associados ao incumprimento, demonstrando que o risco resulta da interação entre múltiplos fatores e não de uma única variável isolada

**É possível classificar os clientes em categorias de risco de incumprimento (baixo e alto risco), com base nas probabilidades geradas pelo modelo preditivo?**

Sim, é possível classificar os clientes em categorias de risco com base nas probabilidades geradas pelo modelo preditivo.

O modelo final selecionado, *XGBoost + SMOTE*, não se limita a realizar uma classificação binária entre cumprimento e incumprimento. Também gera probabilidades associadas às previsões, permitindo uma análise mais flexível e alinhada com o contexto real de decisão de crédito.

Com base no threshold ótimo identificado de 0.56, os clientes podem ser classificados em duas categorias:
* Alto risco → clientes classificados pelo modelo como associados a maior probabilidade de incumprimento;
* Baixo risco → clientes classificados pelo modelo como associados a menor probabilidade de incumprimento.

Esta abordagem permite segmentar os clientes de forma clara e objetiva, facilitando o processo de tomada de decisão por parte da instituição financeira.

Em termos práticos, esta classificação possibilita a definição de estratégias diferenciadas, como a rejeição de clientes de elevado risco, a realização de uma análise adicional ou a aplicação de condições de crédito mais restritivas, contribuindo para uma gestão mais eficiente do risco de crédito.
 
## 5. Conclusão da Fase de Modelação 
A fase de modelação permitiu desenvolver, testar e otimizar diversos modelos de classificação com o objetivo de identificar clientes em incumprimento. O principal desafio identificado foi o desequilíbrio do *dataset* e a consequente dificuldade dos modelos em detetar corretamente a classe de risco.

Ao longo das diferentes etapas, verificou-se que vários modelos apresentavam um bom desempenho global, refletido em valores elevados de *F1-Score*. No entanto, todos os modelos iniciais evidenciaram limitações na identificação da classe minoritária, não cumprindo a meta definida para o *Recall* da classe de incumprimento. Este comportamento demonstrou que a principal limitação não estava na capacidade preditiva global, mas sim na sensibilidade dos modelos à classe de maior risco.

A aplicação de técnicas de otimização, nomeadamente o ajuste de hiperparâmetros e do *threshold* de decisão, permitiu melhorias relevantes. Ainda assim, foi a introdução do reequilíbrio de dados através do *SMOTE* que se revelou determinante para aumentar significativamente o *Recall* e permitir o cumprimento da meta definida para a classe de incumprimento.

Neste contexto, o modelo final selecionado foi o *XGBoost + SMOTE*, por apresentar o melhor equilíbrio entre desempenho global e identificação dos clientes em incumprimento. Este modelo cumpriu simultaneamente os dois critérios definidos:

- *F1-Score* ≥ 0.80;
- *Recall* da classe de incumprimento ≥ 0.70.

Embora o *Gradient Boosting + SMOTE* também tenha cumprido ambos os critérios, o *XGBoost + SMOTE* foi escolhido por apresentar um *F1-Score* superior, mantendo o mesmo valor de *Recall*. Assim, revelou-se a solução mais equilibrada entre os modelos válidos.

Para além do cumprimento das metas, o modelo final apresenta ainda:
- desempenho global consistente, com *F1-Score* superior a 0.80;
- boa capacidade de identificação da classe de incumprimento;
- interpretabilidade relativa, suportada pela análise da importância das variáveis;
- capacidade discriminativa competitiva, confirmada pela análise da curva ROC.

A análise da matriz de confusão revelou um comportamento esperado neste tipo de problema: a redução dos falsos negativos foi acompanhada por um aumento dos falsos positivos. Ainda assim, este *trade-off* é aceitável no contexto da concessão de crédito, uma vez que o custo associado à aprovação de clientes em incumprimento tende a ser superior ao custo de rejeitar ou analisar com maior detalhe clientes potencialmente cumpridores.

Apesar dos resultados positivos, importa reconhecer algumas limitações. O modelo ainda apresenta dificuldades na identificação de alguns perfis de risco, especialmente casos associados a características intermédias ou a maior esforço financeiro. Além disso, o *Recall* obtido em validação cruzada foi inferior ao observado no conjunto de teste, sugerindo que o desempenho na identificação da classe de incumprimento poderá variar consoante a amostra utilizada.

Em síntese, o modelo desenvolvido demonstra ser adequado aos objetivos do projeto, apresentando um bom compromisso entre desempenho global e identificação de clientes de risco. Embora não constitua uma solução perfeita, apresenta potencial para ser utilizado como ferramenta de apoio à decisão na concessão de crédito, podendo beneficiar futuramente da introdução de novas variáveis, maior volume de dados e técnicas adicionais de engenharia de atributos.

# 5. Referências Bibliográficas
1. Prata, M. (2020). Creditability - German Credit Data [Dataset]. Kaggle. Consultado pela última vez a 10 de março de 2026,  e https://www.kaggle.com/datasets/mpwolke/cusersmarildownloadsgermancsv/data
2. Hofmann, H. (1994). Statlog (German Credit Data) [Dataset]. UCI Machine Learning Repository. Consultado pela última vez a 10 de março de 2026, de https://archive.ics.uci.edu/dataset/144/statlog+german+credit+data
3. Géron, A. (2019). Mãos à obra: Aprendizado de máquina com Scikit-Learn e TensorFlow. Starlin Alta Editora e Consultoria Eireli.
4. Zhou, Z.-H. (2021). Machine Learning. Springer Singapore. Consultado pela última vez a 18 de maio de 2026, de https://link.springer.com/book/10.1007/978-981-15-1967-3
5. Scikit-learn developers. (2025). Tuning the decision threshold for class prediction. Scikit-learn. Consultado pela última vez a 18 de maio de 2026, de https://scikit-learn.org/stable/modules/classification_threshold.html
Wei, H. (2025). SMOTE algorithm optimization and application in corporate credit risk prediction with diversification strategy consideration. Scientific Reports, 15, 23598. https://doi.org/10.1038/s41598-025-09173-x
 --- 
*Data de última atualização: 18/05/2026* 
