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

