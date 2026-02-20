# Milestone 1: Iniciação e Definição do Projeto 
 
## 1. Descrição Detalhada do Problema 
Atualmente, as instituições financeiras recebem muitos pedidos de crédito e precisam de decidir se aprovam ou não cada empréstimo. Estas decisões são importantes, pois uma escolha errada pode resultar em perdas financeiras devido ao incumprimento dos clientes.

O problema deste projeto consiste em apoiar uma instituição financeira na decisão de aprovar ou recusar um empréstimo, prevendo a probabilidade de incumprimento de cada cliente com base em dados históricos.

Este tema é relevante porque o crédito ao consumo tem vindo a aumentar, tornando necessário melhorar os processos de avaliação de risco, de forma a reduzir perdas e apoiar decisões mais informadas. 
 
## 2. Objetivos SMART  
1.  **Objetivo 1:** Prever o incumprimento de crédito dos clientes, alcançando um F1-score mínimo de 0.80, até à M3.
2.  **Objetivo 2:** Identificar as 5 variáveis com maior impacto no risco de crédito, através de técnicas de análise exploratória e interpretação de modelos, até à M3.

**Perguntas de Investigação**
1.Quais são as variáveis financeiras e demográficas que mais influenciam a probabilidade de incumprimento de crédito?
2.Existe uma relação significativa entre o rendimento anual do cliente e o risco de incumprimento?
3.Qual o modelo de classificação que apresenta melhor desempenho na previsão do incumprimento de crédito?
 
## 3. Metodologia de Gestão (PBL) 
* **Divisão de Tarefas:** 
  * **Iara Gomes:** Responsável pela Engenharia de Dados. 
  * **Rita Vinagreiro:** Responsável pela Modelação Estatística. 
  * **Ana Silva:** Responsável pela Visualização e Documentação.
  * **Nota:** Todos os membros irão participar de forma equititativa em cada tarefa. 
* **Ferramentas de Colaboração:** [GitHub Projects para Kanban, reuniões semanais via 
Teams/Discord e presencial quando necessário, Google Docs]. 
 
## 4. Análise de Viabilidade dos Dados 
* **Disponibilidade:** O dataset foi obtido através da plataforma Kaggle e encontra-se disponível para utilização imediata em formato CSV. Os dados foram carregados com sucesso num notebook Kaggle, permitindo o acesso direto para análise e modelação, não sendo necessária ligação a bases de dados externas. 
* **Qualidade Inicial:** A qualidade inicial dos dados foi avaliada através dos métodos df.head(), df.info(), df.describe() e df.isnull().sum(). A análise confirmou a existência de 1000 registos completos, sem valores em falta (NaN). As variáveis apresentam maioritariamente tipo numérico (int64), incluindo variáveis categóricas previamente codificadas. Desta forma, o dataset apresenta boa qualidade inicial, não sendo necessária imputação de valores em falta nesta fase. Eventuais transformações e preparação adicional dos dados serão realizadas na Milestone 2.
* **Ética:** O dataset é público e encontra-se anonimizado, não contendo dados pessoais identificáveis. A sua utilização destina-se exclusivamente a fins académicos, cumprindo os princípios do Regulamento Geral sobre a Proteção de Dados (RGPD). 
 
## 5. Cronograma Interno 
| Fase | Data Limite | Entregável Esperado | 
| :--- | :--- | :--- | 
| M1: Iniciação | [24/02/2026] | Repositório estruturado e Plano de Projeto. |
| M2: Exploração | [Data] | Notebook de EDA e Dados Processados. | 
| M3: Modelação | [Data] | Comparação de algoritmos e métricas. | 
| M4: Finalização| [Data] | Pitch e Relatório Final. | 
 --- 
*Data de última atualização: [18/02/2026]* 
