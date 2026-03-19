# Milestone 2: Análise Exploratória e Engenharia de Atributos 
 
## 1. Análise Exploratória de Dados (EDA) 
### 1.1. Distribuição da Variável Alvo 
A variável alvo do presente estudo é Creditability, que indica o nível de risco de crédito do cliente, assumindo dois valores possíveis:
* 1 - Bom crédito
* 0 - Mau crédito

A análise da distribuição revela que, num total de 1000 observações:
* 700 clientes (70%) apresentam bom crédito
* 300 clientes (30%) apresentam mau crédito

Verifica-se, assim, que a variável alvo apresenta um ligeiro desequilíbrio, existindo uma predominância de clientes classificados como bom crédito.  
Tratando-se de uma variável binária, esta não segue uma distribuição normal, mas sim uma distribuição binomial.

**Factos importantes:** 
* A variável alvo apresenta uma distribuição de 70% / 30%, evidenciando um desequilíbrio moderado.
* Um modelo que previsse sempre "Bom crédito" teria automaticamente uma accuracy de 70%.
* Assim, para avaliar corretamente o desempenho do modelo, será importante considerar métricas adicionais como Precision, Recall, F1-score e ROC-AUC.
* O problema em análise é um caso de classificação binária supervisionada.
 
### 1.2. Correlações Relevantes 
A análise da matriz de correlação permitiu identificar as variáveis com maior associação à variável alvo (Creditability). Destacam-se:
* Account_Balance (0.35) – correlação positiva moderada
* Payment_Status_of_Previous_Credit (0.23) – correlação positiva fraca
* Credit_Amount (-0.15) – correlação negativa fraca
* Duration_of_Credit_monthly (-0.21) – correlação negativa fraca

A variável Account_Balance apresenta a maior correlação com o objetivo do modelo, sugerindo que o saldo da conta é um dos principais fatores associados ao risco de crédito.

As variáveis Duration_of_Credit_monthly e Credit_Amount indicam que empréstimos de maior duração e montante tendem a apresentar maior probabilidade de incumprimento.

De forma geral, as correlações observadas são moderadas ou fracas, indicando que nenhuma variável isoladamente explica completamente o comportamento da variável alvo, reforçando a necessidade de modelação multivariada.

**Análise Gráfica das Variáveis Mais Relevantes**
* **Duration_of_Credit_monthly vs Creditability:** Notou-se que créditos com maior duração apresentam maior probabilidade de incumprimento. No gráfico de dispersão Credit Amount vs Duration e no gráfico Duration vs Creditability, observa-se maior concentração de maus créditos em prazos mais longos, confirmando a correlação negativa fraca identificada (-0.21). Isto sugere que compromissos financeiros prolongados podem aumentar o risco de crédito.
* **Account_Balance vs Creditability:** Verificou-se que clientes com menor saldo de conta apresentam maior incidência de mau crédito. A variável Account_Balance apresenta a maior correlação com a variável alvo (0.35), sendo classificada como correlação positiva moderada. Os gráficos evidenciam que níveis mais elevados de saldo estão associados a maior probabilidade de bom crédito, sugerindo que estabilidade financeira é um fator relevante na avaliação do risco.

Apesar das tendências identificadas, observa-se sobreposição significativa entre classes nos gráficos de dispersão, indicando que o problema não apresenta separação linear clara.
 
## 2. Qualidade dos Dados e Limpeza 
### 2.1. Tratamento de Dados em Falta (Missing Data)
Após uma análise do dataset, através do código, concluímos que a percentagem de dados nulos é zero para todas as variáveis. A validação dessa afirmação foi realizada também através da filtragem de tabelas no Excel, confirmando que não há valores ausentes em nenhuma das variáveis

### 2.2. Outliers e Inconsistências 
Durante a análise exploratória, identificamos a presença de outliers em várias variáveis do conjunto de dados. O número de outliers por variável foi o seguinte:
* Duration_of_Credit_monthly: 70 outliers
* Credit_Amount: 72 outliers
* Duration_in_Current_address: 0 outliers
* Age_years: 23 outliers
* Instalment_per_cent: 0 outliers
* No_of_Credits_at_this_Bank: 6 outliers
* No_of_dependents: 155 outliers

Apesar da presença de valores identificados como outliers, procedeu-se a uma análise do contexto das variáveis para avaliar se estes representavam erros nos dados ou apenas observações extremas mas plausíveis.

No caso das variáveis Credit_Amount, Duration_of_Credit_monthly e Age_years, os valores extremos correspondem a montantes de crédito mais elevados, durações de empréstimo superiores ou clientes com idades mais altas. Estas situações são plausíveis no contexto da concessão de crédito e podem representar perfis de risco distintos, sendo por isso relevantes para a modelação preditiva.

Relativamente à variável No_of_Credits_at_this_Bank, os valores considerados extremos representam clientes com um número superior de créditos ativos, o que constitui informação potencialmente relevante para avaliar o risco financeiro.

