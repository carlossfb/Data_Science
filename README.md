
# Data Science

Aqui iremos introduzir o Python como forma de manipular conjunto de dados, juntamente de bibliotecas úteis.

Os códigos aqui são testados no ambiente de desenvolvimento provido pelo Colab

#### Importando a biblioteca PANDAS com o nome PD para uso facilitado

```bash
  import pandas as pd
```

#### Utilizando a biblioteca para leitura dos dados de um arquivo CSV

Primeiro de tudo, importar o DATASET, nossa base de dados e colocar dentro de uma variável.

```http
  df = pd.read_csv("caminho_do_arquivo", error_bad_lines=false, sep=";")
```

A variável se chama DF abreviando DATAFRAME, que nada mais é que uma representação de dados em formato de tabela, o PATH do arquivo lido no exemplo era de um DRIVE, possivel graças a conexão do colab com a nuvem (que pode ser feita sem muitas dificuldades), o parâmentro de ERROR_BAD_LINES serve para o arquivo ler ignorando a princípio possiveis erros em alguma linha, desnecessário quando descobrimos que o separados do CSV ao invés de usar VIRGULA estava com PONTO E VIRGULA, que era o que estava causando um erro, por isso foi usado o SEP. 

##### Leitura de vários arquivos

Só repetir o processo acima, e para juntar esses DATAFRAMES usamos:
```http
  df = pd.concat([df1,df2,df3])
```
Eles ficarão um abaixo do outro.

##### Pegar amostra dos dados

Só repetir o processo acima, e para juntar esses DATAFRAMES usamos:
```http
  df.sample(5)
```

#### Lendo as 5 pimeiras linhas

Você dentro dos parênteses pode colocar o numero de linhas que quer também.

```http
  df.head()
```
#### Renomeando as colunas

Indicando COLUMNS e depois dentro de chaves podemos mostrar os equivalentes para cada coluna.
**O DF = DF...**, vai servir para sobrescrever o dataframe que teriamos antes pelo novo, com as mudanças.

```http
  df = df.rename(columns={"country":"Pais","continent":"Continente"})
```
#### Número de linhas e colunas

```http
  df.shape
```

#### Nome das colunas

```http
  df.columns
```
#### Tipos de cada coluna

```http
  df.dtypes
```
#### Modificar tipo de dado de uma coluna para object

```http
  df["NomeColuna"] = df["NomeColuna"].astype("object")
```
#### Monstar as ultimas linhas

```http
  df.tail()
```

Podemos especificar o numero de linhas colocando um numero dentro dos parênteses.

#### Retorna informações estatísticas do conjunto de dados

```http
  df.describe()
```
#### Retorna um array com apenas os valores que não se repetem na coluna CONTINENTE

```http
df["Continente"].unique()
```

#### Retorna apenas os dados cuja coluna CONTINENTE é igual a Oceania.
Utilizamos aqui o LOC para criar esses pequenos filtros e o HEAD para mostrar as 5 primeiras linhas

```http
  Oceania = df.loc[df["Continente"] == "Oceania"]
  Oceania.head()
```
#### Retorna a quantidade de Países para cada continente

```http
  df.groupby("Continente")["Pais"].nunique()
```
### Exercício

Para cada ano da nossa base de dados, qual a expectativa de vida média?

```http
  df.groupby("Ano")["Expectativa de vida"].mean()
```
#### Retorna a quantidade de campos nulos

```http
  df.isnull().sum()
```
#### Substituir campos nulos da coluna por média de valores daqueles dados

Usaremos de exemplo uma tabela comercial onde algumas vendas estão sem registro:

```http
  df["Vendas"].fillna(df["Vendas"].mean(), inplace=true)
```
O inplace é importante pra persistir essa alteração

#### Substituir campos nulos da coluna por zero

```http
  df["Vendas"].fillna(0, inplace=True)
```
O inplace é importante pra persistir essa alteração

#### Apagar as linhas com registros nulos

```http
  df.dropna[inplace=True]
```
O inplace é importante pra persistir essa alteração

#### Apagar as linhas com registros nulos em uma coluna específica

```http
  df.dropna[subset=["Vemdas"], inplace=True]
```
O inplace é importante pra persistir essa alteração

#### Apagar as linhas com registros nulos em todas colunas

```http
  df.dropna[how="all", inplace=True]
```
O inplace é importante pra persistir essa alteração

#### Criando uma nova coluna

Criaremos a coluna total que é igual o preço multiplicado pela quantidade de vendas.

```http
  df["Total"] = df["ValorUnitario"].mul(df["QTD"])
  ```
#### Trazendo os 3 maiores totais de venda

```http
  df.nlargest(3, "Total")
  ```
#### Trazendo os 3 menores totais de venda

```http
  df.nsmallest(3, "Total")
  ```
#### Trazendo a soma das vendas por cidade

```http
  df.groupby("Cidade")["Total"].sum()
  ```
#### Ordenando o conjunto de dados

```http
  df.sort_values("Total", ascending=false).head(10)
  ```

### Trabalhando com DATAS 

#### Transformando em data

```http
  df["Data"] = pd.to_datetime(df["Data"])
```
