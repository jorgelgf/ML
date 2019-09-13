# USO DE SVM PARA PREVISÃO DE UMA PESSOA EM PÉ OU SENTADO
 
## Introdução
<p align="justify">O grupo é composto por Jorge Luís e Severino Migue, alunos do curso de bacharelado em Ciências e Tecnologia da UFRN.
O presente relatório visa identificar se uma pessoa está em pé ou sentado por meio de um algoritmo.
Para que seja possível realizar esse processo, utilizamos uma base de dados coletada através de um vídeo no qual foi retirado alguns frames desse mesmo vídeo, após associamos o estado de uma pessoa em pé ou sentado.</p>
## Metodologia
<p align="justify">Utilizamos a linguagem de programação python para desenvolver os códigos e dentro dessa linguagem a ferramenta escolhida foi o Support Vector Machine, que trata-se de um algoritmo de aprendizagem de máquina que é utilizado principalmente em problemas que envolvem classificações. Fizemos os testes com 25% dos dados , restando 75% para treino. 
 
## Códigos<br>
 
### Trechos principais:
 
```py	
 
#Selecionando a base de dados
FILE_TO_DOWNLOAD =  "dataBase.csv"
DOWNLOAD_ROOT = "https://github.com/migueloten/relatorio_svm/raw/master/"
DATA_PATH = "csv/"
DATA_URL = DOWNLOAD_ROOT + DATA_PATH + FILE_TO_DOWNLOAD
 
def fetch_data(data_url="https://raw.githubusercontent.com/migueloten/relatorio_svm/master/csv/dataBase.csv", data_path="csv/", file_to_download="dataBase.csv"):
  if not os.path.isdir(data_path):
    os.makedirs(data_path)
  urllib.request.urlretrieve(data_url, data_path+file_to_download)
 
fetch_data()
 ```
 
 
```py
#Atributos escolhidos na base de dados
X = dataset.iloc[:,2:35].values
y = dataset.iloc[:,35].values
 ```
 
```py
#Manipulando os parâmetros do SVM (gamma e C)
#classifier = SVC(kernel = 'linear', random_state = 0)
classifier = Pipeline((
("scaler", StandardScaler()),
("svm_clf", SVC(kernel="rbf,", gamma=0.01, C=10))
))
 
```
 
```py
#Descobrindo a matriz de confusão
from sklearn.metrics import confusion_matrix
cm = confusion_matrix(y_test, y_pred)

print(cm)
``` 
 #### Link para código fonte:<br>
<a href="https://colab.research.google.com/drive/1rDdSCldgDo7eVW3qpJv2bLlNuAcICZ0I#scrollTo=_HE3vh8Hn7uS">Clique aqui</a> <br><br>
 
 
## Experimentos<br>
 
### Parâmetros manipulados:
 
* nose_x, nose_y:  Posição do nariz
* leftEye_x, leftEye_y	: Posição do olho<br>
* rightEye_x, rightEye_y: Posição do olho direito<br>
* leftEar_x, leftEar_y: Posição da orelha esquerda<br>
* rightEar_x, rightEar_y: Posição da orelha direita	<br>
* leftShoulder_x, leftShoulder_y: Posição do ombro esquerdo<br>
* rightShoulder_x, rightShoulder_y	: Posição do ombro direito<br>
* leftElbow_x, leftElbow_y: Posição do cotovelo esquerdo<br>
* rightElbow_x, rightElbow_y: Posição do cotovelo direito	<br>
* leftWrist_x, leftWrist_y: Posição do pulso esquerdo<br>
* rightWrist_x, rightWrist_y: Posição do pulso direito<br>
* leftHip_x, leftHip_y: Posição do quadril esquerdo<br>
* rightHip_x, rightHip_y: Posição do quadril direito<br>
* leftKnee_x, leftKnee_y: Posição do joelho esquerdo
* rightKnee_x, rightKnee_y: Posição do joelho direito
* leftAnkle_x, leftAnkle_y: Posição do tornozelo esquerdo
* rightAnkle_x, rightAnkle_y: Posição do tornozelo direito
 
<p align="justify">
 
</p>
 

