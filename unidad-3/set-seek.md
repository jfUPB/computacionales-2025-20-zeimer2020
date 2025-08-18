# Unidad 3

## 🔎 Fase: Set + Seek

¿Para qué sirven los breakpoints?: para congelar el codigo en un punto preciso para analizar su funcionamiento

¿Para qué se usa la ventana de depuración Autos?: para observar cómo cambian las variables y ver el funcionamiento del programa


``` c++
#include <iostream>

using namespace std;

// Función que modifica el parámetro pasado por valor
void modificarPorValor(int n) {
    cout << "Dentro de modificarPorValor, valor inicial: " << n << endl;
    n += 5;
    cout << "Dentro de modificarPorValor, valor modificado: " << n << endl;
}

// Función que modifica el parámetro pasado por referencia
void modificarPorReferencia(int &n) {
    cout << "Dentro de modificarPorReferencia, valor inicial: " << n << endl;
    n += 5;
    cout << "Dentro de modificarPorReferencia, valor modificado: " << n << endl;
}

// Función que modifica el parámetro utilizando punteros
void modificarPorPuntero(int *n) {
    cout << "Dentro de modificarPorPuntero, valor inicial: " << *n << endl;
    *n += 5;
    cout << "Dentro de modificarPorPuntero, valor modificado: " << *n << endl;
}

int main() {
    int a = 10;
    int b = 10;
    int c = 10;

    cout << "Valor inicial de a (paso por valor): " << a << endl;
    cout << "Valor inicial de b (paso por referencia): " << b << endl;
    cout << "Valor inicial de c (paso por puntero): " << c << endl;

    cout << "\nLlamando a modificarPorValor(a)..." << endl;
    modificarPorValor(a);
    cout << "Después de modificarPorValor, valor de a: " << a << endl;

    cout << "\nLlamando a modificarPorReferencia(b)..." << endl;
    modificarPorReferencia(b);
    cout << "Después de modificarPorReferencia, valor de b: " << b << endl;

    cout << "\nLlamando a modificarPorPuntero(&c)..." << endl;
    modificarPorPuntero(&c);
    cout << "Después de modificarPorPuntero, valor de c: " << c << endl;

    return 0;
}
```


#### Acitivad 4

##### exp 1 se muestra una excepcion pq se esta tratando de modificar el area de solo lectura, osea la funcion main

##### exp 2 no se pudo realizar pq se intenta cambiar una constante

##### exp 3 al empezar la variable se ve con numero asigno y la que no se ha inicializado tiene0, despues la variable inicializada cambia de numero

##### exp 4 una variable indicada como variable estatica no se puede modificar, debido a esto no es posible modificar la variable en este caso

#### Actividad 5 integradora

analizar un programa integral, predecir su comportamiento en memoria y verificar tus hipótesis utilizando el depurador de Visual Studio.

``` c++
#include <iostream>

int contador_global = 100;

void ejecutarContador() {
    static int contador_estatico = 0;
    contador_estatico++;
    std::cout << "  -> Llamada a ejecutarContador. Valor de contador_estatico: " << contador_estatico << std::endl;
}

void sumaPorValor(int a) {
    a = a + 10;
    std::cout << "  -> Dentro de sumaPorValor, 'a' ahora es: " << a << std::endl;
}

void sumaPorReferencia(int& a) {
    a = a + 10;
    std::cout << "  -> Dentro de sumaPorReferencia, 'a' ahora es: " << a << std::endl;
}

void sumaPorPuntero(int* a) {
    *a = *a + 10;
    std::cout << "  -> Dentro de sumaPorPuntero, '*a' ahora es: " << *a << std::endl;
}

int main() {
    int val_A = 20;
    int val_B = 20;
    int val_C = 20;

    std::cout << "--- Experimento con paso de parámetros ---" << std::endl;
    std::cout << "Valor inicial de val_A: " << val_A << std::endl;
    sumaPorValor(val_A);
    std::cout << "Valor final de val_A: " << val_A << std::endl << std::endl;

    std::cout << "Valor inicial de val_B: " << val_B << std::endl;
    sumaPorReferencia(val_B);
    std::cout << "Valor final de val_B: " << val_B << std::endl << std::endl;

    std::cout << "Valor inicial de val_C: " << val_C << std::endl;
    sumaPorPuntero(&val_C);
    std::cout << "Valor final de val_C: " << val_C << std::endl << std::endl;

    std::cout << "--- Experimento con variables estáticas ---" << std::endl;
    ejecutarContador();
    ejecutarContador();
    ejecutarContador();

    return 0;
}
```
Predicción

