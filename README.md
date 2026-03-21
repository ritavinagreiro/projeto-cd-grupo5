# Avaliação e Análise do Risco de Crédito com Base em Dados de um Banco Alemão


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
Emprestar dinheiro implica sempre um risco: a possibilidade de o cliente não reembolsar o capital em dívida, total ou parcialmente. Este risco denomina-se risco de crédtio e a sua gestão eficaz é determinante para a estabilidade financeira de qualquer banco. 

Neste contexto, o presente projeto tem como objetivo apoiar uma instituição financeira na decisão de aprovar ou recusar um empréstimo, prevendo a probabilidade de incumprimento de cada cliente com base em dados históricos, através de modelos automatizados de previsão de risco de crédito. 

A utilização de técnicas de Machine Learning permite tornar este processo mais eficiente, reduzindo perdas financeiras e promovendo decisões mais informadas e consistentes.
 
 
### Objetivos do Projeto 
* **Objetivo 1:** Desenvolver um modelo preditivo capaz de apoiar a instituição financeira na decisão de aprovação ou recusa de crédito, treinado com 80% dos dados e avaliado num conjunto de teste independente, que atinja um F1-Score mínimo de 0.80 e uma AUC_ROC mínima de 0.80, até ao final do Milestone 3.
* **Objetivo 2:** Comparar diferentes algoritmos de classificação para prever o risco de crédito, utilizando validação cruzada no conjunto de treino, de forma a selecionar o modelo com melhor desempenho, garantindo um F1-Score mínimo de 0.80 e consistência entre validação e teste, até ao final do Milestone 3.

### Perguntas de Investigação
1. Quais são as variáveis financeiras e demográficas que mais influenciam a probabilidade de incumprimento de crédito?
2. Qual a relação entre características do crédito (montante, duração) e a probabilidade  incumprimento?
3. Qual o modelo de classificação que apresenta melhor desempenho na previsão do incumprimento de crédito?
5. Quais são as cinco variáveis com maior importância preditiva na previsão do risco de incumprimento, com base nas métricas de feature importance do modelo selecionado?
6. As variáveis identificadas como mais importantes pelo modelo coincidem com as variáveis destacadas na análise exploratória dos dados?
 
### Fonte de Dados 

| **Dataset** | German Credit Data (Kaggle)|
|:---|:---|
| **Link** | https://www.kaggle.com/datasets/mpwolke/cusersmarildownloadsgermancsv/data |
| **Dimensão** | 1000 observações (linhas) e 21 variáveis (colunas)|
| **Variável Alvo**|Creditability (1 = Bom crédito, 0 = Mau crédito)|
| **Descrição** | O dataset contém informação financeira e demográfica de clientes, utilizada para avaliar o risco de crédito e prever a probabilidade de incumprimento. |

 
### Bibliotecas e ferramentas
O projeto vai ser desenvolvido em ambiente Jupyter Notebook para programar, recorrendo às bibliotecas NumPy; Pandas; Seaborn; Matplotlib e Scikit-learn.  
 
## 2. Exploração (Milestone 2) 
### Limpeza e Preparação 
Após a análise inicial do dataset, verificou-se que não existem valores em falta e que as variáveis já se encontram codificadas em formato numérico.

Durante a análise exploratória foram identificados outliers em algumas variáveis numéricas: Duration_of_Credit_monthly; Credit_Amount; Age_Years; No_of_Credit_at_this_Bank; No_of_dependents. No entanto, após análise do contexto dos dados, concluiu-se que estes valores correspondem a observações plausíveis no domínio do crédito, não representavando erros ou inconsistências, pelo que foram mantidos no dataset.

Foi ainda aplicado o StandarScaler às variáveis numéricas contínuas, de forma a garantir que todas apresentam a mesma escala, evitando enviesamentos no desempenho dos modelos.
 
### Principais Conclusões (EDA) 
![Figura 1 – Matriz de correlação](reports/figures/figura1.jpeg)
**Figura 1 – Matriz de correlação entre as variáveis do dataset.**

A análise exploratória dos dados, suportada pela matriz de correlação apresentada na Figura 1, permitiu identificar relações relevantes entre as variáveis do dataset e o risco de crédito.

Destaca-se a variável *Account_Balance*, que apresenta a maior correlação com a variável alvo, sugerindo que clientes com níveis de saldo mais elevados tendem a apresentar menor probabilidade de incumprimento.

Adicionalmente, verifica-se que variáveis como *Duration_of_Credit_monthly* e *Credit_Amount* apresentam correlações negativas com a variável alvo, indicando que créditos de maior duração e montante estão associados a maior risco de crédito.

As variáveis derivadas criadas, nomeadamente *Credit_per_Month* e *Credit_Age_Ratio*, evidenciam também relações relevantes com outras variáveis do dataset, permitindo captar informação adicional sobre a intensidade do crédito e o peso relativo do empréstimo face à idade do cliente. Estes resultados sugerem que estas variáveis podem contribuir para melhorar a capacidade preditiva dos modelos.

Apesar das relações identificadas, observa-se que a maioria das correlações apresenta intensidade fraca a moderada, indicando que o risco de crédito não pode ser explicado por uma única variável.


* **Ponto-chave:** O risco de crédito resulta da combinação de múltiplos fatores financeiros e características do empréstimo, sendo necessária a utilização de modelos de classificação multivariados para capturar essas relações de forma eficaz.
 
 
 
## 3. Modelação (Milestone 3) 
### Abordagem Técnica 
* **Modelos:** [Ex: Random Forest e XGBoost] 
* **Métrica Principal:** [Ex: F1-Score ou RMSE] 
 
 
 
## 4. Finalização (Milestone 4) 
### Resposta ao Problema 
[Resumo da solução e como ela gera valor para o negócio.] 
 
### Recomendações de Inovação 
1. [Sugestão prática baseada nos resultados]



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
