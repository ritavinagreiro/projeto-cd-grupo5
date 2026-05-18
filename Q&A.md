# Q&A Assíncrono - Milestone 4

## 1. Porque foi escolhido o modelo *XGBoost + SMOTE* como modelo final?

O modelo *XGBoost + SMOTE* foi escolhido porque apresentou o melhor equilíbrio entre desempenho global e capacidade de identificação da classe de incumprimento.

Ao longo da modelação, verificou-se que vários modelos apresentavam bons valores de *F1-Score*, mas tinham dificuldade em identificar corretamente os clientes em incumprimento. Esta era a principal preocupação do projeto, porque, no contexto da concessão de crédito, o erro mais crítico é classificar como cumpridor um cliente que, na realidade, pode entrar em incumprimento.

O modelo final atingiu, no conjunto de teste, um *F1-Score* de **0.8213** e um *Recall* da classe de incumprimento de **0.7500**, cumprindo simultaneamente as duas metas definidas no objetivo SMART do projeto:

- *F1-Score* ≥ 0.80;
- *Recall* da classe de incumprimento ≥ 0.70.

Além disso, o modelo conseguiu identificar corretamente **45 dos 60 clientes em incumprimento**, reduzindo os falsos negativos face ao modelo *baseline* de Regressão Logística. Assim, a escolha do *XGBoost + SMOTE* não foi feita apenas com base no desempenho estatístico, mas sobretudo pela sua utilidade prática como ferramenta de apoio à decisão de crédito.

## 2. Porque foi dada prioridade ao *Recall* da classe de incumprimento em vez da *Accuracy*?

A *Accuracy* não foi utilizada como métrica principal porque o *dataset* apresenta desequilíbrio entre classes: cerca de **70% dos clientes estão em cumprimento** e **30% em incumprimento**. Neste contexto, um modelo poderia obter uma *Accuracy* aparentemente elevada classificando muitos clientes como cumpridores, mas falhando na identificação dos clientes de maior risco.

Por esse motivo, foi dada maior importância ao *Recall* da classe de incumprimento. Esta métrica mede a capacidade do modelo para identificar corretamente os clientes que realmente entram em incumprimento.

No contexto bancário, os falsos negativos representam o erro mais grave. Um falso negativo corresponde a um cliente que entra em incumprimento, mas que o modelo classificou como cumpridor. Numa situação real, este erro poderia levar à aprovação indevida de crédito e originar perdas financeiras para a instituição.

Assim, o objetivo não foi apenas obter um bom desempenho global, mas garantir que o modelo tivesse capacidade para sinalizar uma parte significativa dos clientes de risco. O modelo final atingiu um *Recall* de **0.7500**, ou seja, identificou **75% dos clientes em incumprimento** no conjunto de teste.

## 3. O modelo pode ser usado automaticamente para aprovar ou recusar crédito?

Não. O modelo deve ser entendido como uma ferramenta de apoio à decisão e não como um mecanismo automático de aprovação ou recusa de crédito.

Apesar de apresentar bons resultados, o modelo tem limitações. Foi desenvolvido com o *German Credit Data*, um conjunto de dados com **1000 observações**, que pode não representar totalmente a realidade atual de uma instituição financeira portuguesa. Além disso, faltam variáveis importantes para uma análise de crédito real, como rendimento mensal, taxa de esforço atual, histórico recente de pagamentos, taxa de juro, garantias reais e informação económica atualizada.

Na prática, o modelo deve funcionar como um sistema de alerta ou triagem inicial. Clientes classificados como maior risco podem ser encaminhados para análise adicional, pedido de garantias ou revisão manual. Já os clientes classificados como baixo risco podem seguir um processo de análise mais simples, sem dispensar totalmente a validação humana.

Desta forma, o modelo ajuda a tornar a análise de crédito mais consistente e baseada em dados, mas a decisão final deve continuar a envolver julgamento humano, documentação atualizada, regras internas da instituição e avaliação do contexto económico.
