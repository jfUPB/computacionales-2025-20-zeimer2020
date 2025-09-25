# Bitácora de aprendizaje de la unidad 6


### seek 
funcionamiento del programa:

### Actividad 1

##### ¿Cómo puedes interactuar con la aplicación? Menciona específicamente las teclas y qué efecto parecen tener sobre las partículas.

me permite realizar acciones como atraer las particulas con la A, alejarlas con la R, paralizarlas con la S y volver a la normalidad son la S, las funciones de atraccion y repeler se guian del mouse


##### ¿Observas los diferentes tipos de “partículas”? ¿Se comportan todas igual inicialmente?

no, cada una se comporta de manera diferente, las verdes son las mas rapidas, las rojas van a velocidad media y las azules son las mas lentas

##### Toma algunas capturas de pantalla de la aplicación en diferentes momentos (estado inicial, después de presionar ‘a’, ‘r’, ‘s’, ‘n’) y añádelas a tu bitácora.

Atraer
<img width="533" height="472" alt="image" src="https://github.com/user-attachments/assets/73d4907c-57e4-4dea-8de1-64fc5863b380" />
Nornal
<img width="980" height="617" alt="image" src="https://github.com/user-attachments/assets/0696f30f-c391-4ae8-95a7-3368c35c98e8" />
Stop despues de Repeler
<img width="993" height="571" alt="image" src="https://github.com/user-attachments/assets/1cbfd4c7-7f0a-4788-ab91-f374dc4cc37a" />

##### ¿Qué crees que está pasando “detrás de cámaras” cuando presionas las teclas? Formula una hipótesis inicial sobre cómo la aplicación cambia el comportamiento de las partículas.

cada vez que pulsamos una tecla llamamos un metodo o algun sector del codigo que modifica el comportamiento de las particulas, o tambien siplemente tenemos varios comportamientos y se activan una vez que pulsamos las diferentes teclas al momento de ejectuar el programa


Los observers lo que hacen es actualizarse cuando un objeto especifico cambia, por ejemplo tenemos una particula, si esa particula cambia y esta vinculada a los observers, todos estos se actualizaran en funcion del cambio realizado

### Actividad 2

Explica con tus propias palabras el propósito del patrón Observer. ¿Qué problema resuelve?
Dicho patron se encarga de usar o mas bien introducir polimorfismo, dejando que otras clasese que serian los observadores esten ahi tecnicamente suscritos (como dices en el ejemplo del github) a la clase que sea sujeto

Dibuja un diagrama que muestre la relación entre Subject, Observer, ofApp y Particle en el caso de estudio, indicando quién es el Sujeto y quiénes los Observadores.
<img width="721" height="619" alt="image" src="https://github.com/user-attachments/assets/ec60b1bc-7434-4a80-a919-a2ddb153114e" />


Construye un diagrama de secuencia que muestre cómo funciona el patrón Observer al presionar una tecla.


¿Qué ventajas crees que ofrece usar el patrón Observer en esta aplicación en comparación con, por ejemplo, que ofApp::update recorriera todas las partículas y les dijera directamente que cambien su comportamiento basado en una variable global? Piensa en términos de acoplamiento y extensibilidad.

Usar el patrón Observer reduce el acoplamiento porque las partIculas no dependen directamente de una variable global ni de que ofApp::update las controle, sino que reaccionan a notificaciones de un sujeto; esto facilita la extensibilidad, ya que se pueden añadir nuevos tipos de partIculas u observadores sin cambiar la lOgica central, manteniendo el cOdigo más limpio, modular y fAcil de mantener.














