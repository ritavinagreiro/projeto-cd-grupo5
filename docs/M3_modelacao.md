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
*Listagem dos algoritmos testados e a justificação da escolha.* 
 
| Algoritmo | Parâmetros Base | Métrica (Treino) | Métrica (Teste) | Notas | 
| :--- | :--- | :--- | :--- | :--- | 
| Random Forest | n_estimators=100 | 0.95 | 0.82 | Sinais de overfitting | 
| XGBoost | default | 0.88 | 0.85 | Melhor generalização | 
| SVM | kernel='rbf' | 0.80 | 0.79 | Lento no treino | 
 
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
