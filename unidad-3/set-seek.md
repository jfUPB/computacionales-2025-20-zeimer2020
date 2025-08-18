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

Primero se mostrara el valor almacenado en A. Luego se invocara la funcion SumaPorValor(), a la cual se le pasa como parametro val_A, que en realidad es una copia de la variable original guardada en la memoria stack. Dentro de la funcion se suma 10 al valor recibido, por lo que en la consola aparecera: Dentro de sumaPorValor, 'a' ahora es: 30. Sin embargo, esto no altera el valor de val_A, ya que solo se modifico la copia y no la direccion de memoria de la variable original.

En el caso de B la situacion cambia, pues al ser pasado por referencia no se envia una copia, sino la variable real. Por eso, la operacion dentro de la funcion si modifica el valor de val_B, y el nuevo valor sera 30.

Algo similar ocurre en el tercer ejemplo, porque la funcion recibe directamente la direccion de memoria de la variable y trabaja sobre ella, lo que hace que el resultado final tambien sea 30.

Finalmente, con las tres llamadas a ejecutarContador(), el contador aumenta hasta 3. Aunque pareciera que la variable se reinicia en cada llamada, esto no ocurre, ya que al ser una variable estatica solo se inicializa una unica vez y conserva su valor entre ejecuciones.

Escribe la salida completa que esperas.

val_A: 20
val_B: 30
val_C: 30

contador_estatico: 3
Dibuja un mapa de memoria conceptual de este programa
(acordate de colocar el mapa)

Verificación y análisis

Comparación con el depurador

Output <img width="627" height="289" alt="image" src="https://github.com/user-attachments/assets/44e0707b-4e4e-48d2-8207-d3d5af7320d1" />


Los resultados coincidieron con lo esperado, pero para confirmar el motivo use un breakpoint y note que el sistema asigna un valor previo antes de la inicializacion real, y que los puntos clave son las lineas que modifican variables o llaman funciones, ya que ahi esta la diferencia del ejercicio.

Describe qué demuestran estas capturas sobre la diferencia entre los diferentes tipos de paso por parámetros analizados.

SumarPorValor()


<img width="598" height="332" alt="image" src="https://github.com/user-attachments/assets/6d053722-5c03-4661-9f54-5f7e09a8365e" />

SumarPorReferencia()

<img width="630" height="357" alt="image" src="https://github.com/user-attachments/assets/caf7c7d7-516e-4d9d-8262-60d4e28a7f55" />

<img width="643" height="417" alt="image" src="https://github.com/user-attachments/assets/b3e3c56c-5a05-489f-b616-47103fc6383a" />

SumarPorPuntero()


<img width="751" height="404" alt="image" src="https://github.com/user-attachments/assets/428c15bb-c09f-482c-9840-906813ede2b6" />

<img width="782" height="453" alt="image" src="https://github.com/user-attachments/assets/7cb2fccf-aa0c-439c-83e2-a2c8170792c6" />


Explica con tus propias palabras el comportamiento de contador_estatico. ¿Por qué “recuerda” su valor entre llamadas a la función ejecutarContador? ¿En qué se diferencia de una variable local normal?

Lo que sucede con una variable estatica es que conserva su valor porque queda asociada siempre al mismo lugar de memoria. Dicho de otro modo, no se crea una copia nueva cada vez que se llama, sino que se mantiene ligada a una direccion fija, lo que explica que solo se inicialice una unica vez y que luego “recuerde” lo que ya tenia.

La diferencia frente a una variable comun esta en el lugar donde se almacenan. Mientras las variables normales suelen vivir en la memoria stack y se destruyen al terminar la funcion, las estaticas se guardan en la misma zona de memoria que las globales. Esa ubicacion especial les da la capacidad de mantener su valor entre llamadas sucesivas y de no volver a inicializarse en cada ejecucio.

