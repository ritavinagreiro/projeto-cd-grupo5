# Milestone 2: Análise Exploratória e Engenharia de Atributos 
 
## 1. Análise Exploratória de Dados (EDA) 
### 1.1. Distribuição da Variável Alvo 
A variável alvo do presente estudo é *Creditability*, que indica o nível de risco de crédito do cliente, assumindo dois valores possíveis:
* 1 - Cumprimento
* 0 - Incumprimento

A análise da distribuição da variável alvo (`distribuicao_creditability.png`) revela que, num total de 1000 observações:  
* 700 clientes (70%) encontram-se em situação de cumprimento
* 300 clientes (30%) encontram-se em situação de incumprimento

Verifica-se, assim, que a variável alvo apresenta um desequilíbrio moderado, existindo uma predominância de clientes classificados como estando em cumprimento. 

Tratando-se de uma variável binária, *Creditability* não segue uma distribuição normal, mas sim uma distribuição binomial.

**Factos importantes:** 
* A variável alvo apresenta uma distribuição de 70% / 30%, evidenciando um desequilíbrio moderado.
* Um modelo que previsse sempre "Cumprimento" teria automaticamente uma *accuracy* de 70%.
* Assim, para avaliar corretamente o desempenho do modelo, será importante considerar métricas adicionais como *Precision*, *Recall*, *F1-Score* e *AUC-ROC*.
* O problema em análise é um caso de classificação binária supervisionada.
 
### 1.2. Correlações Relevantes 
A análise da matriz de correlação  (`matriz_correlacao.png`) permitiu identificar as variáveis com maior associação à variável alvo (*Creditability*). Destacam-se:

* *Account_Balance* (0.35) – correlação positiva moderada
* *Payment_Status_of_Previous_Credit* (0.23) – correlação positiva fraca
* *Value_Savings_Stocks* (0.17) – correlação positiva fraca
* *Credit_Amount* (-0.15) – correlação negativa fraca
* *Duration_of_Credit_monthly* (-0.21) – correlação negativa fraca

A variável *Account_Balance* apresenta a maior correlação com a variável alvo, sugerindo que o saldo da conta é um dos principais fatores associados ao risco de crédito.

As variáveis *Duration_of_Credit_monthly* e *Credit_Amount* indicam que empréstimos de maior duração e maior montante tendem a estar associados a maior probabilidade de incumprimento.

De forma geral, as correlações observadas são moderadas ou fracas, indicando que nenhuma variável isoladamente explica completamente o comportamento da variável alvo. Este resultado reforça a necessidade de recorrer a uma abordagem multivariada na fase de modelação.

#### **Análise Gráfica das Variáveis Mais Relevantes**

***Duration_of_Credit_monthly* vs *Creditability*:** A análise através de *boxplots* evidencia diferenças na distribuição da duração do crédito entre clientes em cumprimento e em incumprimento (`figura3.png`). Observa-se que os clientes em situação de incumprimento tendem, em média, a apresentar créditos com maior duração. Esta tendência está alinhada com a correlação negativa fraca identificada (-0.21), sugerindo que empréstimos com prazos mais longos podem estar associados a uma maior probabilidade de incumprimento.

***Credit_Amount* vs *Creditability*:** A análise da variável *Credit_Amount* (`figura2.png`) revela que montantes de crédito mais elevados tendem a estar associados a maior risco de incumprimento. Embora exista alguma dispersão nos dados, verifica-se que os clientes em incumprimento apresentam, em média, valores de crédito superiores. Este resultado está em linha com a correlação negativa observada (-0.15), sugerindo que empréstimos de maior valor podem representar um maior nível de risco financeiro.

***Age_years* vs *Creditability*:** A variável *Age_years* (`figura4.png`) apresenta diferenças menos acentuadas entre as classes. Apesar de se observar alguma variação, não existe uma separação clara entre clientes em cumprimento e em incumprimento com base apenas na idade. Assim, a idade, quando analisada isoladamente, não parece ser um fator determinante na previsão do risco de crédito.

Apesar das diferenças observadas, verifica-se alguma sobreposição entre as distribuições das classes. Isto indica que nenhuma variável, analisada individualmente, permite distinguir totalmente os clientes em cumprimento dos clientes em incumprimento, reforçando a necessidade de recorrer a uma abordagem multivariada na fase de modelação.

