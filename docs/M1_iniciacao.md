# Milestone 1: Iniciação e Definição do Projeto 
 
## 1. Descrição Detalhada do Problema 

O setor bancário enfrenta diariamente o desafio de avaliar pedidos de crédito, sendo necessário decidir, de forma rápida e fundamentada, quais os clientes que apresentam maior risco de incumprimento. Uma decisão incorreta pode resultar em perdas financeiras significativas, afetando a rentabilidade e a estabilidade das instituições financeiras.

Neste contexto, o problema deste projeto consiste no desenvolvimento de um modelo de classificação capaz de prever o incumprimento de crédito, com base em características financeiras e demográficas dos clientes, de forma a apoiar o processo de decisão na concessão de crédito.

A variável objetivo corresponde ao estado do crédito do cliente, sendo utilizada para identificar situações de incumprimento e representada pela variável *Creditability*, de natureza binária, em que 1 indica cumprimento das obrigações de crédito (bom crédito) e 0 indica incumprimento (mau crédito).

A relevância deste problema prende-se com o aumento do crédito ao consumo e com a necessidade crescente de sistemas de apoio à decisão que permitam reduzir o risco associado à concessão de crédito e melhorar a eficiência das instituições financeiras

## 2. Objetivos SMART  
* **Objetivo 1:** Desenvolver um modelo preditivo capaz de apoiar a instituição financeira na decisão de aprovação ou recusa de crédito, treinado com 80% dos dados e avaliado num conjunto d teste independente, que atinja um F1-Score mínimo de 0.80 e uma AUC_ROC mínima de 0.80, até ao final do Milestone 3.

* **Objetivo 2:** Comparar diferentes algoritmos de classificação para prever o risco de crédito, utilizando validação cruzada no conjunto de treino, de forma a selecionar o modelo com melhor desempenho, garantindo um F1-Score mínimo de 0.80 e consistência entre validação e teste, até ao final do Milestone 3.

**Perguntas de Investigação**

1.   ⁠Quais são as variáveis financeiras e demográficas que mais influenciam a probabilidade de incumprimento de crédito?  
2.   Qual a relação entre características do crédito (montante, duração) e a probabilidade incumprimento?   
3.   Qual o modelo de classificação que apresenta melhor desempenho na previsão do incumprimento de crédito?   
4.   Quais são as cinco variáveis com maior importância preditiva na previsão do risco de incumprimento, com base nas métricas de feature importance do modelo selecionado?   
5.   As variáveis identificadas como mais importantes pelo modelo coincidem com as variáveis destacadas na análise exploratória dos dados?
 
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

## 5. Dicionário de Dados  

Apesar de todas as variáveis surgirem representadas numericamente no ficheiro CSV, nem todas correspondem a variáveis quantitativas. Em diversos casos, os valores numéricos representam apenas códigos atribuídos a categorias qualitativas.

Assim, a classificação apresentada no dicionário abaixo foi realizada com base na natureza conceptual das variáveis e não exclusivamente na sua representação numérica no dataset.

Devido ao facto de o repositório de dados fornecido não incluir a informação necessária para a análise de cada variável, o grupo optou por recorrer ao seguinte link, que disponibiliza a descrição detalhada do dataset, permitindo assim realizar uma análise correta:
https://archive.ics.uci.edu/dataset/144/statlog+german+credit+data

| Variável (Dataset) | Tipo de Variável | Valores | Descrição |
|--------------------|------------------|--------|----------|
| **Creditability** | Binária | 1 = Cumprimento; 0 = Incumprimento | Estado do crédito do cliente |
| Account Balance | Categórica ordinal | 1 = Saldo < 0 DM; 2 = 0 ≤ saldo < 200 DM; 3 = ≥ 200 DM; 4 = Sem conta corrente | Saldo da conta corrente |
| Duration | Numérica inteira | Valores inteiros (meses) | Duração do crédito |
| Payment Status | Categórica ordinal | 0 = Nenhum crédito anterior ou todos pagos; 1 = Todos os créditos neste banco pagos; 2 = Créditos pagos pontualmente até ao momento; 3 = Atrasos no passado; 4 = Conta crítica ou outros créditos fora deste banco | Histórico de crédito |
| Purpose | Categórica nominal | 0 = Automóvel novo; 1 = Automóvel usado; 2 = Mobiliário/equipamentos; 3 = Rádio/televisão; 4 = Eletrodomésticos; 5 = Reparações; 6 = Educação; 7 = Férias; 8 = Requalificação; 9 = Negócios; 10 = Outros | Finalidade do crédito |
| Credit Amount | Numérica contínua | Valores numéricos contínuos | Montante do crédito solicitado |
| Savings/Stock Value | Categórica ordinal | 1 = Saldo < 100 DM; 2 = 100 ≤ saldo < 500 DM; 3 = 500 ≤ saldo < 1000 DM; 4 = ≥ 1000 DM; 5 = Desconhecido ou sem conta poupança | Conta poupança ou títulos |
| Employment Length | Categórica ordinal | 1 = Desempregado; 2 = < 1 ano; 3 = 1–4 anos; 4 = 4–7 anos; 5 = ≥ 7 anos | Tempo no emprego atual |
| Installment Rate | Numérica inteira | Valores inteiros (escala de 1 a 4) | Percentagem do rendimento comprometida |
| Sex/Marital Status | Categórica nominal | 1 = Homem divorciado/separado; 2 = Mulher; 3 = Homem solteiro; 4 = Homem casado/viúvo | Estado civil e sexo |
| Guarantor | Categórica nominal | 1 = Nenhum; 2 = Co-candidato; 3 = Fiador | Existência de fiadores |
| Duration in Current Address | Numérica inteira | Valores inteiros (escala de 1 a 4) | Tempo de residência |
| Most Valuable Available Asset | Categórica nominal | 1 = Imóveis; 2 = Poupança/seguro de vida; 3 = Automóvel ou outros bens; 4 = Desconhecido ou sem propriedade | Património mais valioso |
| Age | Numérica inteira | Valores inteiros (anos) | Idade do cliente |
| Concurrent Credits | Categórica nominal | 1 = Outros bancos; 2 = Lojas; 3 = Nenhum | Créditos simultâneos |
| Housing | Categórica nominal | 1 = Arrendada; 2 = Própria; 3 = Gratuita | Tipo de habitação |
| No of Credits at this Bank | Numérica inteira | Valores inteiros | Nº de créditos neste banco |
| Occupation | Categórica nominal | 1 = Desempregado ou não qualificado; 2 = Não qualificado; 3 = Qualificado; 4 = Gestor ou altamente qualificado | Situação profissional |
| Number of Dependents | Numérica inteira | Valores inteiros | Nº de dependentes |
| Telephone | Binária | 1 = Não possui; 2 = Possui | Existência de telefone |
| Foreign Worker | Binária | 1 = Sim; 2 = Não | Trabalhador estrangeiro |