¿Cuál será la salida final en la consola de este programa?

En un principio va a mostrar el valor guardado en A, posteriormente llamará la función SumaPorValor() y le entregará como parametro val_A, que como aprendimos en realidad es una copia de la variable inicializada en la memoria stack. Dentro de esta función se le sumará 10 al valor que entregó "a", por lo que en la consola escribirá: Dentro de sumaPorValor, 'a' ahora es: 30, sin embargo esto no cambiará el valor de val_A puesto que no se modificó el valor en el espacio de memoria de esta variable, solo el de la copia.
En el caso de B esto es diferente, puesto que es por referencia entonces no le pasa una copia sino la variable de verdad, por lo que la operación que se realiza dentro de la función si afecta el valor de la variable val_B. El nuevo valor será 30.
En este caso tambien se modifica el valor de la variable entregada, sin embargo lo hace diferente, puesto que recibe el espacio de memoria de la variable y eso es lo que manipula realmente, provocando que el resultado final sea 30.
Por último están esas tres llamadas a la función ejecutarContador(), en este caso si se aumentaría el contador hasta 3, incluso si parece que reescribe la variable varias veces este no es el caso puesto que una variable estática solo se puede inicializar una vez.
Escribe la salida completa que esperas.

val_A: 20
val_B: 30
val_C: 30

contador_estatico: 3
Dibuja un mapa de memoria conceptual de este programa

Verificación y análisis

Comparación con el depurador

Output <img width="627" height="289" alt="image" src="https://github.com/user-attachments/assets/44e0707b-4e4e-48d2-8207-d3d5af7320d1" />


De primerazo observo que efectivamente los resultados finales concuerdan con lo que predije, sin embargo me gustaría saber si eso pasó por las razones correctas, entonces ahora voy a hacer un análisis más a fondo utilizando el breakpoint.

Observé que una línea antes de que se inicialice una variable el computador la inicializa antes y le asigna un valor antes de asignarle el valor real.

Los puntos de interés me imagino que se refieron a aquellas líneas de código que alteral variables o ejecutan acciones. Por otro lado tambien pienso que se pueden referir a cuando se llaman funciones, pues es donde radica la diferencia del ejercicio que nos compete.

Describe qué demuestran estas capturas sobre la diferencia entre los diferentes tipos de paso por parámetros analizados.

SumarPorValor()

Acá observamos como se crea una copia cuando el parámetro entregado es solo "int a"

<img width="598" height="332" alt="image" src="https://github.com/user-attachments/assets/6d053722-5c03-4661-9f54-5f7e09a8365e" />

SumarPorReferencia()
Acá se puede ver como aunque se crea una copia de la variable esta igual modifica la variable entregada como parámetro, por eso es que se ve que el valor fue modificado.

<img width="630" height="357" alt="image" src="https://github.com/user-attachments/assets/caf7c7d7-516e-4d9d-8262-60d4e28a7f55" />

<img width="643" height="417" alt="image" src="https://github.com/user-attachments/assets/b3e3c56c-5a05-489f-b616-47103fc6383a" />

SumarPorPuntero()
Este me gustó mucho observar que sucedia puesto que se ve como literal agarra el espacio de memoria donde está guardado el valor y lo utiliza para crear una copia de una variable para así modificar su valor y finalmente alterar el valor.

<img width="751" height="404" alt="image" src="https://github.com/user-attachments/assets/428c15bb-c09f-482c-9840-906813ede2b6" />

<img width="782" height="453" alt="image" src="https://github.com/user-attachments/assets/7cb2fccf-aa0c-439c-83e2-a2c8170792c6" />


Explica con tus propias palabras el comportamiento de contador_estatico. ¿Por qué “recuerda” su valor entre llamadas a la función ejecutarContador? ¿En qué se diferencia de una variable local normal?
Entiendo que recuerda su valor por que es estático, sin embargo la razón por la cual una variable estática "recuerda" díria que es por que es una especie de referencia constante, es decir, es una variable a la que siempre que se llama su valor va ligado con un espacio de memoria específico, y por eso solo se inicializa una vez y recuerda su valor.

Se diferencia de una variable normal por el espacio de memoria donde está guardado, las variables estáticas estánn guardado en el espacio de memoria donde también están las globales, lo que le da sus propiedades únicas de recordar su valor y de solo ser inicializados una vez.

