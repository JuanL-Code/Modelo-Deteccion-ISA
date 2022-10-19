# Modelo-Deteccion-ISA

# Introduccion
ISA ITCO es una filial que se encarga del negocio de la transmision de energia esto implica un control de sus activos fisicos y de sus indicadores para asegurar que la calidad del servicio cumpla con los requerimientos establecidos por la ley (CREG).
Uno de los tantos activos implicados en el proceso de transmision son los aisladores electricos los cuales hacen parte de las líneas eléctricas de alta tensión y son los elementos que cumplen la función de sujetar mecánicamente a los conductores que forman parte de la línea, manteniéndolos aislados de tierra y de otros conductores.
Dada su funcionalidad y tipo de usos estos se encuentran a la interperie y es por ello que con el tiempo cumplen con su vida util, algunas posibles fallas en estos pueden ser la corrosion, engrietamiento o entiezamiento, entre otros, a estos se les llama "modos de falla".
Actualmente se tienen documentados en las bases de datos 13 posibles modos de falla los cuales varian en base al tipo de material y a la gravedad del mismo.
Para asegurar el correcto funcionamiento de las lineas de transmision se debe hacer un control continuo de estos activos vitales para el funcionamiento del mismo, actualmente estas revisiones se hacen de manera manual lo cual implica que un tecnico se dirija a sitio exacto, haga un analisis de la falla y lo documente.
Es por ello que dentro de ISA se lleva desde hace meses un estudio y proceso para el desarrollo de modelos de inteligencia artificial que permitan a cualquier individuo saber automaticamente que modo de falla se encuentra en base a un previo entrenamiento.

# Proceso a mejorar
Se busca entonces hacer una guia que permita a cualquier usuario crear un modelo de inteligencia artificial en nube para detectar lo que el usuario desee

# Indicaciones
El algoritmo de deteccion y reconocimiento corre en un framework llamado YOLO el cual funciona por medio de una ingesta de imagenes y un entrenamiento previo en nube sin la necesidad de usar recursos propios como CPU o GPU

