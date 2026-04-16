# Milestone 3: Modelação e Avaliação 
 
## 1. Estratégia de Modelação 
**Divisão do dataset:**   
Foi adotada uma estratégia de validação baseada numa divisão 80% treino / 20% teste, com estratificação da variável alvo (*stratify=y*) e utilização de *random_state=42*, garantindo reprodutibilidade e preservação da distribuição original das classes (70% “Bom Crédito” e 30% “Mau Crédito”).   
Esta abordagem assegura o isolamento rigoroso do conjunto de teste, evitando data leakage e permitindo uma avaliação realista da capacidade de generalização do modelo.

**Métrica de Sucesso:**   
Dado o carácter desequilibrado do *dataset*, a métrica principal selecionada foi o *F1-Score*, por permitir um equilíbrio entre precisão e recall.  
Adicionalmente, foram consideradas:
* *AUC-ROC*, para avaliar a capacidade discriminativa do modelo;
* *Recall* da classe “Mau Crédito”, dado que, no contexto bancário, é crítico minimizar a aprovação de clientes com elevado risco de incumprimento.

## 2. Experiências Realizadas 
### 2.1. Modelo Baseline 
*O ponto de partida simples.* 
* **Algoritmo:** (p/ex.: Regressão Logística) 
* **Resultado:** (p/ex.: Accuracy: 0.72) 
 
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