### 1.3. **Resposta às Perguntas de Investigação (Análise Exploratória)**  
**Quais são as características financeiras e demográficas mais comuns entre os clientes em incumprimento de crédito?**  
Os resultados indicam que os clientes em incumprimento tendem a apresentar montantes de crédito mais elevados e prazos de financiamento mais longos, conforme evidenciado pelos *boxplots* analisados. Adicionalmente, variáveis como o *Credit_per_Month* sugerem um maior esforço financeiro mensal nestes clientes. A análise da variável *Account_Balance* revela ainda que níveis mais baixos de saldo estão associados a maior risco. Em termos demográficos, a idade isoladamente não apresenta forte capacidade discriminativa, embora a variável *Credit_Age_Ratio* sugira maior risco em clientes mais jovens com créditos elevados.

**Existe relação entre o montante do crédito e a ocorrência de incumprimento?**  
Sim. A análise da variável *Credit_Amount*, tanto em termos de correlação como através dos boxplots, indica que valores mais elevados estão associados a maior probabilidade de incumprimento. No entanto, esta relação não é isoladamente determinante, sendo influenciada por outros fatores financeiros.

**De que forma a duração do crédito influencia a ocorrência de incumprimento?**  
A duração do crédito apresenta influência no risco de incumprimento, sendo que créditos com maior duração estão associados a maior probabilidade de incumprimento. Esta relação é visível tanto na análise de correlação como na distribuição observada nos gráficos, podendo ser explicada pelo aumento da exposição ao risco ao longo do tempo.
 
## 2. Qualidade dos Dados e Limpeza 
### 2.1. Tratamento de Dados em Falta (*Missing Data*)
Após a análise do *dataset* através do código, concluiu-se que não existem valores nulos em nenhuma das variáveis. Esta validação foi também confirmada através da filtragem das tabelas no Excel, reforçando que o conjunto de dados não apresenta valores ausentes.

### 2.2. Outliers e Inconsistências 
Durante a análise exploratória, identificamos a presença de *outliers* em várias variáveis do conjunto de dados. O número de outliers por variável foi o seguinte:
* *Duration_of_Credit_monthly*: 70 *outliers*
* *Credit_Amount*: 72 *outliers*
* *Duration_in_Current_address*: 0 *outliers*
* *Age_years*: 23 *outliers*
* *Instalment_per_cent*: 0 *outliers*
* *No_of_Credits_at_this_Bank*: 6 *outliers*

Apesar da presença de valores identificados como *outliers*, procedeu-se a uma análise do contexto das variáveis para perceber se estes representavam erros nos dados ou apenas observações extremas mas plausíveis.

No caso das variáveis *Credit_Amount*, *Duration_of_Credit_monthly* e *Age_years*, os valores extremos correspondem a montantes de crédito mais elevados, durações de empréstimo superiores ou clientes com idades mais altas. Estas situações são plausíveis no contexto da concessão de crédito e podem representar perfis de risco distintos, sendo por isso relevantes para a modelação preditiva.

Relativamente à variável *No_of_Credits_at_this_Bank*, os valores considerados extremos representam clientes com um número superior de créditos ativos neste banco, o que constitui informação potencialmente relevante para avaliar o risco financeiro.

Desta forma, concluiu-se que os valores identificados não representam erros ou inconsistências nos dados. Consequentemente, decidiu-se manter todos os registos no *dataset*, preservando informação potencialmente relevante para o desenvolvimento do modelo de previsão do risco de crédito.

### 2.3. Seleção de Atributos

A seleção de atributos constitui uma etapa importante na preparação dos dados, tendo como objetivo identificar e manter as variáveis mais relevantes para a previsão do risco de crédito, removendo aquelas que apresentam menor contributo para o modelo.

Neste contexto, a decisão de seleção de atributos foi apoiada pela matriz de correlação e pela análise gráfica das variáveis, nomeadamente através de histogramas e *boxplots*.

A matriz de correlação evidenciou que algumas variáveis, como *Telephone*, *Foreign_Worker* e *No_of_dependents*, apresentam valores de correlação muito próximos de zero relativamente à variável alvo (*Creditability*), sugerindo uma fraca associação com o risco de incumprimento.

Além disso, a análise gráfica destas variáveis não revelou padrões relevantes nem diferenças significativas entre clientes em cumprimento e em incumprimento, indicando uma reduzida capacidade discriminativa.

Com base nestes resultados, optou-se pela remoção destas variáveis do *dataset*, uma vez que a sua inclusão não acrescentaria valor significativo ao processo de modelação, podendo introduzir ruído e aumentar desnecessariamente a complexidade do modelo.

As restantes variáveis foram mantidas, por apresentarem relações relevantes com o problema ou por contribuírem para enriquecer a informação disponível para o modelo.

Esta abordagem permitiu obter um conjunto de dados mais consistente, focado nas variáveis com maior potencial preditivo e adequado à fase de modelação.