# Funcionamiento
1. Para la creacion de un modelo de IA enfocado a un modo de falla o cualquier otro uso se comienza haciendo una recoleccion minima de unas 100 images(Ej: Si se desea un modelo de IA que detecte y reconozca piezas corroidas debemos recolectar 100 imagenes minimo de este modo de falla)![evidencias 1](https://user-images.githubusercontent.com/68828858/196544265-79db9f5d-6b46-4c89-9cd0-43f9718eb1eb.PNG)

2. Estas imagenes se exportaran a un software basado en python llamado "LabelIMG" en el cual se hace una seleccion de la zona que corresponde a la indicada y se le da un nombre de clase, lo que hace LabelIMG es guardar un archivo .txt el cual guarda las posiciones cartesianas dentro de esa imagen de tal manera que hace una correlacion entre la imagen y este archivo txt. 
![evidencia 3](https://user-images.githubusercontent.com/68828858/196544469-35d10ad4-8001-4196-b3bc-b644e605f649.PNG)

3. Despues de hacer la creacion de los recuadros dentro de LabelIMG nos quedara una carpeta en la cual estaran todas. Cada imagen genera un archivo txt dentro del cual se ubica por cada recuadro un par organizado de coordenadas. En el ejemplo pasado mostrabamos dentro de labelIMG como etiquetabamos dentro de la imagen #145, el resultado sera entonces un txt homonimo con los 5 taggeos correspondientes, el numero cero al inicio de cada coordenada hace refentencia a la clase a la cual corresponde ese taggeo, en caso de tener dentro de un mismo modelo mas de una clase este numero se modificara(Ej. Si dentro de un modelo queremos identificar piezas corroidas y egrietadas).![evidencia 2](https://user-images.githubusercontent.com/68828858/196545354-c832cd60-ad4d-4021-ab23-0f9037a4bc59.PNG)

4. Una vez finalizado estos procedimientos, haremos de la carpeta un .zip el cual utilizaremos dentro de Google Colab para hacer un entrenamiento y uso en nube, este .zip ya pasara entonces por unos pasos de codificacion que se explican a mas detalle en la seccion de procedimiento para entonces proceder con las descompresion del archivo y la posterior puesta en marcha del modelo en nube.

![evidencias 4](https://user-images.githubusercontent.com/68828858/196546488-db3e6c71-ebf8-4dda-89c3-57d03904d99f.PNG)

5. Una vez hacemos el procedimiento de entrenamiento en nube cargamos una imagen de prueba, la imprimimos y nos lanza el resultado final
![evidencia  5](https://user-images.githubusercontent.com/68828858/196548210-86d0cba5-5aa4-4ef1-963b-c551de400e91.PNG)
![evidencia 6](https://user-images.githubusercontent.com/68828858/196548216-52d0444b-7920-4f16-a263-badaf6051349.PNG)

# Paso a Paso
## 1. Instalamos el software 

```

$ git clone https://github.com/tzutalin/labelImg
$ conda install pyqt=5
$ conda install -c anaconda lxml
$ cd labelImg
$ pyrcc5 -o libs/resources.py resources.qrc
$ python labelImg.py

```
Al correr la ultima linea nos abrira el software de etiquetado 
## 2. Estructura carpetas
Dentro de la carpeta clonada crearemos la siguiente estructura de carpetas

```

--train_data
  -- images
      --train
      --val
  -- labels
      --train
      --val
      
```

Una vez hecha la creacion de las carpetas, guardaremos en train_data/images/train las imagenes que deseamos etiquetar en formato jpg o jpeg y copiamos las imagenes tambien en train_data/images/val. 
Dentro de LabelImg en la barra izquierda seleccionaremos "Open Dir" y abriremos la carpeta  train_data/images/train y en la opcion de "Change save dir" seleccionaremos train_data/labels/train para guardar todos los archivos txt de las etiquetas.
Adiconal en la barra superior seleccionaremos el menu de view y daremos click a la opcion de "Auto Save mode"

De esta manera entonces nos quedaran cargadas todas la imagenes y tambien la ruta de guardado automatico de los taggeos que hagamos 

![evidencia 9](https://user-images.githubusercontent.com/68828858/196728660-33165ee9-c86a-44bc-9249-7325e1aecab2.PNG)


# 3. Taggeo

Para taggear cada imagen usamos las siguientes teclas: con w hacemos el uso del cuadro para seleccionar la zona que deseamos etiquetar, le damos un nombre a la etiqueta y despues al boton de next para continuar con la siguiente imagen, asi hasta complementarlas todas

![evidencia 10](https://user-images.githubusercontent.com/68828858/196740017-8ff14419-eb83-4434-a4be-8fc089149f20.PNG)


# 4. Preparacion de los archivos

Una vez listo el proceso de taggeo nos quedara en la carpeta train_data/labels/train todos los archivos txt los cuales copiaremos a la carpeta train_data/labels/val

Ahora, la carpeta train_data la comprimiremos para ser usada dentro de google colab

# 5. Google Colab

Crearemos una cuenta de Google colab y copiaremos el siguiente notebook [Notebook](https://colab.research.google.com/drive/1NR6DdW_B0pYFanj4TB9emuKE3XI-T311?usp=sharing) como copia en nuestro drive dando en el menu de arhivo/guardar una copia en drive

## 5.1 Como correr el notebook
1. Primero daremos click en run setup para cargar e instalar el framework dentro de nuestro entorno virtual

![evidencia 11](https://user-images.githubusercontent.com/68828858/196731777-6fda6403-76ce-46fa-8fea-8f8978b26440.PNG)

## 5.2 Cargar los datos
Primero subiremos a google colab el .zip "train_data", una vez cargado correremos la linea de cargar los datos

```

!unzip -q ../train_data.zip -d ../

```

## 5.3 Creamos un archivo de configuracion
En Visual Studio/Sublime/Notepad++/Bloc de notas creamos un archivo de configuracion con el siguiente codigo

```
path: ../train_data  # dataset root dir
train: ../train_data/images/train/  # train images (relative to 'path') 128 images
val: ../train_data/images/val/  # val images (relative to 'path') 128 images
test:  # test images (optional)

# Classes
nc: 1  # number of classes
names: ['Aislador']  # class names

```

Este archivo cambia en base a las necesidades y usos que le den al modelo, en este caso los parametros a cambiar seria el numero de clases y el nombre de las mismas
Estes archivo lo guardamos como "customdata.yaml" y debe ser de formato en texto plano y lo subiremos dentro de google colab en la carpeta yolov5/data

## 5.4 Entrenamiento
Corremos la linea de entrenamiento, en este caso use un modelo de 163 imagenes y lo entrene durante 20 ciclos, tardo 1 hora, se puede hacer pruebas en base a cada caso, lo importante es estar por encima de un numero de ciclos para conseguir un entrenamiento bueno pero tampoco superar determinado nivel por uso de tiempo y recursos y adicional evitando un overfitting del modelo.

```

!python train.py --img 640 --batch 4 --epochs 20 --data customdata.yaml --weights yolov5s.pt --cache

```

## 5.6 Verificacion

Una vez finalizado el entrenamiento subiremos a google colab una imagen de prueba llamada test.jpg, al estar cargadas corremos las siguientes lineas 

```

-!python detect.py --weights runs/train/exp/weights/last.pt --img 640 --conf 0.25 --source "../test.jpg"
display.Image(filename='../test.jpg', width=600)

```

Estamos cargando la ruta del modelo entrenado y de la imagen de test, una vez finalizado iremos a yolov5/runs/detect/exp/test.jpg
Ese sera el resultado, podemos hacer diferentes test solo debemos modificar el parametro donde --source "../test(X).jpg y dado que soo carga el modelo una vez no se requiere hacer un entrenamiento nuevo


![evidencia 7](https://user-images.githubusercontent.com/68828858/196739515-976bb824-f720-4bd0-bf05-3045160260be.PNG)




