# Relatório de Conclusão e Entrega de Valor (Milestone 4) 
 
## 1. Síntese de Resultados e Impacto 
### **O Problema Resolvido:**  
O projeto tinha como objetivo desenvolver um modelo preditivo capaz de apoiar uma instituição financeira na identificação de clientes com maior risco de incumprimento de crédito.    
Esse objetivo foi alcançado através da construção e avaliação de vários modelos de classificação supervisionada, tendo sido selecionado como modelo final o **XGBoost com SMOTE**, por cumprir simultaneamente as metas definidas para o projeto:

  * **F1-Score ≥ 0,80**
  * **Recall da classe de incumprimento ≥ 0,70**

O modelo final obteve os seguintes resultados no conjunto de teste:
| Métrica | Resultado | Interpretação simples |
|---|---:|---|
| F1-Score | 0,8213 | O modelo mantém um bom equilíbrio entre acertos globais e deteção de clientes de risco. |
| Recall do incumprimento | 0,7500 | O modelo identifica 75% dos clientes que efetivamente entram em incumprimento. |
| AUC-ROC | 0,8090 | O modelo apresenta boa capacidade para distinguir clientes cumpridores de clientes de risco. |

### **Interpretação dos Resultados:**   
Em termos práticos, no conjunto de teste existiam **60 clientes em incumprimento**.  
O modelo final conseguiu identificar corretamente **45 desses 60 clientes**, deixando por identificar **15 clientes de risco**.

Comparando com o modelo inicial de Regressão Logística, a melhoria é relevante:
| Indicador | Modelo *baseline* | Modelo final |
|---|---:|---:|
| Clientes em incumprimento corretamente identificados | 31 | 45 |
| Clientes em incumprimento não identificados | 29 | 15 |

Isto significa que o modelo final reduziu de forma significativa o erro mais crítico neste contexto: aprovar ou considerar como seguro um cliente que, na realidade, apresenta risco de incumprimento.

No entanto, esta melhoria teve um custo: o modelo passou a classificar mais clientes cumpridores como clientes de risco. Esta situação corresponde a falsos positivos. Apesar disso, no contexto da concessão de crédito, este comportamento é aceitável, porque é normalmente menos prejudicial analisar um cliente cumpridor com mais detalhe do que aprovar automaticamente um cliente com elevada probabilidade de incumprimento.

### **Valor para o Utilizador/Negócio:**   
O principal valor do projeto está na criação de uma ferramenta de apoio à decisão de crédito.   

O modelo não deve substituir a decisão humana, mas pode ajudar uma instituição financeira a:
1. Identificar antecipadamente clientes com maior risco de incumprimento;
2. Reduzir perdas financeiras associadas à aprovação de crédito de elevado risco;
3. Priorizar a análise manual dos clientes sinalizados como mais arriscados;
4. Apoiar decisões mais consistentes, baseadas em dados e não apenas em avaliação subjetiva;
5. Criar categorias de risco, distinguindo clientes de baixo risco e alto risco com base na probabilidade prevista pelo modelo.

Assim, a solução transforma dados históricos de crédito em conhecimento útil para a gestão do risco financeiro.

## 2. Análise Crítica e Limitações 
Apesar dos resultados positivos, o modelo apresenta limitações que devem ser reconhecidas de forma transparente.
 
### **Limitações dos Dados:**  
O projeto foi desenvolvido com o dataset *German Credit Data*, composto por 1000 observações. Embora este conjunto de dados seja útil para fins académicos, apresenta algumas limitações:

- Os dados não representam necessariamente a realidade atual de uma instituição financeira portuguesa;
- A dimensão do dataset é relativamente reduzida para um problema de risco de crédito;
- Algumas variáveis estão codificadas numericamente, o que dificulta a interpretação direta por utilizadores não técnicos;
- Não existem variáveis importantes que, num contexto real, poderiam melhorar a análise, como rendimento mensal, taxa de esforço, situação profissional detalhada, histórico recente de incumprimentos, taxa de juro, garantias reais ou evolução económica.

Além disso, o *dataset* apresenta desequilíbrio entre classes, com maior proporção de clientes em cumprimento do que em incumprimento. Este desequilíbrio obrigou à utilização de técnicas como o *SMOTE*, que ajudam o modelo a aprender melhor os padrões da classe minoritária.

### **Limitações do Modelo:**  
O modelo final apresenta bom desempenho no conjunto de teste, mas não é perfeito.  
A validação cruzada revelou que o *Recall* médio da classe de incumprimento foi inferior ao valor observado no conjunto de teste, o que indica que a capacidade de deteção de clientes de risco pode variar consoante a amostra utilizada.

Também importa destacar que:
- O modelo faz previsões com base em padrões estatísticos, mas não prova relações de causalidade;
- O ajuste do threshold melhora a deteção de incumprimentos, mas pode aumentar os falsos positivos;
- O modelo pode ter dificuldade em identificar alguns perfis intermédios, especialmente clientes com maior esforço financeiro mensal;
- O desempenho deve ser validado com dados novos antes de qualquer aplicação real.

### **Contextos de Falha:**   
O modelo não deve ser utilizado de forma automática e isolada para aprovar ou recusar crédito.  
A sua utilização é mais adequada como ferramenta de triagem inicial ou alerta de risco.

