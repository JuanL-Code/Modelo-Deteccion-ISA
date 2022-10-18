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

