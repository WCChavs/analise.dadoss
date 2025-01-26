# analise.dadoss

# README - Análise de Cancelamentos de Clientes

Este repositório contém um projeto de análise de dados desenvolvido durante um curso intensivo, focado em entender os cancelamentos de clientes. O código visa explorar como diferentes variáveis impactam nas decisões de cancelamento e fornecer insights que podem ser usados para otimizar processos de retenção de clientes.

## Objetivo

O objetivo deste projeto é realizar uma análise detalhada sobre os cancelamentos, explorando como variáveis como duração do contrato, número de ligações ao call center e atrasos no pagamento influenciam o comportamento de cancelamento dos clientes. Ao final da análise, esperamos extrair informações valiosas para ajudar a reduzir a taxa de cancelamento e melhorar a experiência do cliente.

## Estrutura do Código

### Passo 1: Importação da Base de Dados

O código começa com a importação da base de dados, que está armazenada em um arquivo CSV denominado `cancelamentos_sample.csv`. O pandas é utilizado para carregar o arquivo CSV em um DataFrame.

```python
import pandas as pd
tabela = pd.read_csv("cancelamentos_sample.csv")
```

### Passo 2: Visualização da Base de Dados

Após carregar os dados, a coluna `CustomerID`, que não é relevante para a análise, é removida. A base de dados é então exibida para uma análise preliminar.

```python
tabela = tabela.drop(columns="CustomerID")
display(tabela)
```

### Passo 3: Limpeza de Dados

O código realiza a limpeza de dados, verificando e removendo linhas com valores ausentes (`NaN`). Essa etapa é importante para garantir que as análises subsequentes não sejam comprometidas por dados faltantes.

```python
display(tabela.info())  # Exibe informações sobre o DataFrame
tabela = tabela.dropna()  # Remove linhas com valores ausentes
display(tabela.info())  # Exibe novamente para verificar a remoção
```

### Passo 4: Análise Inicial dos Cancelamentos

A análise inicial dos cancelamentos é feita para entender a distribuição dos clientes que cancelaram versus os que não cancelaram. O código exibe o número de cancelamentos e a porcentagem de clientes que cancelaram.

```python
display(tabela["cancelou"].value_counts())  # Contagem de cancelamentos
display(tabela["cancelou"].value_counts(normalize=True))  # Percentual de cancelamentos
```

### Passo 5: Análise das Causas dos Cancelamentos

A análise mais profunda envolve entender como as variáveis influenciam as taxas de cancelamento. O código cria gráficos para cada coluna da base de dados, comparando a distribuição dos dados entre clientes que cancelaram e os que não cancelaram. Para isso, a biblioteca `plotly` é utilizada para criar visualizações interativas.

```python
import plotly.express as px

for coluna in tabela.columns:
    grafico = px.histogram(tabela, x=coluna, color="cancelou")
    grafico.show()
```

Esses gráficos ajudam a identificar padrões e possíveis causas de cancelamento, como:

- **Clientes com contratos mensais**: Todos os clientes com contratos mensais cancelaram, sugerindo a necessidade de promover planos anuais e trimestrais.
- **Número de ligações ao call center**: Clientes que ligam mais de 4 vezes para o call center tendem a cancelar. Isso sugere que uma ação corretiva deve ser tomada para resolver os problemas dos clientes rapidamente.
- **Atrasos nos pagamentos**: Clientes que atrasaram o pagamento por mais de 20 dias têm uma taxa de cancelamento maior. A recomendação é implementar uma política de resolução de atrasos em até 10 dias.

### Passo 6: Filtragem dos Dados para Análise

Com base nas observações feitas, o código filtra os dados para manter apenas os clientes que não possuem contrato mensal, realizaram até 4 ligações para o call center e têm atrasos de no máximo 20 dias.

```python
tabela = tabela[tabela["duracao_contrato"]!="Monthly"]
tabela = tabela[tabela["ligacoes_callcenter"]<=4]
tabela = tabela[tabela["dias_atraso"]<=20]
```

Após a filtragem, é realizada uma nova análise para verificar a distribuição dos cancelamentos no conjunto de dados filtrado.

```python
display(tabela["cancelou"].value_counts())  # Contagem de cancelamentos no novo conjunto
display(tabela["cancelou"].value_counts(normalize=True))  # Percentual de cancelamentos
```

## Pacotes Necessários

Para rodar este código, você precisará instalar as dependências abaixo. Você pode instalar todos os pacotes necessários utilizando o comando `pip install`:

```bash
!pip install pandas numpy openpyxl nbformat ipykernel plotly
```

Esses pacotes são usados para manipulação de dados, visualização de gráficos e execução do código em um ambiente Jupyter Notebook.

## Como Executar o Projeto

1. Clone o repositório ou baixe os arquivos necessários.
2. Certifique-se de que o arquivo `cancelamentos_sample.csv` esteja disponível no diretório de trabalho.
3. Instale as dependências necessárias utilizando o comando acima.
4. Execute o código em um ambiente de sua preferência, como Jupyter Notebook ou Google Colab.
5. Acompanhe a análise e os gráficos gerados, fazendo ajustes conforme necessário.

## Conclusão

Este código oferece uma análise detalhada dos cancelamentos de clientes, permitindo identificar padrões e causas que podem ser tratadas para melhorar a retenção. As informações extraídas a partir das variáveis analisadas são valiosas para aprimorar políticas de atendimento, planos de contrato e resolução de problemas. A partir dessa análise, empresas podem tomar decisões mais informadas e focadas em reduzir cancelamentos.

Se tiver sugestões ou dúvidas, sinta-se à vontade para contribuir ou fazer perguntas!

---

