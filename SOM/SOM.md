# SOM - Self-Organizing Map
### Jorge Luís Gurgel Fernandes
 
## Introdução
<p align="justify">
O presente relatório visa identificar a possibilidade de aprovação ou reprovação da disciplina de LOP por meio de um banco de dados contendo
informações de atividades submetidas. Para isso, foi utilizado a linguagem de programação python para desenvolver os códigos e dentro dessa linguagem a ferramenta escolhida foi uma Rede Neural de aprendizado não supervisionado (SOM).
 
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
som = MiniSom(x = tamanhoXdaRede, y = tamanhoYdaRede, input_len = 20, sigma = 1.0, learning_rate = 0.3)
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
[[ 26.  31.  28.  16.  48.]
 [ 28.  21.  23.  27.  26.]
 [ 32.  19.  12.  62.  63.]
 [ 13.  23.  37.  51. 219.]
 [ 33.  26.  28.  33.  23.]]
Aprovados
[[24. 30. 26. 15. 38.]
 [25. 20. 21. 20. 17.]
 [31. 19.  8. 47. 45.]
 [13. 21. 24. 18. 61.]
 [31. 21. 20. 26. 18.]]
```
<br>Gráfico de pizza obtido atráves dos dados (Azul aprovados, LARANJA reprovados)

![Gráfico](https://github.com/jorgelgf/ML/blob/master/SOM/img/download.png)
 
 #### Link para código fonte:<br>
<a href="https://colab.research.google.com/drive/1ROlZfxLZprMUYUhli91bPciYnXAnV9u6#scrollTo=aRQLCTZKDhFo">Clique aqui</a> <br><br>
 
 
## Conclusão<br>

<p align="justify">
 Após a utilização do código pode-se verificar que existe ao menos dois grupos com probabilidade de 100% de aprovação assim como também alguns grupos em que possuem uma probabilidade acima dos 50% de reprovação. Com essas informações em mãos é possível efetuar ações com a finalidade de reverter a situação dos alunos com risco de reprovação.
 
</p>
 ## Referências<br>
 https://medium.com/neuronio-br/descobrindo-som-uma-rede-neural-com-aprendizado-não-supervisionado-f22bc1e55eca	