## 3. Engenharia de Atributos (*Feature Engineering*)

### 3.1. Transformações Realizadas

**Encoding:**  
Apesar de algumas variáveis do *dataset* representarem categorias, estas já se encontram previamente codificadas em formato numérico no conjunto de dados original. Desta forma, não foi necessário aplicar técnicas adicionais de *encoding*.

**Escalonamento:**  
Com o objetivo de garantir que as variáveis numéricas apresentavam uma escala comparável, foi aplicado o transformador `StandardScaler`, do *Scikit-learn*, às variáveis numéricas contínuas *Duration_of_Credit_monthly*, *Credit_Amount*, *Age_years* e às variáveis derivadas criadas posteriormente.

A padronização transforma os dados de forma a que apresentem média próxima de zero e desvio padrão próximo de um, permitindo reduzir o impacto das diferenças de escala entre variáveis. Este procedimento é especialmente relevante em algoritmos sensíveis à escala dos dados, contribuindo para uma modelação mais equilibrada (*Géron, 2019*).

Importa referir que, no código, as variáveis derivadas foram criadas antes do escalonamento, com base nos valores originais das variáveis numéricas. Só depois foi aplicado o `StandardScaler`, garantindo que todas as variáveis contínuas utilizadas na modelação ficaram numa escala comparável.

As restantes variáveis numéricas foram mantidas na sua forma original, uma vez que correspondem sobretudo a categorias codificadas ou a contagens discretas com intervalos reduzidos, nas quais a aplicação de escalonamento não acrescentaria benefícios relevantes para a modelação.

### 3.2. Criação de Novos Atributos
Com o objetivo de enriquecer a informação disponível para o modelo e captar relações adicionais entre as variáveis do *dataset*, foram criadas duas novas variáveis derivadas das variáveis originais: *Credit_per_Month* e *Credit_Age_Ratio*.

***Credit_per_Month*:**  
Foi criada a variável *Credit_per_Month*, que representa o montante de crédito por mês. Esta variável foi calculada através da divisão do montante total do crédito pela duração do empréstimo.

Esta métrica permite avaliar o esforço financeiro mensal associado ao crédito, uma vez que valores mais elevados podem indicar que o cliente suporta uma maior intensidade de crédito por mês.

A análise do *boxplot* (`boxplot_credit_per_month.png`) sugere que valores mais elevados desta variável aparecem com alguma frequência entre clientes com maior risco de crédito. Assim, um maior esforço financeiro mensal pode estar associado a uma maior probabilidade de incumprimento.

***Credit_Age_Ratio*:**  
Foi também criada a variável *Credit_Age_Ratio*, que relaciona o montante de crédito solicitado com a idade do cliente.

Esta variável permite analisar a dimensão do crédito relativamente ao perfil etário do cliente, ajudando a identificar situações em que clientes relativamente jovens assumem montantes de crédito elevados.

A análise do *boxplot* (`boxplot_credit_age_ratio.png`) sugere que valores mais elevados desta variável aparecem com maior frequência entre clientes em incumprimento. Isto indica que créditos elevados em relação à idade podem estar associados a maior probabilidade de incumprimento.

As novas variáveis foram criadas a partir dos valores originais das variáveis numéricas. Posteriormente, foi aplicado o `StandardScaler` às variáveis derivadas, garantindo que todas as variáveis numéricas contínuas utilizadas na modelação apresentam uma escala comparável.

#### 3.2.1 Análise de Correlação com as Novas Variáveis
A matriz de correlação (`matriz_correlacao.png`) permitiu identificar algumas relações entre as variáveis do *dataset* após a criação dos novos atributos.

Observa-se uma correlação relativamente elevada entre *Credit_Amount* e *Duration_of_Credit_monthly*, indicando que empréstimos de maior valor tendem a estar associados a prazos mais longos.

As variáveis derivadas *Credit_per_Month* e *Credit_Age_Ratio* apresentam também correlação com *Credit_Amount*, o que é esperado, uma vez que foram construídas a partir desta variável.

Relativamente à variável alvo *Creditability*, continuam a destacar-se variáveis relacionadas com o saldo da conta, a duração do crédito e o montante do empréstimo, sugerindo que estes fatores podem influenciar o risco de incumprimento.

#### 3.2.2 Multicolinearidade
Para perceber se existiam variáveis muito relacionadas entre si, foi calculado o *Variance Inflation Factor* (*VIF*).

A análise mostrou que algumas variáveis apresentam valores de *VIF* mais elevados. Isto já era esperado em alguns casos, principalmente nas variáveis criadas a partir de outras variáveis do *dataset*, como acontece com as variáveis derivadas.

