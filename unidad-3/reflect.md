# Unidad 3


## 🤔 Fase: Reflect


#### Actividad de reflect

##### Explica con tus propias palabras qué es el stack y qué es el heap en C++.

ambas forman parte de la memoria del pc o la ram, sin embargo el stack guarda cosas locales mientras que el heap guarda una informacion que se debe inicializar o liberar y luego borrar para que no se consuma ram innecesaria.

##### Describe las tres formas de pasar parámetros a una función en C++ (valor, referencia y puntero). Para cada una, explica qué sucede en memoria y cuándo usarías cada método.

Con el valor lo que pasa es que cuando se llama se crea una copia y no se modifica la variable original, solo lo usaria si lo fuera a necesitar en funciones espcificas, como en momentos en los que quiero que sea diferente, ya que no modifica la original.

Con la referencia lo que se hace es llamar la variable original pero con un nombre distinto o un alias, este sirve si lo que se quiere es modificar la variable original.

con el puntero lo que se busca es intentar apuntar a la posicion de la variable, es decir, lo que se llama es la direccion de memoria donde esta la variable y se modifica lo que esta dentro de esta, lo usaria en casos donde necesite asignar una variable a otro objeto.


##### ¿Qué diferencia hay entre una variable local, una variable global y una variable local estática? ¿En qué segmento del mapa de memoria se almacena cada una?

una Varibale local solo puede usarse en un contexto local, osea si fue creada en una funcion especifica solo podra usarse en esa funcion especifca y se destruye al acabar la funcion, sin embargo una variable global se crea de una forma en la que se pueda usar desde cualquier lado, llamarla desde cualquier contexto, funcion o parte del codigo, ademas no se destruye, por otro lado la variable local estatica tiene la misma funcion que la variable local normal, pero esta no se destruye al finalizar la funcion en la que este. la Variable local se guarda en el stack mientras que las globales y globales estaticas tienen guardado en una direccion de memoria especial para mantenerse el resto del codigo.


##### Explica qué es un objeto en C++ desde la perspectiva de memoria. ¿Dónde se almacenan los miembros de instancia y dónde los miembros estáticos?


Un objeto es un bloque de memoria que guarda datos en una direccion.
los miembros de instancia tienen que se instanciados y eliminadeos por lo que hacen parte de la memoria heap, mientras que los estaticos existen durante todo el programa entonces se almacenan en la moemoria de variables estaticas y globales

codigo problematico 

``` c++
#include <iostream>
using namespace std;

class Enemigo {
public:
    static int totalEnemigos;
    int vida;
    int* armas;

    Enemigo(int v) : vida(v) {
        totalEnemigos++;
        armas = new int[3];
        armas[0] = 10; armas[1] = 15; armas[2] = 20;
    }
};

int Enemigo::totalEnemigos = 0;

void crearEscuadron() {
    for(int i = 0; i < 5; i++) {
        Enemigo soldado(100);
        soldado.vida -= 10;
    }
    cout << "Escuadrón creado. Total enemigos: " << Enemigo::totalEnemigos << endl;
}
int main() {
    crearEscuadron();
    crearEscuadron();
    return 0;
}
```
##### Análisis de problemas: identifica al menos dos problemas serios en este código relacionados con el manejo de memoria. Explica por qué cada uno es problemático.

uno de los problemas es que no hay  destructor entonces variables como las armas no se destruyen nunca pero se crean y no se usan, entonces se esta ocupando espacio de la ram lo cual hara que el codigo vaya mas lento.

el segundo problema radica en que cuando se crea otro escuadron deberia destruirse el anterior, pero esto no ocurre


##### Predicción de comportamiento: ¿Qué valor mostrará totalEnemigos después de ejecutar el programa? ¿Por qué ocurre esto?

primero muestra 5 y luego muestra 10, esto ocurre pq llamamos a la funcion 2 veces seguidas y los escuadrones de enemigos no se destruyen despues de llamar a otro


##### Propuesta de solución: escribe una versión corregida de la clase Enemigo que solucione los problemas identificados. Explica brevemente cada cambio que hiciste.


``` c++
#include <iostream>
using namespace std;

class Enemigo {
public:
    static int totalEnemigos;
    int vida;
    int* armas;

    Enemigo(int v) : vida(v) {
        ++totalEnemigos;
        armas = new int[3];
        armas[0] = 10; armas[1] = 15; armas[2] = 20;
    }

    ~Enemigo() {
        delete[] armas;   
        --totalEnemigos;    
    }
};

int Enemigo::totalEnemigos = 0;

void crearEscuadron() {
    for (int i = 0; i < 5; ++i) {
        Enemigo soldado(100);
        soldado.vida -= 10;
    }
    cout << "Escuadrón creado. Total enemigos: " << Enemigo::totalEnemigos << endl;
}

int main() {
    crearEscuadron();
    crearEscuadron();
    return 0;
}

``` 