No caso da variável No_of_dependents, o elevado número de valores classificados como outliers deve-se ao facto de esta ser uma variável discreta com um número reduzido de categorias possíveis. Assim, o método IQR pode identificar como outliers alguns valores que são, na verdade, observações válidas da variável.

Desta forma, concluiu-se que os valores identificados não representam erros ou inconsistências nos dados. Consequentemente, decidiu-se manter todos os registos no dataset, preservando informação potencialmente relevante para o desenvolvimento do modelo de previsão do risco de crédito.
 
## 3. Engenharia de Atributos (Feature Engineering) 
### 3.1. Transformações Realizadas 
**Encoding:**  
Apesar de algumas variáveis do dataset representarem categorias, estas já se encontram previamente codificadas em formato numérico no conjunto de dados original. Desta forma, não foi necessário aplicar técnicas adicionais de encoding.

**Escalonamento:**   
Com o objetivo de garantir que as variáveis numéricas apresentam a mesma escala, foi aplicado o método StandardScaler às variáveis numéricas contínuas. Este método transforma os dados de forma a que apresentem média próxima de zero e desvio padrão próximo de um.

O escalonamento foi aplicado às variáveis Duration_of_Credit_monthly, Credit_Amount e Age_years, bem como às variáveis derivadas criadas posteriormente, garantindo que todas as variáveis utilizadas na modelação apresentam a mesma escala.

As restantes variáveis numéricas foram mantidas na sua forma original, uma vez que correspondem a escalas categóricas ou contagens discretas com intervalos reduzidos, nas quais a aplicação de escalonamento não acrescentaria benefícios relevantes para a modelação.

 
### 3.2. Criação de Novos Atributos 
Com o objetivo de enriquecer a informação disponível para o modelo e capturar relações adicionais entre as variáveis do datset, foram criadas novas variáveis derivadas das variáveis originais. Sendo elas:
* **Credit_per_month:**
* Foi criada a variável Credit_per_month, que representa o montante de crédito por mês. Esta variável foi calculada através da divisão do montante total do crédito pela duração do empréstimo.
* Por exemplo, alguns dos valores observados para esta variável incluem 58.28, 311.00, 70.08, 176.83 e 180.92, representando diferentes níveis de intensidade do crédito assumido mensalmente pelos clientes.
* Esta métrica permite avaliar o esforço financeiro associado ao empréstimo, uma vez que valores mais elevados podem indicar que o cliente suporta prestações mensais mais elevadas.
* A análise dos gráficos sugere que valores mais elevados desta variável aparecem com maior frequência entre clientes com maior risco de crédito, indicando que créditos elevados em relação à idade podem estar associados a maior probabilidade de incumprimento.

* **Credit_Age_Ratio:**
* Foi também criada a variável Credit Age Ratio, que relaciona o montante de crédito solicitado com a idade do cliente.
* Alguns exemplos de valores observados para esta variável incluem 49.95, 77.75, 36.57, 54.41 e 57.13. Estes valores representam o peso relativo do crédito em função da idade do cliente.
* Esta variável permite analisar a dimensão do crédito relativamente ao perfil etário do cliente, ajudando a identificar situações em que clientes relativamente jovens assumem montantes de
crédito elevados.
* A análise dos gráficos sugere que valores mais elevados desta variável aparecem com maior frequência entre clientes com maior risco de crédito, indicando que créditos elevados em relação à
idade podem estar associados a maior probabilidade de incumprimento.

Uma vez que estes novos atributos foram criados a partir de variáveis numéricas que já tinham sido escalonadas, foi também aplicado Standardscaler a estas variáveis derivadas. Este
procedimento garante que todas as variáveis numéricas utilizadas na modelação apresentam a mesma escala, evitando que diferenças na magnitude das variáveis influenciem o desempenho dos
algoritmos de machine learning.
 
## 4. Dicionário de Dados Final (Pós-Processamento) 
*Listagem final das variáveis que serão entregues ao modelo na Fase 3.* 
 
| Atributo | Tipo | Descrição | 
| :--- | :--- | :--- | 
| `cliente_id` | ID | Removido (não preditivo) | 
| `idade_norm` | Float | Idade após normalização | 
| `is_premium` | Binary | 1 para clientes com plano superior | 
 
## 5. Conclusões da Fase de Exploração 
*O que aprenderam sobre o dataset que não sabiam no final do Milestone 1? Os dados são suficientes 
para avançar para a modelação?* 

## 6. Referências Bibliográficas
1. Prata, M. (2020). Creditability - German Credit Data [Dataset]. Kaggle. Consultado pela última vez a 18 de março de 2026, de https://www.kaggle.com/datasets/mpwolke/cusersmarildownloadsgermancsv/data
2. Hofmann, H. (1994). Statlog (German Credit Data) [Dataset]. UCI Machine Learning Repository. Consultado pela última vez a 19 de março de 2026, de https://archive.ics.uci.edu/dataset/144/statlog+german+credit+data
 --- 
*Data de última atualização: [DD/MM/AAAA]* 

