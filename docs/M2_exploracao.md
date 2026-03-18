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
 
## 3. Engenharia de Atributos (Feature Engineering) 
### 3.1. Transformações Realizadas 
**Encoding:**  
Apesar de algumas variáveis do dataset representarem categorias, estas já se encontram previamente codificadas em formato numérico no conjunto de dados original. Desta forma, não foi necessário aplicar técnicas adicionais de encoding.

**Escalonamento:**   
Com o objetivo de garantir que as variáveis numéricas apresentam a mesma escala, foi aplicado o método StandardScaler às variáveis numéricas contínuas. Este método transforma os dados de forma a que apresentem média próxima de zero e desvio padrão próximo de um.

O escalonamento foi aplicado às variáveis Duration_of_Credit_monthly, Credit_Amount e Age_years, bem como às variáveis derivadas criadas posteriormente, garantindo que todas as variáveis utilizadas na modelação apresentam a mesma escala.

As restantes variáveis numéricas foram mantidas na sua forma original, uma vez que correspondem a escalas categóricas ou contagens discretas com intervalos reduzidos, nas quais a aplicação de escalonamento não acrescentaria benefícios relevantes para a modelação.

 
### 3.2. Criação de Novos Atributos 
*Descrevam as variáveis que criaram para ajudar o modelo.* 
* **Nova Variável [Nome]:** (Ex: "Criámos a 'Tenure_Per_Year' que divide o tempo de contrato 
pela idade do cliente.") 
 
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
 --- 
*Data de última atualização: [DD/MM/AAAA]* 

