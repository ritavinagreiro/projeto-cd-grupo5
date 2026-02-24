# Milestone 1: Iniciação e Definição do Projeto 
 
## 1. Descrição Detalhada do Problema 
Atualmente, as instituições financeiras recebem muitos pedidos de crédito e precisam de decidir se aprovam ou não cada empréstimo. Estas decisões são importantes, pois uma escolha errada pode resultar em perdas financeiras devido ao incumprimento dos clientes.

O problema deste projeto consiste em apoiar uma instituição financeira na decisão de aprovar ou recusar um empréstimo, prevendo a probabilidade de incumprimento de cada cliente com base em dados históricos.

Este tema é relevante porque o crédito ao consumo tem vindo a aumentar, tornando necessário melhorar os processos de avaliação de risco, de forma a reduzir perdas e apoiar decisões mais informadas. 
 
## 2. Objetivos SMART  
1.  **Objetivo 1:** Prever o incumprimento de crédito dos clientes, alcançando um F1-score mínimo de 0.80, até à M3.
2.  **Objetivo 2:** Identificar as 5 variáveis com maior impacto no risco de crédito, através de técnicas de análise exploratória e interpretação de modelos, até à M3.

**Perguntas de Investigação**
1. Quais são as variáveis financeiras e demográficas que mais influenciam a probabilidade de incumprimento de crédito?
2. Existe uma relação significativa entre o rendimento anual do cliente e o risco de incumprimento?
3. Qual o modelo de classificação que apresenta melhor desempenho na previsão do incumprimento de crédito?
4. Como otimizar e implementar o modelo na prática, minimizando perdas e mantendo equidade no acesso ao crédito?
 
## 3. Metodologia de Gestão (PBL) 
* **Divisão de Tarefas:** 
  * **Iara Gomes:** Responsável pela Engenharia de Dados. 
  * **Rita Vinagreiro:** Responsável pela Modelação Estatística. 
  * **Ana Silva:** Responsável pela Visualização e Documentação.
  * **Nota:** Todos os membros irão participar de forma equititativa em cada tarefa. 
* **Ferramentas de Colaboração:** GitHub Projects para Kanban, reuniões semanais via 
Teams/Discord e presencial quando necessário, Google Docs. 
 
## 4. Análise de Viabilidade dos Dados 
* **Disponibilidade:** O dataset foi obtido através da plataforma Kaggle e encontra-se disponível para utilização imediata em formato CSV. Os dados foram carregados com sucesso num notebook Kaggle, permitindo o acesso direto para análise e modelação, não sendo necessária ligação a bases de dados externas. 
* **Qualidade Inicial:** A qualidade inicial dos dados foi avaliada através dos métodos df.head(), df.info(), df.describe() e df.isnull().sum(). A análise confirmou a existência de 1000 registos completos, sem valores em falta (NaN). As variáveis apresentam maioritariamente tipo numérico (int64), incluindo variáveis categóricas previamente codificadas. Desta forma, o dataset apresenta boa qualidade inicial, não sendo necessária imputação de valores em falta nesta fase. Eventuais transformações e preparação adicional dos dados serão realizadas na Milestone 2.
* **Ética:** O dataset é público e encontra-se anonimizado, não contendo dados pessoais identificáveis. A sua utilização destina-se exclusivamente a fins académicos, cumprindo os princípios do Regulamento Geral sobre a Proteção de Dados (RGPD).
* **Dataset:** https://www.kaggle.com/datasets/mpwolke/cusersmarildownloadsgermancsv/data

## 5. Descrição Técnica
O dataset selecionado para o desenvolvimento do projeto corresponde a um conjunto de dados de risco de crédito, contendo 1000 observações e 21 variáveis, incluindo a variável alvo associada ao incumprimento. Trata-se de um problema de classificação binária supervisionada, cujo objetivo consiste em prever a probabilidade de incumprimento de crédito com base em características financeiras e demográficas dos clientes.

Do ponto de vista estrutural, as variáveis encontram-se maioritariamente codificadas em formato numérico (int64), incluindo variáveis que originalmente seriam categóricas, mas que já se apresentam previamente transformadas. Esta característica facilita a aplicação direta de algoritmos de Machine Learning, reduzindo a necessidade de procedimentos adicionais de codificação nesta fase inicial. A análise preliminar confirmou igualmente a inexistência de valores em falta, o que contribui para a robustez inicial do dataset e elimina, nesta etapa, a necessidade de técnicas de imputação.

Apesar da boa qualidade estrutural, identificam-se desde já alguns aspetos que poderão exigir atenção nas fases seguintes do projeto. Em primeiro lugar, verifica-se que as variáveis apresentam diferentes escalas numéricas, o que poderá justificar a aplicação de técnicas de normalização ou padronização, dependendo do modelo escolhido. Em segundo lugar, sendo um problema de risco de crédito, é relevante analisar a distribuição da variável alvo, uma vez que um eventual desbalanceamento entre classes poderá influenciar o desempenho dos modelos de classificação.

Adicionalmente, considerando que o dataset possui uma dimensão moderada (1000 registos), será necessário adotar mecanismos de validação adequados, como validação cruzada, de forma a reduzir ) risco de overfitting e garantir a generalização do modelo. Importa ainda assegurar que, para além do desempenho preditivo, o modelo selecionado permita identificar e interpretar as variáveis com maior impacto no risco de incumprimento, garantindo não apenas capacidade preditiva, mas também utilidade analítica para apoio à decisão.

Assim, numa fase posterior do projeto, será realizada uma análise exploratória aprofundada, seguida da preparação dos dados, divisão em conjuntos de treino e teste, aplicação de diferentes algoritmos de classificação e avaliação comparativa com base em métricas adequadas, nomeadamente precision, recall e F1-score.

## 6. Bibliotecas 
O desenvolvimento do projeto será realizado em ambiente Jupyter Notebook, recorrendo às seguintes bibliotecas da linguagem Python: NumPy, Pandas, Seaborn, Matplotlib e Scikit-learn. Estas ferramentas permitem realizar análise exploratória de dados, visualização estatística, preparação e transformação de variáveis, bem como implementação e avaliação de modelos de Machine Learning.

## 7. Cronograma Interno 
| Fase | Data Limite | Entregável Esperado | 
| :--- | :--- | :--- | 
| M1: Iniciação | [24/02/2026] | Repositório estruturado e Plano de Projeto. |
| M2: Exploração | [Data] | Notebook de EDA e Dados Processados. | 
| M3: Modelação | [Data] | Comparação de algoritmos e métricas. | 
| M4: Finalização| [Data] | Pitch e Relatório Final. | 
 --- 
*Data de última atualização: [20/02/2026]* 