Apesar disso, estes valores não impedem a utilização das variáveis na fase de modelação. No entanto, devem ser considerados na interpretação dos resultados, uma vez que variáveis muito correlacionadas podem influenciar a estabilidade de alguns modelos.

Assim, conclui-se que existem alguns sinais de multicolinearidade, mas não ao ponto de comprometer o avanço para a modelação.
 
## 4. Dicionário de Dados Final (Pós-Processamento) 
 
| Atributo | Tipo | Descrição |
| :--- | :--- | :--- |
| *Creditability* | Binária | Variável alvo do modelo |
| *Account_Balance* | Inteiro (Ordinal) | Saldo da conta corrente |
| *Duration_of_Credit_monthly* | Float | Prazo do empréstimo em meses |
| *Payment_Status_of_Previous_Credit* | Inteiro (Ordinal) | Estado do pagamento de créditos anteriores |
| *Purpose* | Inteiro (Nominal) | Finalidade do crédito |
| *Credit_Amount* | Float | Valor do empréstimo solicitado |
| *Value_Savings_Stocks* | Inteiro (Ordinal) | Valor existente em poupanças ou títulos |
| *Length_of_current_employment* | Inteiro (Ordinal) | Tempo de emprego atual |
| *Instalment_per_cent* | Inteiro | Percentagem do rendimento comprometida com o crédito |
| *Sex_Marital_Status* | Inteiro (Nominal) | Estado civil e sexo |
| *Guarantors* | Inteiro (Nominal) | Existência de fiador ou co-candidato |
| *Duration_in_Current_address* | Inteiro | Tempo de residência na morada atual |
| *Most_valuable_available_asset* | Inteiro (Nominal) | Ativo mais valioso |
| *Age_years* | Float | Idade do cliente em anos |
| *Concurrent_Credits* | Inteiro (Nominal) | Existência de créditos em simultâneo |
| *Type_of_apartment* | Inteiro (Nominal) | Tipo de habitação |
| *No_of_Credits_at_this_Bank* | Inteiro | Número de créditos neste banco |
| *Occupation* | Inteiro (Nominal) | Ocupação profissional |
| *Credit_per_Month* | Float | Montante de crédito por mês |
| *Credit_Age_Ratio* | Float | Relação entre crédito solicitado e idade do cliente | 

## 5. Conclusões da Fase de Exploração 
A análise exploratória dos dados permitiu compreender melhor o comportamento do risco de crédito e preparar o conjunto de dados para a fase de modelação.

Inicialmente, foram identificados alguns valores extremos em variáveis como *Credit_Amount*, *Duration_of_Credit_monthly* e *Age_years*. No entanto, após análise do contexto, concluiu-se que estes valores não representam erros, mas sim situações reais e plausíveis no âmbito da concessão de crédito. Por esse motivo, optou-se por manter os registos, preservando informação relevante para a identificação de diferentes perfis de risco.

A análise de correlações mostrou que *Account_Balance* é uma das variáveis mais associadas à variável alvo, sugerindo que o saldo da conta bancária tem uma relação importante com o risco de incumprimento. Verificou-se também que créditos de maior montante e maior duração tendem a estar mais associados a situações de incumprimento.

Foram ainda criadas duas novas variáveis, *Credit_per_Month* e *Credit_Age_Ratio*, com o objetivo de captar relações adicionais entre o montante do crédito, a duração do empréstimo e a idade do cliente. Estas variáveis permitem enriquecer a informação disponível para o modelo e podem contribuir para uma melhor identificação de perfis de risco.

Assim, conclui-se que os dados apresentam qualidade suficiente para avançar para a fase de modelação, embora devam ser consideradas algumas limitações, nomeadamente a existência de variáveis categóricas codificadas numericamente e possíveis sinais de multicolinearidade entre alguns atributos.


## 6. Referências Bibliográficas
1. Prata, M. (2020). *Creditability - German Credit Data* [Dataset]. Kaggle. Consultado pela última vez a 18 de março de 2026, de https://www.kaggle.com/datasets/mpwolke/cusersmarildownloadsgermancsv/data
2. Hofmann, H. (1994). *Statlog (German Credit Data)* [Dataset]. UCI Machine Learning Repository. Consultado pela última vez a 24 de março de 2026, de https://archive.ics.uci.edu/dataset/144/statlog+german+credit+data
3. Géron, A. (2019). *Mãos à obra: Aprendizado de máquina com Scikit-Learn e TensorFlow*. Starlin Alta Editora e Consultoria Eireli.
 --- 
*Data de última atualização: 18/05/2026* 