O modelo pode falhar em situações como:

- Clientes com perfis muito diferentes dos existentes no dataset de treino;
- Alterações económicas significativas, como inflação elevada, desemprego ou subida das taxas de juro;
- Mudanças nas políticas internas de crédito de uma instituição;
- Dados incompletos, mal registados ou com variáveis diferentes das utilizadas no treino.

Por estes motivos, a decisão final deve continuar a envolver análise humana e validação por especialistas.
 
## 3. Considerações Éticas e de Viés 
### **Privacidade:**   
O *dataset* utilizado não contém identificadores pessoais diretos, como nomes, moradas ou números de identificação.  
Ainda assim, num contexto real, a utilização de modelos de crédito deve respeitar regras rigorosas de proteção de dados, garantindo que apenas são usadas variáveis necessárias, proporcionais e devidamente autorizadas.

### **Viés e justiça na decisão:**  
Modelos de risco de crédito podem reproduzir ou amplificar desigualdades existentes nos dados históricos.  
Variáveis relacionadas com saldo bancário, poupanças, idade, garantias ou histórico de crédito podem refletir diferenças socioeconómicas entre clientes.

Por isso, é essencial garantir que o modelo:
- Não discrimina injustamente determinados grupos de clientes;
- É avaliado regularmente quanto à existência de enviesamentos;
- É usado como apoio à decisão, e não como mecanismo automático de exclusão;
- Permite revisão humana em casos duvidosos ou de maior impacto para o cliente.

### **Transparência e explicabilidade:**   
A utilização da importância dos atributos permitiu compreender quais as variáveis que mais influenciaram as previsões do modelo.  
Esta análise é relevante porque evita que o modelo funcione como uma “caixa negra” e permite explicar, de forma mais clara, os fatores associados ao risco de crédito.

As variáveis mais relevantes identificadas foram:
- *Account_Balance*
- *Value_Savings_Stocks*
- *Guarantors*
- *Payment_Status_of_Previous_Credit*
- *Duration_of_Credit_monthly*

Esta informação permite que a instituição compreenda melhor os fatores de risco e complemente a previsão automática com análise financeira e julgamento profissional.
 
## 4. Roadmap e Trabalhos Futuros   
* **1. Interpretabilidade com *SHAP*** : Integrar a biblioteca *SHAP* para gerar explicações individuais de cada previsão. Isto permitiria ao analista de crédito perceber por que razão o modelo classificou um cliente como alto risco ("o saldo de conta negativo e a duração de 48 meses aumentaram a probabilidade de incumprimento em X%"), cumprindo simultaneamente requisitos regulatórios de explicabilidade.

* **2. Enriquecimento com Variáveis Comportamentais e Macroeconómicas**  
Incorporar dados adicionais que capturem a dinâmica temporal do comportamento financeiro:
  * Histórico de pagamentos mensais (pontualidade, atrasos)
  * Rácio de utilização de crédito rotativo
  * Indicadores macroeconómicos externos (taxa de desemprego, *Euribor*) para ajuste de risco sistémico

* **3. Deployment — Interface Web com Streamlit**  : Desenvolver uma aplicação web simples com Streamlit que permita a qualquer analista de crédito inserir os dados de um novo cliente e obter de imediato uma classificação de risco (Baixo / Médio / Alto) com a probabilidade associada e as principais variáveis que influenciaram a decisão. Isto transformaria o modelo num produto utilizável por equipas não-técnicas.

* **4. Monitorização Contínua com PSI**  : Implementar o cálculo do *Population Stability Index (PSI)* para detetar automaticamente quando a distribuição dos dados de entrada se afasta significativamente do perfil de treino — sinal de que o modelo pode estar a perder validade (*model drift*) e precisa de ser recalibrado.

* **5. Teste com Dataset Português ou Europeu**  : Validar a metodologia num dataset de crédito português ou europeu para aferir a transferibilidade do modelo para o contexto real onde seria aplicado. O *German Credit Data*, apesar de ser um benchmark académico reconhecido, tem limitações de representatividade geográfica e temporal.

## 5. Conclusão Final
O projeto demonstrou que é possível utilizar técnicas de *Machine Learning* para apoiar decisões de crédito, identificando clientes com maior probabilidade de incumprimento.

O modelo final, *XGBoost com SMOTE*, cumpriu os objetivos definidos no início do projeto, alcançando um *F1-Score* de 0,8213 e um *Recall* de incumprimento de 0,7500.  

Em linguagem simples, o modelo conseguiu identificar 3 em cada 4 clientes em incumprimento, reduzindo significativamente o erro mais crítico no contexto da concessão de crédito.

Apesar das limitações identificadas, a solução apresenta valor prático como ferramenta de apoio à decisão, permitindo uma análise mais orientada por dados, uma melhor gestão do risco e uma priorização mais eficiente dos clientes que exigem avaliação adicional.

O projeto não deve ser visto como uma solução definitiva, mas sim como uma base sólida para evolução futura, com potencial para ser melhorada através de novos dados, maior explicabilidade, validação externa e desenvolvimento de uma interface prática para utilizadores não técnicos.

---

**Data de Conclusão:** 18/05/2026   
**Versão do Projeto:** v4.0 Final 
