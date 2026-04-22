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
*Descrevam como melhoraram o melhor modelo.* 
* **Técnica Utilizada:** (p/ex.: "Utilizámos GridSearchCV para ajustar os hiperparâmetros 
`max_depth` e `learning_rate`.") 
* **Melhoria obtida:** (p/ex.: "O F1-Score subiu de 0.85 para 0.88 após o ajuste.") 
 
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
*Data de última atualização: [DD/MM/AAAA]* 
