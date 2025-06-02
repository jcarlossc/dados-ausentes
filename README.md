# Inconsistência - Dados Ausentes
Estudo sobre dados ausentes.

# Dados ausentes
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

## ✅ Colunas com muitos valores ausentes

## ✅ Linhas inteiras vazias
