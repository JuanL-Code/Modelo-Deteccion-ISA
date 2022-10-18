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
1. Para la creacion de un modelo de IA enfocado a un modo de falla o cualquier otro uso se comienza haciendo una recoleccion minima de unas 100 images
2. Estas imagenes se exportaran a un software basado en python llamado "LabelIMG" en el cual se hace una seleccion de la zona que corresponde a la indicada y se le da un nombre de clase, lo que hace LabelIMG es guardar un archivo .txt el cual guarda las posiciones cartesianas dentro de esa imagen de tal manera que hace una correlacion 
