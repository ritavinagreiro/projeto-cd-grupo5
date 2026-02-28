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

## 5. Descrição das Variáveis  

Apesar de todas as variáveis surgirem representadas numericamente no ficheiro CSV, nem todas correspondem a variáveis quantitativas. Em diversos casos, os valores numéricos representam apenas códigos atribuídos a categorias qualitativas.

Assim, a classificação apresentada no dicionário abaixo foi realizada com base na natureza conceptual das variáveis e não exclusivamente na sua representação numérica no dataset.

| Variável (Dataset) | Tipo de Variável | Descrição |
| :--- | :--- | :--- |
| **Creditability** | Binária | Classificação do crédito: **1 = Bom crédito; 0 = Mau crédito** |
| Account Balance | Categórica | Saldo da conta corrente: 1 = Saldo < 0 DM; 2 = 0 ≤ saldo < 200 DM; 3 = ≥ 200 DM; 4 = Sem conta corrente |
| Duration | Numérica | Duração do crédito, expressa em meses. |
| Payment Status | Categórica | Histórico de crédito: 0 = Nenhum crédito anterior ou todos pagos; 1 = Todos os créditos neste banco pagos; 2 = Créditos pagos pontualmente até ao momento; 3 = Atrasos no passado; 4 = Conta crítica ou outros créditos fora deste banco |
| Purpose | Categórica | Finalidade do crédito: 0 = Automóvel novo; 1 = Automóvel usado; 2 = Mobiliário/equipamentos; 3 = Rádio/televisão; 4 = Eletrodomésticos; 5 = Reparações; 6 = Educação; 7 = Férias; 8 = Requalificação; 9 = Negócios; 10 = Outros |
| Credit Amount | Numérica | Montante total do crédito solicitado, expresso em DM. |
| Savings/Stock Value | Categórica | Conta poupança/títulos: 1 = Saldo < 100 DM; 2 = 100 ≤ saldo < 500 DM; 3 = 500 ≤ saldo < 1000 DM; 4 = ≥ 1000 DM; 5 = Desconhecido ou sem conta poupança |
| Employment Length | Categórica | Tempo no emprego atual: 1 = Desempregado; 2 = < 1 ano; 3 = 1–4 anos; 4 = 4–7 anos; 5 = ≥ 7 anos |
| Installment Rate | Numérica | Percentagem do rendimento disponível comprometida com o pagamento das prestações do crédito (escala 1 a 4). |
| Sex/Marital Status | Categórica | Estado civil e sexo do cliente: 1 = Homem divorciado/separado; 2 = Mulher; 3 = Homem solteiro; 4 = Homem casado/viúvo |
| Guarantor | Categórica | Outros devedores/fiadores: 1 = Nenhum; 2 = Co-candidato (co-devedor); 3 = Fiador |
| Duration in Current Address | Categórica | Tempo de residência atual (escala de 1 a 4 anos). |
| Most valuable available asset | Categórica | Património mais valioso disponível: 1 = Imóveis; 2 = Contrato de poupança/seguro de vida; 3 = Automóvel ou outros bens; 4 = Desconhecido ou sem propriedade |
| Age | Numérica | Idade do cliente, expressa em anos. |
| Concurrent Credits | Categórica | Existência de créditos simultâneos: 1 = Outros bancos; 2 = Lojas; 3 = Nenhum |
| Housing | Categórica | Tipo de habitação: 1 = Arrendada; 2 = Própria; 3 = Gratuita |
| No of Credits at this Bank | Numérica | Número de créditos existentes neste banco. |
| Occupation | Categórica | Situação profissional do cliente: 1 = Desempregado ou não qualificado (não residente); 2 = Não qualificado (residente); 3 = Qualificado/empregado administrativo; 4 = Gestor, autónomo ou altamente qualificado |
| Number of Dependents | Numérica | Número de dependentes ao encargo do cliente. |
| Telephone | Binária | Existência de telefone registado: 1 = Não possui telefone; 2 = Possui telefone registado |
| Foreign Worker | Binária | Indica se o cliente é trabalhador estrangeiro: 1= Sim; 2 = Não |

## 6. Descrição Técnica
O dataset selecionado para o desenvolvimento do projeto corresponde a um conjunto de dados de risco de crédito, contendo 1000 observações e 21 variáveis, incluindo a variável alvo associada ao incumprimento. Trata-se de um problema de classificação binária supervisionada, cujo objetivo consiste em prever a probabilidade de incumprimento de crédito com base em características financeiras e demográficas dos clientes.

Do ponto de vista estrutural, as variáveis encontram-se maioritariamente codificadas em formato numérico (int64), incluindo variáveis que originalmente seriam categóricas, mas que já se apresentam previamente transformadas. Esta característica facilita a aplicação direta de algoritmos de Machine Learning, reduzindo a necessidade de procedimentos adicionais de codificação nesta fase inicial. A análise preliminar confirmou igualmente a inexistência de valores em falta, o que contribui para a robustez inicial do dataset e elimina, nesta etapa, a necessidade de técnicas de imputação.

Apesar da boa qualidade estrutural, identificam-se desde já alguns aspetos que poderão exigir atenção nas fases seguintes do projeto. Em primeiro lugar, verifica-se que as variáveis apresentam diferentes escalas numéricas, o que poderá justificar a aplicação de técnicas de normalização ou padronização, dependendo do modelo escolhido. Em segundo lugar, sendo um problema de risco de crédito, é relevante analisar a distribuição da variável alvo, uma vez que um eventual desbalanceamento entre classes poderá influenciar o desempenho dos modelos de classificação.

Adicionalmente, considerando que o dataset possui uma dimensão moderada (1000 registos), será necessário adotar mecanismos de validação adequados, como validação cruzada, de forma a reduzir ) risco de overfitting e garantir a generalização do modelo. Importa ainda assegurar que, para além do desempenho preditivo, o modelo selecionado permita identificar e interpretar as variáveis com maior impacto no risco de incumprimento, garantindo não apenas capacidade preditiva, mas também utilidade analítica para apoio à decisão.

Assim, numa fase posterior do projeto, será realizada uma análise exploratória aprofundada, seguida da preparação dos dados, divisão em conjuntos de treino e teste, aplicação de diferentes algoritmos de classificação e avaliação comparativa com base em métricas adequadas, nomeadamente precision, recall e F1-score.

## 7. Bibliotecas 
O desenvolvimento do projeto será realizado em ambiente Jupyter Notebook, recorrendo às seguintes bibliotecas da linguagem Python: NumPy, Pandas, Seaborn, Matplotlib e Scikit-learn. Estas ferramentas permitem realizar análise exploratória de dados, visualização estatística, preparação e transformação de variáveis, bem como implementação e avaliação de modelos de Machine Learning.

## 8. Cronograma Interno 
| Fase | Data Limite | Entregável Esperado | 
| :--- | :--- | :--- | 
| M1: Iniciação | 24/02/2026 | Repositório estruturado e Plano de Projeto. |
| M2: Exploração | 24/03/2026 | Notebook de EDA e Dados Processados. | 
| M3: Modelação | [Data] | Comparação de algoritmos e métricas. | 
| M4: Finalização| [Data] | Pitch e Relatório Final. | 
 --- 
*Data de última atualização: 28/02/2026* 
