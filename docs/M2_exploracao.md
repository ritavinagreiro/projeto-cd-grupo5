# Milestone 2: Análise Exploratória e Engenharia de Atributos 
 
> **Nota de Revisão:** Este documento pressupõe que o dataset já foi identificado e descrito no 
ficheiro `docs/M1_iniciacao.md`. Caso precise de consultar o significado original das variáveis, 
deve consultar essa Milestone. 
 
## 1. Análise Exploratória de Dados (EDA) 
### 1.1. Distribuição da Variável Alvo 
A variável alvo do presente estudo é Creditability, que indica o nível de risco de crédito do cliente, assumindo dois valores possíveis:<br>
1 - Bom crédito<br>
0 - Mau crédito<br>

A análise da distribuição revela que, num total de 1000 observações:<br>
700 clientes (70%) apresentam bom crédito<br>
300 clientes (30%) apresentam mau crédito<br>

Verifica-se, assim, que a variável alvo apresenta um ligeiro desequilíbrio, existindo uma predominância de clientes classificados como bom crédito.<br>
Tratando-se de uma variável binária, esta não segue uma distribuição normal, mas sim uma distribuição binomial.<br>

**Factos importantes:** <br>
A variável alvo apresenta uma distribuição de 70% / 30%, evidenciando um desequilíbrio moderado.<br>
Um modelo que previsse sempre "Bom crédito" teria automaticamente uma accuracy de 70%.<br>
Assim, para avaliar corretamente o desempenho do modelo, será importante considerar métricas adicionais como Precision, Recall, F1-score e ROC-AUC.<br>
O problema em análise é um caso de classificação binária supervisionada.
 
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
Após uma análise do dataset, através do código concluímos que a percentagem de nulos é zero, para todas as variáveis, e testamos esta afirmnação através da filtragem de tabelas do Excel. 

### 2.2. Outliers e Inconsistências 
*Descrevam se encontraram valores impossíveis (ex: idade = 200) e como os resolveram.* 
 
## 3. Engenharia de Atributos (Feature Engineering) 
### 3.1. Transformações Realizadas 
* **Encoding:** (Ex: "Convertemos a variável 'Género' em numérica usando One-Hot Encoding.") 
* **Escalonamento:** (Ex: "Aplicámos o StandardScaler nas variáveis numéricas para que todas 
fiquem na mesma escala.") 
 
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

