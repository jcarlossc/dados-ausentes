# Inconsistência - Dados Ausentes
Estudo sobre dados ausentes.

## Dados ausentes
## ✅ Valores NaN ou None
* ```df.isnull().sum()```. Conta quantos NaN por coluna.
* ```df.dropna()```. Remove todas as linhas com NaN.
* ```df.dropna(subset=['coluna1', 'coluna2'])```. Remove linhas com NaN só nessas colunas.
* ```df.dropna(axis=1)```. Remove colunas inteiras que têm NaN.
* ```df.fillna(0)```. Preenche todos os NaN com 0.
* ```df['coluna'].fillna('Desconhecido', inplace=True)```. Preenche apenas uma coluna com texto.
* ```df['idade'].fillna(df['idade'].mean(), inplace=True)```. Preenche NaN com a média.
* ```df.fillna(method='ffill')```. Forward fill → preenche com o valor anterior.
* ```df.fillna(method='bfill')```. Backward fill → preenche com o valor seguinte.
* ```df['temperatura'].interpolate(method='linear', inplace=True)```. Se você está lidando com números (ex: dados de sensores), pode interpolar.
## ✅ Strings vazias "" ou espaços em branco " "
* ```df['coluna'].apply(lambda x: x.strip() == '')```. True se for vazio ou só espaços.
* ```(df['coluna'].str.strip() == '').sum()```. Contar quantos casos assim existem.
* ```import numpy as np df['coluna'] = df['coluna'].replace(r'^\s*$', np.nan, regex=True)```. Substituir por NaN (para tratar como valor faltante).
* ```df['coluna'] = df['coluna'].str.strip()```. Remover espaços extras ao redor.
* ```df = df.dropna(subset=['coluna'])```. Remover essas linhas.
## ✅ Placeholder errado: 'na', 'N/A', '999', -1, etc. usados como se fossem valores
* ```df = pd.read_csv('dados.csv', na_values=['na', 'n/a', 'N/A', 'NULL', -1, 999, 0])```.  Ler o CSV já marcando eles como NaN.
* ```import numpy as np df['coluna'] = df['coluna'].replace(['na', 'n/a', 'N/A', 'NULL', -1, 999], np.nan)```. Substituir manualmente após carregar. Para colunas específicas.
* ```df.replace(['na', 'n/a', 'N/A', 'NULL', -1, 999], np.nan, inplace=True)```. Substituir manualmente após carregar. Para todo o dataframe.
* ```df.dropna(subset=['coluna'])```. Remover linha.
* ```df['coluna'].fillna(média_ou_valor)```. Preencher com valor.
## ✅ Colunas com muitos valores ausentes
* ```percent_missing = df.isnull().mean() * 100```. Calcular a porcentagem de valores ausentes por coluna.
* ```high_missing = percent_missing[percent_missing > 50]```. Colunas que têm mais de 50% ausentes.
* ```df = df.drop(columns=['nome_da_coluna'])```. Se a coluna é irrelevante ou muito vazia (ex: > 70-80% ausente) → provavelmente pode ser removida.
* ```df['coluna'].fillna('Desconhecido', inplace=True)```.  Se a coluna é importante, mas incompleta → tente preencher os valores ausentes: Com valor fixo (ex: 'Desconhecido', 0).
* ```df['coluna'].fillna(df['coluna'].mean(), inplace=True)```. Ou, tente preencher com estatística (média, mediana, moda).
* ```limiar = 0.7  colunas_para_remover = percent_missing[percent_missing > (limiar * 100)].index  df = df.drop(columns=colunas_para_remover)```. Automatizar a limpeza.
## ✅ Linhas inteiras vazias
* ```linhas_vazias = df.isnull().all(axis=1).sum()```. Antes de limpar, você pode ver quantas linhas serão afetadas.
* ```df = df.replace(r'^\s*$', np.nan, regex=True)```. Padronizar strings vazias como NaN.
* ```df = df.dropna(how='all')```. Remover linhas 100% vazias.
* ```limiar = 0.8  df = df[df.isnull().mean(axis=1) < limiar]```. Remover linhas onde 80% das colunas estão vazias.
