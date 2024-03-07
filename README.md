# Python Insights - Analisando Dados com Python

### Case - Cancelamento de Clientes

Você foi contratado por uma empresa com mais de 800 mil clientes para um projeto de Dados. Recentemente a empresa percebeu que da sua base total de clientes, a maioria são clientes inativos, ou seja, que já cancelaram o serviço.

Precisando melhorar seus resultados, ela quer entender os principais motivos desses cancelamentos e quais as ações mais eficientes para reduzir esse número.

## Passo a passo

1. **Importar a Base de Dados:**  
   - Carregar os dados de cancelamento dos clientes de um arquivo CSV.

2. **Visualizar a Base de Dados:**  
   - Examinar a estrutura e conteúdo da base de dados para identificar colunas relevantes e informações úteis.

3. **Corrigir a Base de Dados:**  
   - Tratar valores ausentes e remover informações irrelevantes que possam atrapalhar a análise.

4. **Análise de Cancelamento:**  
   - Analisar a distribuição dos cancelamentos para entender a proporção de clientes que cancelaram o serviço.

5. **Análise da Causa do Cancelamento:**  
   - Investigar as principais causas de cancelamento e propor ações corretivas para reduzir o número de cancelamentos.

```python
# Passo 1: Importar a base de dados
import pandas as pd 

tabela = pd.read_csv("cancelamentos_sample.csv")

# Passo 2: Visualizar a base de dados
tabela = tabela.drop(columns="CustomerID")
display(tabela)

# Passo 3: Corrigir a base de dados
display(tabela.info()) 
tabela = tabela.dropna() 
display(tabela.info()) 

# Passo 4: Análise de cancelamento
display(tabela["cancelou"].value_counts(normalize=True)) 

# Passo 5: Análise da causa do cancelamento
import plotly.express as px 

for coluna in tabela.columns:
    grafico = px.histogram(tabela, x=coluna, color="cancelou")
    grafico.show()

# Ações Propostas:
# - Todos os clientes do contrato mensal cancelam, sugerindo ofertas de desconto nos planos anuais e trimestrais.
# - Clientes que ligam mais de 4 vezes para o call center tendem a cancelar, recomendando um processo para resolver problemas em no máximo 3 ligações.
# - Clientes que atrasaram mais de 20 dias têm maior propensão ao cancelamento, indicando uma política para resolver atrasos em até 10 dias (equipe financeira).

tabela = tabela[tabela["duracao_contrato"]!="Monthly"]
tabela = tabela[tabela["ligacoes_callcenter"]<=4]
tabela = tabela[tabela["dias_atraso"]<=20]

display(tabela["cancelou"].value_counts())
display(tabela["cancelou"].value_counts(normalize=True).map("{:.1%}".format))
```

Neste projeto, utilizamos técnicas de análise de dados para entender os padrões de cancelamento dos clientes e propomos ações específicas para reduzir o número de cancelamentos e melhorar os resultados da empresa.
