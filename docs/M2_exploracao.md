# Milestone 2: Análise Exploratória e Engenharia de Atributos 
 
> **Nota de Revisão:** Este documento pressupõe que o dataset já foi identificado e descrito no 
ficheiro `docs/M1_iniciacao.md`. Caso precise de consultar o significado original das variáveis, 
deve consultar essa Milestone. 
 
## 1. Análise Exploratória de Dados (EDA) 
### 1.1. Distribuição da Variável Alvo 
A variável alvo do presente estudo é Creditability, que indica o nível de risco de crédito do cliente, assumindo dois valores possíveis: 

1 - Bom crédito 

0 - Mau crédito 

A análise da distribuição revela que, num total de 1000 observações: 

700 clientes (70%) apresentam bom crédito 

300 clientes (30%) apresentam mau crédito 

Verifica-se, assim, que a variável alvo apresenta um ligeiro desequilíbrio, existindo uma predominância de clientes classificados como bom crédito. 

Tratando-se de uma variável binária, esta não segue uma distribuição normal, mas sim uma distribuição binomial. 

**Factos importantes:**
A variável alvo apresenta uma distribuição de 70% / 30%, evidenciando um desequilíbrio moderado. 

Um modelo que previsse sempre "Bom crédito" teria automaticamente uma accuracy de 70%. 

Assim, para avaliar corretamente o desempenho do modelo, será importante considerar métricas adicionais como Precision, Recall, F1-score e ROC-AUC.

O problema em análise é um caso de classificação binária supervisionada.
 
### 1.2. Correlações Relevantes 
*Quais as variáveis que têm maior relação com o problema? Incluam referências a gráficos que 
geraram no Kaggle.* 
* **Atributo A vs. Alvo:** (Ex: "Notámos que quanto maior a idade, menor a probabilidade de 
cancelamento.") 
* **Atributo B vs. Alvo:** (Ex: "O tipo de contrato mensal está fortemente ligado à saída de 
clientes.") 
 
## 2. Qualidade dos Dados e Limpeza 
### 2.1. Tratamento de Dados em Falta (Missing Data) 
* **Colunas afetadas:** [Lista de colunas] 
* **Estratégia adotada:** (Ex: "Substituímos os nulos da coluna 'Salário' pela mediana para 
evitar o impacto de outliers.") 
 
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

