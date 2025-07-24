# Unidad 1

## 🤔 Fase: Reflect

### Actividad 5

### Actividad 5

Sin consultar tus apuntes, el simulador o cualquier otro material, responde con tus propias palabras a las siguientes preguntas. ¡No te preocupes por la perfección! El objetivo es ver qué recuerdas ahora mismo.

Parte 1: recuperación de conocimiento (retrieval practice)

Describe con tus palabras las tres fases del ciclo Fetch-Decode-Execute.
Fetch Decode y Execute: primero lo que pasa es que se obtiene la informacion en la fase de Fetch de la memoria como las instrucciones con @

luego el computador interpreta en la fase de Decode

al final en la fase execute se ejcutan las dichas instrucciones y los saltos

¿Qué rol juega el Program Counter (PC) en este ciclo?

El pc basicamente es una guia, siempre indica que instruccion sigue, que salto se hace y muestra que ocurrira en el programa mostrando cada instruccion

¿Cuál es la diferencia fundamental entre una instrucción-A (que empieza con @) y una instrucción-C (que involucra D, M, A, etc.) en el lenguaje ensamblador de Hack? Da un ejemplo de cada una.

Por ejemplo con la instruccion A (@): carga una direccion o constante en el registro A que se puede ver en el computador Hack
por ejemplo @10 que coloca 10 en A

Instruccion C: recibe el valor de A o realiza calculos, con la M tambien puede pasar datos a la RAM
que seria el valor que se encuentre en la A
Diferencias
La instrucciónA asigna direcciones o valores, la instrucción D realiza operaciones o saltos.


Explica la función de los siguientes componentes del computador Hack: el registro D, el registro A y la ALU.

el registro D guarda el dato proporcionado el registro A y lo puede enviar al registro de la Ram o realizar operaciones matematicas basicas
el registro A puede almacenar datos como numeros y de ahi enviarlos a el registro D
la Alu colabora para realizar operaciones matematicas o logicas

¿Cómo se implementa un salto condicional en Hack? Describe un ejemplo (p. ej., saltar si el valor de D es mayor que cero).

el Salto se realiza jump y se ejcuta si el resultado comp cumple la condicion, como que el numero sea mayor que o menor que una condicion
D;JGT

¿Cómo se implementa un loop en el computador Hack? Describe un ejemplo (p. ej., un loop que decremente un valor hasta que llegue a cero).

Es similar al salto se usa la instruccion D;JGT o D;JLE
la segunda oopcion siendo less or equal

``` asm

@7
D=A
@0
M=D
(LOOP)
M=M-1
D=M
@END
D;JLE
@LOOP
0;JMP
(END)
@8
M=D
```

¿Cuál es la diferencia entre la instrucción D=M y la instrucción M=D?

la primera instruccion D=M es que el registro que hay en D se guardara en la direccion de la ram actual mientras que la otra es que el registro de memoria actual pasara al registro D


Describe brevemente qué se necesita para leer un valor del teclado (KBD) y para “pintar” un pixel en la pantalla (SCREEN).

en primer lugar se necesita activar el teclado y llamar con @KEYBOARD ademas de etiquetarlo (KEYBOARD)


Parte 2: reflexión sobre tu proceso (metacognición)

¿Cuál fue el concepto o actividad más desafiante de esta unidad para ti y por qué?

Los loops y el teclado fue una de las cosas que mas me costo, no terminaba de comprenderlo y me equivocaba con los saltos pero al final lo logre manejar.

La metodología de “predecir, ejecutar, observar y reflexionar” fue central en nuestras actividades. ¿En qué momento esta metodología te resultó más útil para entender algo que no tenías claro?

la parte de predecir me costo un poco pq estaba mas acostumbrado a hacerlo desde el inicio, pero me di cuenta de que era muchisimo mejor predecir, me sirvio mucho en todas las actividades y en el ejemplo de la pregunta anterior, sobre todo me ayudo a entender el tema de los loops 

Describe un momento “¡Aha!” que hayas tenido durante estas dos semanas. ¿Qué estabas haciendo cuando ocurrió?

cuando logre hacer el loop y que el teclado reaccionara

Pensando en la próxima unidad, ¿Qué harás diferente en tu proceso de estudio para aprender de manera más efectiva?

estar mas pendiente de no equivocarme en las ramas y no cometer errores en la colocacion de las actividades en las carpetas