## 6. Descrição Técnica
O dataset selecionado para o desenvolvimento do projeto corresponde a um conjunto de dados de risco de crédito, contendo 1000 observações e 21 variáveis, incluindo a variável alvo associada ao incumprimento. Trata-se de um problema de classificação binária supervisionada, cujo objetivo consiste em prever a probabilidade de incumprimento de crédito com base em características financeiras e demográficas dos clientes.

Do ponto de vista estrutural, as variáveis encontram-se maioritariamente codificadas em formato numérico (int64), incluindo variáveis que originalmente seriam categóricas, mas que já se apresentam previamente transformadas. Esta característica facilita a aplicação direta de algoritmos de Machine Learning, reduzindo a necessidade de procedimentos adicionais de codificação nesta fase inicial. A análise preliminar confirmou igualmente a inexistência de valores em falta, o que contribui para a robustez inicial do dataset e elimina, nesta etapa, a necessidade de técnicas de imputação.

Apesar da boa qualidade estrutural, identificam-se desde já alguns aspetos que poderão exigir atenção nas fases seguintes do projeto. Em primeiro lugar, verifica-se que as variáveis apresentam diferentes escalas numéricas, o que poderá justificar a aplicação de técnicas de normalização ou padronização, dependendo do modelo escolhido. Em segundo lugar, sendo um problema de risco de crédito, é relevante analisar a distribuição da variável alvo, uma vez que um eventual desequilíbrio entre classes poderá influenciar o desempenho dos modelos de classificação.

Adicionalmente, considerando que o dataset possui uma dimensão moderada (1000 registos), será necessário adotar mecanismos de validação adequados, como validação cruzada, de forma a reduzir ) risco de overfitting e garantir a generalização do modelo. Importa ainda assegurar que, para além do desempenho preditivo, o modelo selecionado permita identificar e interpretar as variáveis com maior impacto no risco de incumprimento, garantindo não apenas capacidade preditiva, mas também utilidade analítica para apoio à decisão.

Assim, numa fase posterior do projeto, será realizada uma análise exploratória aprofundada, seguida da preparação dos dados, divisão em conjuntos de treino e teste, aplicação de diferentes algoritmos de classificação e avaliação comparativa com base em métricas adequadas, nomeadamente precision, recall e F1-score.

## 7. Bibliotecas 
O desenvolvimento do projeto será realizado em ambiente Jupyter Notebook, recorrendo às seguintes bibliotecas da linguagem Python: NumPy, Pandas, Seaborn, Matplotlib e Scikit-learn. Estas ferramentas permitem realizar análise exploratória de dados, visualização estatística, preparação e transformação de variáveis, bem como implementação e avaliação de modelos de Machine Learning.

## 8. Cronograma Interno 
| Fase | Data Limite | Entregável Esperado | 
| :--- | :--- | :--- | 
| M1: Iniciação | 24/02/2026 | Repositório estruturado e Plano de Projeto. |
| M2: Exploração | 24/03/2026 | Notebook de EDA e Dados Processados. | 
| M3: Modelação | 23/04/2026 | Comparação de algoritmos e métricas. | 
| M4: Finalização| [Data] | Pitch e Relatório Final. | 

## 9. Referências Bibliográficas
1. Prata, M. (2020). *Creditability - German Credit Data* [Dataset]. Kaggle. Consultado pela última vez a 18 de março de 2026, de https://www.kaggle.com/datasets/mpwolke/cusersmarildownloadsgermancsv/data
2. Hofmann, H. (1994). *Statlog (German Credit Data)* [Dataset]. UCI Machine Learning Repository. Consultado pela última vez a 4 de março de 2026, de https://archive.ics.uci.edu/dataset/144/statlog+german+credit+data
 --- 
*Data de última atualização: 08/04/2026* 
