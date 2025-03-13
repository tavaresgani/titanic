# Titanic Data Analysis

Este repositório contém um conjunto de dados do Titanic e algumas análises realizadas sobre os dados, incluindo a taxa de sobrevivência por sexo, classe e grupo de idade. A seguir estão os detalhes de como os dados são processados e analisados.

## Bibliotecas Importadas

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```

Essas bibliotecas são utilizadas para manipulação de dados (pandas), visualização de gráficos (matplotlib e seaborn) e cálculos (numpy).

## Leitura do Arquivo

Os dados do Titanic são carregados a partir de um arquivo CSV:

```python
titanic = pd.read_csv('titanic.csv')
```

O conjunto de dados contém as seguintes colunas:

- `PassengerId`: ID do passageiro
- `Survived`: Indicador de sobrevivência (1 = Sobreviveu, 0 = Não Sobreviveu)
- `Pclass`: Classe do passageiro (1, 2, 3)
- `Name`: Nome do passageiro
- `Sex`: Sexo do passageiro
- `Age`: Idade do passageiro
- `SibSp`: Número de irmãos/cônjuges a bordo
- `Parch`: Número de pais/filhos a bordo
- `Ticket`: Número do bilhete
- `Fare`: Preço do bilhete
- `Cabin`: Número do camarote
- `Embarked`: Porto de embarque (C = Cherbourg, Q = Queenstown, S = Southampton)

## Análise de Sobrevivência

### Probabilidade de Sobrevivência por Sexo

Calculamos a taxa de sobrevivência por sexo, multiplicando a média por 100 para obter a porcentagem:

```python
titanic[['Sex', 'Survived']].groupby(['Sex']).mean() * 100
```

Resultados:
- **Mulheres**: 74.20% de chance de sobrevivência
- **Homens**: 18.89% de chance de sobrevivência

### Probabilidade de Sobrevivência por Classe

Calculamos a taxa de sobrevivência de acordo com a classe do passageiro:

```python
titanic[['Pclass', 'Survived']].groupby(['Pclass']).mean() * 100
```

Resultados:
- **Classe 1**: 62.96% de chance de sobrevivência
- **Classe 2**: 47.28% de chance de sobrevivência
- **Classe 3**: 24.24% de chance de sobrevivência

### Gráficos

Geramos dois gráficos para ilustrar as taxas de sobrevivência por sexo e por classe:

```python
fig, (axis1, axis2) = plt.subplots(1,2, figsize=(12,4))
sns.barplot(x='Sex', y='Survived', data=titanic, ax=axis1)
sns.barplot(x='Pclass', y='Survived', data=titanic, ax=axis2)

# Adicionando títulos aos eixos
axis1.set_title('Taxa de sobrevivência por gênero')
axis2.set_title('Taxa de sobrevivência por classe')
```

### Influência da Idade na Taxa de Sobrevivência

Para analisar a influência da idade na taxa de sobrevivência, criamos intervalos de idade e calculamos a taxa média de sobrevivência por grupo de idade:

```python
bins = [0, 10, 20, 30, 40, 50, 60, 70, 80]
titanic['AgeGroup'] = pd.cut(titanic['Age'], bins)
age_survival = titanic.groupby('AgeGroup')['Survived'].mean()
```

Em seguida, geramos um gráfico de barras para visualizar as taxas de sobrevivência por grupo de idade:

```python
plt.figure(figsize=(10, 6))
age_survival.plot(kind='bar', color='skyblue')

# Adicionando título e rótulos aos eixos
plt.title('Taxa de Sobrevivência por Grupo de Idade')
plt.xlabel('Grupo de Idade')
plt.ylabel('Taxa de Sobrevivência')
```

## Requisitos

Certifique-se de ter as bibliotecas necessárias instaladas para rodar este código:

```bash
pip install pandas numpy matplotlib seaborn
```

## Conclusões

Este conjunto de dados fornece informações valiosas sobre os fatores que influenciaram a taxa de sobrevivência no Titanic, como o sexo, a classe social e a idade dos passageiros.
