
---
import pandas as pd

### Leitura

pd.DataFrame()            = Cria um DataFrame.
pd.Series()               = Cria uma Series (vetor unidimensional).
pd.read_csv()             = Lê um arquivo CSV.
pd.read_excel()           = Lê um arquivo Excel.
pd.read_json()            = Lê um arquivo JSON.
pd.read_html()            = Lê tabelas de uma página HTML.

---
### Conversão  

df.to_csv()               = Transforma um DataFrame em CSV.
df.to_excel()             = Transforma um DataFrame em excel.
df.to_csv()               = Transforma um DataFrame em json.
df.to_json()              = Transforma um DataFrame em json.
df.to_html()              = Transforma um DataFrame em html.

----
### Exibição

df.head([n])              – Exibe as primeiras [n] linhas.
df.tail([n])              – Exibe as últimas [n] linhas.
df.shape                  – Exibe o número de linhas e colunas (dimensão) do dataframe.
df.info()                 – Exibe um resumo das colunas e tipos.
df.describe()             – Exibe estatísticas de colunas numéricas (média, desvio etc.).
df.columns                – Exibe o nome das colunas.
df.index                  – Exibe o índice do DataFrame.
df.dtypes                 – Exibe os tipos de dados de cada coluna.
df.memory_usage()         – Exibe a memória ocupada por cada coluna.
df.nunique()              – Conta o número de valores únicos para cada coluna.

---------
### Manipulação e Transformação de Dados

df.rename(columns={ 'old' : 'new' })           = Renomeia colunas ou índices.
df['colunm'].astype([type])                    = Converte o tipo de uma coluna.
df.replace({['A': 'abc'], ['A': 'ABC']})       = Substitui valores existentes por outros.
df.drop(['colunm'])                            = Remove linhas ou colunas especificadas.
df.drop([n])                                   = Remove a linha com índice [n].
df.drop_duplicates()                           = Remove linhas duplicadas.
df.duplicated()                                = Retorna um booleano para cada linha duplicada.
df.fillna([n])                                 = Preenche valores nulos com um valor [n].
df.isna()                                      = Verifica se há valores nulos.
df.notna()                                     = Retorna True para valores não nulos.
df.dropna()                                    = Remove linhas/colunas com valores nulos.

----------
### Seleção e Filtragem de Dados

df['column']                      = Seleciona uma coluna específica do DataFrame.
df['x', 'y']                      = Seleciona múltiplas colunas.
df.iloc[x]                        = Seleção baseada na posição das linhas.
df.iloc[0:2, 1:3]                 = Seleção baseada na posição das linhas e colunas.
df.loc[df['Nome'] == 'x']         = Seleciona as linhas onde a coluna é igual a [x].
df.query(['x > y'])               = Seleciona as linhas com base na expressão.
df[df['Idade'] > 25]              = Filtra usando condições booleanas.
df.get('Nome', pd.Series())       = Recupera uma coluna, com valor padrão se não existir.
df.where(df['Idade'] > 25, 0)     = Substitui onde a condição é falsa.
df.mask(df['Idade'] > 25, 0)      = Substitui onde a condição é verdadeira.

-------------
### Ordenação e Reindexação

df.sort_values(by=['Idade'])   = Ordena com base no(s) valor(es) de coluna(s).
df.sort_index()                = Ordena com base no índice.
df.reset_index(drop=False)     = Reseta o índice, transformando o índice atual em coluna.
df.reset_index(drop=True)      = Reseta o índice.
df.sample([n])                 = Retorna uma amostra aleatória de [n] linhas.

---------
### Estatísticas e Agregações

df['Idade'].sum()          = Soma os valores da coluna.
df['Idade'].mean()         = Calcula a média da coluna.
df['Idade'].median()       = Calcula a mediana dos valores da coluna.
df['Idade'].std()          = Calcula o desvio padrão da coluna.
df['Idade'].var()          = Calcula a variância da coluna.
df['Idade'].min()          = Retornam o valor mínimo da coluna.
df['Idade'].max()          = Retornam o valor máximo da coluna.
df['Idade'].count()        = Conta elementos não nulos da coluna.
df['Idade'].mode()         = Retorna o(s) valor(es) que mais se repetem da coluna.

-------
### Junção de Dados

pd.concat([df1, df2])      = Concatena DataFrames

----------

### Manipulação de Strings

df['Nome'].str.lower()     = Converte todas as letras  para minúsculas.
df['Nome'].str.upper()     = Converte todas as letras  para maiúsculas.
df['Nome'].str.strip()     = Remove espaços em branco no início e fim.