# Avaliação de Risco de Crédito
 
## Identificação da Equipa 
* **Grupo nº:** 5
* **Membros:** 
  * Iara Gomes - Nº 2023133177 
  * Rita Vinagreiro - Nº 2023136923 
  * Ana Silva - Nº20231345191
 
 
 
## Organização do Repositório 
 
A estrutura deste projeto segue as boas práticas de Ciência de Dados e Engenharia de Software: 
 
* **`data/`**: Armazenamento de dados (dados brutos em `raw/` e processados em `processed/`). 
* **`docs/`**: Documentação técnica detalhada dividida por Milestones (M1, M2 e M3). 
* **`notebooks/`**: Jupyter Notebooks para experimentação, limpeza e modelação. 
* **`src/`**: Código-fonte modular (scripts `.py`) para funções reutilizáveis. 
* **`reports/`**: Relatórios finais, apresentações e exportação de figuras (`figures/`). 
* **`requirements.txt`**: Ficheiro de configuração com as bibliotecas necessárias. 
 
 
 
## 1. Iniciação (Milestone 1) 
### Contexto e Problema de Negócio 
O problema consiste em apoiar uma instituição financeira na decisão de aprovar ou recusar um empréstimo, prevendo a probabilidade de incumprimento de cada cliente com base em dados históricos. 
 
### Objetivos do Projeto 
* **Objetivo 1:** Prever o incumprimento de crédito dos clientes, alcançando um F1-Score mínimo de 0.80, até à Milestone 3. 
* **Objetivo 2:** Identificar as 5 variáveis com maior impacto no risco de crédito, através de técnicas de análise exploratória e interpretação de modelos, até à Milestone 3.
 
### Fonte de Dados 
* **Dataset:** https://www.kaggle.com/datasets/mpwolke/cusersmarildownloadsgermancsv/data
* **Dimensão:** 1000 linhas, 21 colunas
 
### Bibliotecas e ferramentas
Como ferramenta usamos o Jupyter Notebook, para programar e para este projeto pretende-se usar as seguingtes ferramentas: NumPy; Pandas; Seaborn; Mathplotlib e Scikit-learn.  
 
## 2. Exploração (Milestone 2) 
### Limpeza e Preparação 
* [Breve resumo das ações de limpeza tomadas. Detalhes em `docs/M2_exploracao.md`] 
 
### Principais Conclusões (EDA) 
> *Dica: Insere aqui o gráfico mais importante do projeto.* 
* **Ponto-chave:** [Ex: Identificámos que o fator X influencia em 40% o resultado Y, por aplicação 
do método ganho de informação] 
 
 
 
## 3. Modelação (Milestone 3) 
### Abordagem Técnica 
* **Modelos:** [Ex: Random Forest e XGBoost] 
* **Métrica Principal:** [Ex: F1-Score ou RMSE] 
 
 
 
## 4. Finalização (Milestone 4) 
### Resposta ao Problema 
[Resumo da solução e como ela gera valor para o negócio.] 
 
### Recomendações de Inovação 
1. [Sugestão prática baseada nos resultados] 
 
 
 
## Como Reproduzir este Projeto 
1. Clone o repositório: `git clone [url-do-repo]` 
2. Instale as dependências: `pip install -r requirements.txt` 
3. Execute os notebooks na pasta `notebooks/` seguindo a ordem numérica. 
 
 
**Instituição:** Coimbra Business School | ISCAC   
**Curso:** Licenciatura em Ciência de Dados para a Gestão   
**Unidade Curricular:** Projeto em Ciência de Dados   
**Professor Responsável:** Dora Melo (dmelo@iscac.pt)   
