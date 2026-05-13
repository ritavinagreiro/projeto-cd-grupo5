# Desenvolvimento de um Modelo Preditivo para Apoio à Decisão de Crédito com abordagem em *Machine Learning*


## Identificação da Equipa 
* **Grupo nº:** 5
* **Membros:** 
  * Iara Gomes - Nº 2023133177 
  * Rita Vinagreiro - Nº 2023136923 
  * Ana Silva - Nº 2023145191
 
 
 
## Organização do Repositório 
 
A estrutura deste projeto segue as boas práticas de Ciência de Dados e Engenharia de Software: 
 
* **`data/`**: Armazenamento de dados (dados brutos em `raw/` e processados em `processed/`). 
* **`docs/`**: Documentação técnica detalhada dividida por Milestones (M1, M2 e M3). 
* **`notebooks/`**: Jupyter Notebooks para experimentação, limpeza e modelação. 
* **`src/`**: Código-fonte modular (scripts `.py`) para funções reutilizáveis. 
* **`reports/`**: Relatórios finais, apresentações e exportação de figuras (`figures/`). 
* **`requirements.txt`**: Ficheiro de configuração com as bibliotecas necessárias. 
 
 
 
## 1. Iniciação (Milestone 1) 
### Contexto e Problema de Negócio 
Emprestar dinheiro implica sempre um risco: a possibilidade de o cliente não reembolsar o capital em dívida, total ou parcialmente. Este risco denomina-se risco de crédito e a sua gestão eficaz é determinante para a estabilidade financeira de qualquer banco. 

Neste contexto, o presente projeto tem como objetivo apoiar uma instituição financeira na decisão de aprovar ou recusar um empréstimo, prevendo a probabilidade de incumprimento de cada cliente com base em dados históricos. Para tal, recorre-se ao desenvolvimento de modelos automatizados de previsão de risco de crédito, assentes em técnicas de *Machine Learning*. 

A adoção destas abordagens permite tornar este processo mais eficiente, contribuindo para a redução de potenciais perdas financeiras e para a promoção de decisões mais informadas e consistentes.
 
 
### Objetivo do Projeto 
* **Objetivo :** Desenvolver um modelo preditivo capaz de apoiar a instituição financeira na identificação de situações de cumprimento ou incumprimento de crédito, treinado com 80% dos dados e avaliado num conjunto de teste independente (20%), que atinja um F1-Score mínimo de 0.80 e uma taxa de identificação de incumprimento (Recall da classe de incumprimento) igual ou superior a 0.70, até ao final do Milestone 3.

### Perguntas de Investigação  
1. Quais são as características financeiras e demográficas mais comuns entre os clientes em incumprimento de crédito?
2. Existe relação entre o montante do crédito e a ocorrência de incumprimento?
3. De que forma a duração do crédito influencia a ocorrência de incumprimento?
4. Quais são as variáveis que mais contribuem para a previsão do incumprimento de crédito?
5. É possível classificar os clientes em categorias de risco de incumprimento (baixo e alto risco), com base nas probabilidades geradas pelo modelo preditivo?
 
### Fonte de Dados 

| **Dataset** | German Credit Data (Kaggle)|
|:---|:---|
| **Link** | https://www.kaggle.com/datasets/mpwolke/cusersmarildownloadsgermancsv/data |
| **Dimensão** | 1000 observações (linhas) e 21 variáveis (colunas)|
| **Variável Alvo**|Creditability (1 = Cumprimento, 0 =Incumprimento)|
| **Descrição** | O *dataset* contém informação financeira e demográfica de clientes, utilizada para avaliar o risco de crédito e prever a probabilidade de incumprimento. |

 
### Bibliotecas e ferramentas
O projeto vai ser desenvolvido em ambiente Jupyter Notebook para programar, recorrendo às bibliotecas NumPy; Pandas; Seaborn; Matplotlib e Scikit-learn.  
 
## 2. Exploração (Milestone 2) 
### Limpeza e Preparação 
Após a análise inicial do dataset, verificou-se que não existem valores em falta e que as variáveis já se encontram codificadas em formato numérico.

Durante a análise exploratória foram identificados discrepantes em algumas variáveis numéricas: *Duration_of_Credit_monthly*; *Credit_Amount*; *Age_Years*; *No_of_Credit_at_this_Bank*; *No_of_dependents*. No entanto, após análise do contexto dos dados, concluiu-se que estes valores correspondem a observações plausíveis no domínio do crédito, não representavando erros ou inconsistências, pelo que foram mantidos no dataset.

Foi ainda aplicado o StandarScaler às variáveis numéricas contínuas, de forma a garantir que todas apresentam a mesma escala, evitando enviesamentos no desempenho dos modelos.
 
### Principais Conclusões (EDA) 
![Figura 1 – Matriz de correlação](reports/figures/matriz_correlacao.png)
**Figura 1 – Matriz de correlação entre as variáveis do dataset.**

A análise exploratória dos dados, suportada pela matriz de correlação apresentada na Figura 1, permitiu identificar relações relevantes entre as variáveis do dataset e o risco de crédito.

Destaca-se a variável *Account_Balance*, que apresenta a maior correlação com a variável alvo, sugerindo que clientes com níveis de saldo mais elevados tendem a apresentar menor probabilidade de incumprimento.

Adicionalmente, verifica-se que variáveis como *Duration_of_Credit_monthly* e *Credit_Amount* apresentam correlações negativas com a variável alvo, indicando que créditos de maior duração e montante estão associados a maior risco de crédito.

