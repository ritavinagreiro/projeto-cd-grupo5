# Avaliação e Análise de Risco de Crédito num Banco Alemão
 
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
Emprestar dinheiro implica sempre um risco: do cliente não reembolsar o capital em dívida, total ou parcialmente. Este risco denomina-se risco de crédtio e a sua gestão eficaz é determinante para a estabilidade financeira de qualquer banco. O problema consiste em apoiar uma instituição financeira na decisão de aprovar ou recusar um empréstimo, prevendo a probabilidade de incumprimento de cada cliente com base em dados históricos, através de modelos automatizados de previsão de risco de crédito. 
 
### Objetivos do Projeto 
* **Objetivo 1:** Desenvolver um modelo preditivo capaz de apoiar a instituição financeira na decisão de aprovação ou recusa de crédito, treinado em 80% dos dados e avaliado no conjunto de teste, que atinja um F1-Score mínimode 0.80 e uma AUC_ROC mínima de 0.80 até ao final do Milestone 3.
* **Objetivo 2:** 

### Perguntas de Investigação
1. Quais são as variáveis financeiras e demográficas que mais influenciam a probabilidade de incumprimento de crédito?
2. Existe uma relação significativa entre o rendimento anual do cliente e o risco de incumprimento?
3. Qual o modelo de classificação que apresenta melhor desempenho na previsão do incumprimento de crédito?
4. Como otimizar e implementar o modelo na prática, minimizando perdas e mantendo equidade no acesso ao crédito?
5. Identificar as 5 variáveis com maior contribuição preditiva, para o risco de incumprimento, medidas através de feature importance.
6. Será que as variáveis obtidas do feature importance são as mesma que foram identificadas na análise exploratória? 
 
### Fonte de Dados 
| **Dataset** | https://www.kaggle.com/datasets/mpwolke/cusersmarildownloadsgermancsv/data|
|:---|:---|
| **Dimensão** | 1000 linhas, 21 colunas |
| **Variável Alvo**|Credibility (1 = Risco bom (ou seja, risco pequeno), 0 = Risco mau)|
 
### Bibliotecas e ferramentas
Como ferramenta vamos usar o Jupyter Notebook para programar, e as seguintes ferramentas: NumPy; Pandas; Seaborn; Matplotlib e Scikit-learn.  
 
## 2. Exploração (Milestone 2) 
### Limpeza e Preparação 
A partir do momento em que analisámos os dados no seu estado bruto, foi denotado que todas as variáveis estavam na sua forma numérica, ou seja, as variáveis numéricas já tinham sido fornecidas na sua forma codificada. 
Durante a análise exploratória foram identificados outliers nas seguintes variáveis numéricas: Duration_of_Credit_monthly; Credit_Amount; Age_Years; No_of_Credit_at_this_Bank; No_of_dependents. No entanto, foi decidido não realizar nenhum processo, para tratar estes outliers, pois foi concluído que estes valores identificados não representavam erros ou inconsistências nos dados. 
Para o escalonamento de atributos, foi aplicado o StandarScaler às variáveis numéricas contínuas.
 
### Principais Conclusões (EDA) 
> *Dica: Insere aqui o gráfico mais importante do projeto.* 
* **Ponto-chave:** [Ex: Identificámos que o fator X influencia em 40% o resultado Y, por aplicação 
do método ganho de informação] 
 
 
 
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
