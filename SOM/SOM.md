# SOM - Self-Organizing Map
### Jorge Luís Gurgel Fernandes
 
## Introdução
<p align="justify">
O presente relatório visa identificar a possibilidade de aprovação ou reprovação da disciplina de LOP por meio de um banco de dados contendo
informações de atividades submetidas.<p align="justify">Para isso, foi utilizado a linguagem de programação python para desenvolver os códigos e dentro dessa linguagem a ferramenta escolhida foi uma Rede Neural de aprendizado não supervisionado (SOM).
 
## Metodologia<br> 
<p align="justify">
 A rede SOM é bastante utilizada quando se tem dataset com muitos atributos, podendo ter uma saída com um número menor de dimensões.
 Essas saídas são denominadas de map (ou feauture map).<br>
Essa rede possuí um sistema que é baseado em aprendizagem competitiva. Os neurônios competem na busca de responder (quem será ativado) através de um conjunto de entradas, o neurônio vencedor será chamado de winner.
 
## Primeira etapa: Coleta dos dados
A base de dados foi obtida da turma de Lógica de Programação da Escola de Ciência e Tecnologias da UFRN (2017.1 até 2019.1).
O banco de dados contém atividades submetidas ao longo de 21 semanas.
<br>
## Códigos<br>
 
### Trechos principais:
Trecho em que foi inserida as devidas bibliotecas e base de dados manipulada:
<br>
```py	

import pandas as pd
import numpy as np
dataSet =  pd.read_csv("https://raw.githubusercontent.com/ect-info/ml/master/dados/lop_submissao_semana.csv",index_col=False )
dataSet.head()
```

Para o manuseio do código da rede SOM, foi manipulado o trecho do código abaixo com a finalidade de mudar o status da situação do aluno, mudança de uma string para um inteiro.
<br>0 - APROVADO
<br>1 - APROVADO POR NOTA
<br>2 - REPROVADO
<br>3 - REPROVADO POR NOTA
<br>4 - REPROVADO POR NOTA E FALTA
<br>
```py	
dataSet['situacao'] = pd.Categorical(dataSet['situacao'])
dataSet['situacao'] = dataSet['situacao'].cat.codes
```

Trecho do código em que é selecionado todas as colunas do banco de dados que contém as submissões das atividades (X_train),
assim como a situação final do aluno (target_train).<br>
 
```py
X_train = dataSet.iloc[:, 2:22].values 
target_train = dataSet.iloc[:,25].values

```
Código abaixo contendo as configurações de treinamento da rede.

```py
# Training the SOM
tamanhoXdaRede =5; 
tamanhoYdaRede = 5; 
quantidadeCaracteristicas = col
from minisom import MiniSom
som = MiniSom(x = tamanhoXdaRede, y = tamanhoYdaRede, input_len = 20, sigma = 1.0, learning_rate = 0.5)
som.pca_weights_init(X_train)

```
<br>Montando matriz de aprovados e reprovados pós treinamento, código abaixo.
<br>
```py
# encontra o vencedor 
x = X_train[1,:]
pos = som.winner(x)
# matriz de zeros para contador de aprovados 
MContAp = np.zeros((tamanhoXdaRede,tamanhoYdaRede))
# matriz de zeros para o contador de reprovados 
MContT = np.zeros((tamanhoXdaRede,tamanhoYdaRede))
cont = 0; 
for x in X_train: 
  pos = som.winner(x)
  if (Y_train[cont] >= 1): #Aprovado 
    MContAp[pos] += 1
  MContT[pos] += 1
  cont= cont+1
```
<br>Impressão da matriz abaixo.
```py
print("Total:")
print(MContT)

print("Aprovados")
print(MContAp)
```

<br>Matriz gerada abaixo.

```py
Total:
[[ 36.  28.  67. 226.  64.]
 [ 19.  30.  46.  66.  21.]
 [ 25.  32.  20.  30.  26.]
 [ 22.  14.  13.  22.  29.]
 [ 18.  12.  18.  27.  37.]]
Aprovados
[[ 16.  15.  38. 198.  52.]
 [  7.  16.  28.  42.  12.]
 [  8.  14.   8.  10.  12.]
 [ 11.   2.   6.   6.  13.]
 [  7.   2.   3.   2.  11.]]
```
<br>Gráfico de pizza obtido atráves dos dados

![Alt Text](https://github.com/{user}/{repo}/raw/{branch}/path/to/image.gif)
 
 #### Link para código fonte:<br>
<a href="https://colab.research.google.com/drive/1rDdSCldgDo7eVW3qpJv2bLlNuAcICZ0I#scrollTo=_HE3vh8Hn7uS">Clique aqui</a> <br><br>
 
 
## Experimentos<br>

<p align="justify">
 
</p>
 