As variáveis derivadas criadas, nomeadamente *Credit_per_Month* e *Credit_Age_Ratio*, evidenciam também relações relevantes com outras variáveis do dataset, permitindo captar informação adicional sobre a intensidade do crédito e o peso relativo do empréstimo face à idade do cliente. Estes resultados sugerem que estas variáveis podem contribuir para melhorar a capacidade preditiva dos modelos.

Apesar das relações identificadas, observa-se que a maioria das correlações apresenta intensidade fraca a moderada, indicando que o risco de crédito não pode ser explicado por uma única variável.


* **Ponto-chave:** O risco de crédito resulta da combinação de múltiplos fatores financeiros e características do empréstimo, sendo necessária a utilização de modelos de classificação multivariados para capturar essas relações de forma eficaz.
 
## 3. Modelação (Milestone 3) 
### Abordagem Técnica 
 **Modelos:**  
No desenvolvimento da fase de modelação, foram testados vários algoritmos de classificação supervisionada com o objetivo de prever o risco de incumprimento de crédito.
Foram considerados diferentes modelos, nomeadamente:
* Regressão Logística (baseline)
* *Random Forest*
* *Gradient Boosting*
* *SVM* (RBF)
* *XGBoost*

Após a fase de experimentação e comparação de desempenho, foram aplicadas técnicas de otimização, incluindo:
* Ajuste de hiperparâmetros (GridSearchCV)
* Validação cruzada (Stratified K-Fold)
* Ajuste do *threshold* de decisão
* Reequilíbrio de dados com *SMOTE*
  
 **Métrica Principal:**  
As métricas principais utilizadas foram:
* *Recall* (classe de incumprimento) – métrica crítica para minimizar falsos negativos
* *F1-Score* – para garantir equilíbrio entre precisão e *recall*
* *AUC-ROC* – como métrica complementar de capacidade discriminativa

**Modelo Final:**  
O modelo final selecionado foi o *XGBoost* com *SMOTE*, por ser o único a cumprir simultaneamente os critérios definidos:
* *F1-Score* ≥ 0.80
* *Recall* (Incumprimento) ≥ 0.70

**Resultados finais:**  
* *F1-Score*: 0.8213
* *Recall* (Incumprimento): 0.7500
* *AUC-ROC*: 0.8090

**Principais Conclusões**  
A modelação evidenciou que o principal desafio do problema está na identificação da classe minoritária (incumprimento), devido ao desequilíbrio do dataset.
A aplicação de técnicas de balanceamento (SMOTE) revelou-se fundamental para melhorar o desempenho do modelo neste aspeto, permitindo atingir os objetivos definidos.
O modelo final apresenta um bom equilíbrio entre desempenho global e capacidade de identificação de risco, sendo adequado como ferramenta de apoio à decisão na concessão de crédito.
 
## 4. Finalização (Milestone 4) 
### Resposta ao Problema  
O objetivo definido na Milestone 1 foi alcançado: desenvolvemos um modelo preditivo capaz de identificar situações de incumprimento de crédito com os seguintes resultados finais:

| Métrica | Objetivo | Resultado |
|---|---|---|
| F1-Score | ≥ 0,80 | **0,8213**  |
| Recall (Incumprimento) | ≥ 0,70 | **0,7500**  |
| AUC-ROC | — | **0,8090** |

O modelo identifica corretamente 3 em cada 4 clientes que vão entrar em incumprimento, antes de qualquer decisão de crédito ser tomada. Isto permite à instituição financeira reduzir perdas, tomar decisões mais consistentes e concentrar a revisão manual nos casos de maior risco.

O modelo final selecionado foi o *XGBoost com SMOTE*, o único a cumprir simultaneamente os dois critérios definidos. A variável com maior poder preditivo foi o saldo da conta bancária (*Account_Balance*): clientes com saldos mais baixos apresentam sistematicamente maior probabilidade de incumprimento. A duração e o montante do crédito também se revelaram determinantes.

### Recomendações de Inovação  
1. **Interpretabilidade com *SHAP*** — Integrar explicações individuais por cliente, indicando quais as variáveis que mais contribuíram para cada classificação. Essencial para conformidade com regulação bancária europeia (Basel III, AI Act) e para aumentar a confiança dos decisores no modelo.  
2. ***Interface Web* com *Streamlit*** — Desenvolver uma aplicação simples que permita a qualquer analista inserir os dados de um novo cliente e obter de imediato a classificação de risco (Baixo / Médio / Alto) com a probabilidade associada — tornando o modelo acessível a equipas não técnicas.  
3. **Monitorização Contínua com PSI** — Implementar o *Population Stability Index* para detetar automaticamente quando o perfil dos novos dados se afasta do perfil de treino, sinalizando a necessidade de recalibração do modelo (*model drift*).

## 5. Referências bibliográficas
1. Prata, M. (2020). *Creditability - German Credit Data* [Dataset]. Kaggle. Consultado pela última vez a 18 de março de 2026, de https://www.kaggle.com/datasets/mpwolke/cusersmarildownloadsgermancsv/data
 
## Como Reproduzir este Projeto 
1. Clone o repositório: `git clone [url-do-repo]` 
2. Instale as dependências: `pip install -r requirements.txt` 
3. Execute os notebooks na pasta `notebooks/` seguindo a ordem numérica. 
 
 
**Instituição:** Coimbra Business School | ISCAC   
**Curso:** Licenciatura em Ciência de Dados para a Gestão   
**Unidade Curricular:** Projeto em Ciência de Dados   
**Professor Responsável:** Dora Melo (dmelo@iscac.pt)   
