# Unidad 1

## 🔎 Fase: Set + Seek

### Actividad 01

#### Ciclo feetch-decode-execute
el proposito de esta actividad es entender como funciona el ciclo fetch-decode-execute

``` asm
@1
D=A
@2
D=D+A
@16
M=D
@END
(END)
0;JMP
```

Reporta tus observaciones para cada experimento en tu bitácora de aprendizaje.

¿Qué sucede? ¿Qué valor se almacena en la dirección de memoria 16? ¿Por qué crees que es ese valor? ¿Qué instrucciones se ejecutan en cada ciclo Fetch-Decode-Execute? ¿Qué cambios observas en el contenido de la memoria y los registros? ¿Qué instrucciones se ejecutan en cada ciclo Fetch-Decode-Execute?

lo que sucede es que despues de almacenar datos en A  se le asignan a D y se suman para dar unos resultados, el dato almacenado en la direccion 16 es el numero 3, lo creo ya que lo almacenamos en la Ram y lo podemos ver ahi. 

Lo que ocurre es que primero recupera los datos colocados, basicamente lo que le decimos que haga, luego lo decodifica a un lenguaje que la propia computaodra pueda entender y al final ejecuta las ordenes que le dimos.

Los cambios observados en la memoria y registros dependen de que le digamos que haga, por ejemplo la ram almacena lo que digamos en la direccion 16 o la 20 segun que le pidamos.

¿Qué diferencia hay entre los datos almancenados en la memoria ROM y en la RAM?

en el segundo experimento vemos como ocurre lo mismo que en el primero solo que se almacena en la direccion 20 el numero 15

Los datos guardados en la moemoria ram son temporales y se desaparecen al apagar el equipo, mientras que los datos guardados en la memoria rom son datos que siempre estan, ademas no cambian o solo cambian mediante procesos especificos.


### Actividad 2

#### Identifica una instruccion que use la ALU y explica que hace
Una instruccion que usa la ALU es M=M-1. Lo que hace es tomar el numero que hay guardado en una posicion de la memoria y le resta 1. En este programa, se usa para ir bajando por la pantalla mientras se borran los punticos

#### Para que sirve el registro PC?
El PC es el que lleva el control de en que parte del programa vamos. el dice que instruccion se debe ejecutar ahora, y normalmente pasa a la siguiente linea, a menos que haya un salto que se escribe JMP que lo mande a otra parte

#### Cual es la diferencia entre @i y @READKEYBOARD?
@i sirve para guardar o usar un numero que esta en la memoria. por otro lado , READKEYBOARD no guarda nada, es solo una marca que le dice al programa donde volver o repetir una parte del codigo

#### Describe que se necesita para leer el teclado y mostrar informacion en la pantalla
Para leer el teclado se usa KBD, que es una direccion especial que nos dice si se presiono una tecla. Para mostrar algo en la pantalla se usan direcciones a partir de SCREEN, donde se puede escribir -1 para encender los pixeles o 0 para apagarlos

#### Identifica un bucle en el programa y explica su funcionamiento
El bucle empieza en la etiqueta READKEYBOARD y se repite una y otra vez. Revisa si alguien presiono una tecla. si no, borra un píxel de la pantalla y vuelve al inicio del bucle, si se presiono una tecla, cambia el comportamiento

#### Identifica una condicion en el programa y explica su funcionamiento
Una condicion del programa es D;JNE, que significa “salte si el valor en D no es 0”. Se usa justo después de leer KBD, para saber si se presiono una tecla. Si se presiono el programa salta a otra parte para hacer algo diferente





