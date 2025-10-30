# Bitácora de aprendizaje de la unidad 8
<a name = "actividad1"> </a>

# Actividad 1

# primera vez: 
# ¿Qué es lo que ves? 
# ¿Qué es lo que esperabas ver? 
# ¿Por qué crees que sucede esto?
Entiendo que estan reescribiendo la funcion threadedFunction para incluir heavyComputation(), y que la misma libreria, al invocar ese metodo, la manda a otro hilo. En cuanto al retraso al cambiar el tamano del circulo, parece estar relacionado con otras llamadas que se ejecutan al mismo tiempo, y el probable responsable es lock(): como explico el profe, se usa para evitar condiciones de carrera, asi que vuelve esa parte exclusiva y hace que el hilo principal tenga que esperar a que termine; por eso, mientras el candado esta activo, el cambio de tamano del circulo no se refleja de inmediato


# segunda vez: Ejecuta el programa y haz clic en la ventana. Observa lo que sucede. ¿Qué es lo que ves? ¿Qué es lo que esperabas ver? ¿Por qué crees que sucede esto?

Veo que están reescribiendo la funcion threadedFunction para incluir heavyComputation(), y supongo que la libreria, al llamar ese metodo, lo manda a un hilo aparte. En cuanto al retraso al cambiar el tamaño del círculo, parece estar relacionado con las demás llamadas que se ejecutan y, creo, el responsable es lock(): como explico el profe, se usa para evitar condiciones de carrera, asi que deja esa seccion como exclusiva y hace que el hilo principal tenga que esperar a que termine, lo que demora que el circulo cambie de tamaño


# En tus propias palabras, explica la diferencia entre concurrencia y paralelismo. ¿Por qué es importante entender esta diferencia al trabajar con hilos?

En pocas palabras: la concurrencia es ir avanzando de a poquitos en varias tareas dentro de un periodo corto, dando la sensacion de que ocurren a la vez. El paralelismo, en cambio, ejecuta varias tareas al mismo tiempo de verdad. Por eso, un solo hilo puede ser concurrente alternando entre varias cosas; pero para hablar de paralelismo se necesitan varios hilos (y normalmente varios nucleos) trabajando en paralel
<a name = "actividad2"> </a>

# Actividad 2

El profe ya me adelanto el tema: esto puede dar lugar a condiciones de carrera. Eso implica que el rendimiento no necesariamente empeora, pero si pueden aparecer errores porque varios hilos trabajan sobre datos distintos que, al final, afectan el mismo recurso compartido. La manera de evitarlo es usar un mutex, que se encarga de permitir que solo un hilo modifique el valor

# Ejecuta el código y observa el resultado. ¿Qué ocurre si cambias el valor de la variable useLock? ¿Por qué crees que ocurre esto?

<img width="514" height="159" alt="image" src="https://github.com/user-attachments/assets/7013886f-aec1-4ad2-a294-5efac253a393" />
<img width="498" height="148" alt="image" src="https://github.com/user-attachments/assets/4520593c-06bb-4e11-b2aa-17472a2fb703" />
esto pasa ya que hay varios hilos simultaneamente agarrando el mismo valor 

# Explica en tus propias palabras ¿Cómo puede presentarse la condición de carrera en este caso? ¿Qué es lo que está pasando? Te pido que propongas un ejemplo.

Se presenta una condicion de carrera cuando dos hilos leen y escriben el mismo dato sin coordinarse: ambos leen un valor viejo y luego una escritura pisa la otra, dejando un resultado incorrecto. Ejemplo: en una agenda de quirofano con 1 cupo a las 10:00, dos hilos leen cupo=1 casi a la vez y ambos reservan; uno escribe cupo=0 y el otro tambien, y terminas con dos cirugias en un unico cupo aunque el contador final parezca coherente.

<a name = "actividad3"> </a>
# Activdidad 3

<img width="1129" height="672" alt="image" src="https://github.com/user-attachments/assets/cef21954-c626-4207-9158-c7f75563bbb3" />
En esta linea: numThreads = std::thread::hardware_concurrency(), el valor devuelto es 16, que corresponde a los cores de mi cpu. Sin embargo, la diferencia en tiempo de computo entre usar un solo hilo y usar 16 es menor a 0.1 s, lo cual me resulta curioso por lo pequena que es. De ahi surge mi pregunta: ¿existen programas en los que lanzar tantos threads sea un gasto innecesario de recursos cuando un unico hilo basta? En este caso seguramente no aplica, pero me quedo la duda y quiero hacer la comparacion. Tambien quiero saber que pasa internamente si fuerzo ese numero a ser mayor que 16.

Mi hipotesis es que el rendimiento sera igual o incluso mas lento: o bien el sistema ignora los cores inexistentes, o reutiliza los que ya hay sin lograr verdadero paralelismo; en cualquier caso, no esperaria una mejora.

diferentes cantidades de threads

16:<img width="377" height="137" alt="image" src="https://github.com/user-attachments/assets/10f00ef4-516a-4d7a-9b94-6f901e727868" />


64:<img width="346" height="138" alt="image" src="https://github.com/user-attachments/assets/aeb1ee8f-32c3-4e2f-a6aa-5dfd55edd74a" />

<a name = "actividad4"> </a>
# Actividad 4

### Cual es la estructura de datos principal que contiene la informacion de todos los boids y que es accedida por multiples hilos?
std::vector<Boid> boids dentro de la clase Flock.

### Observa la funcion Flock::threadedFunction() donde el hilo trabajador calcula el movimiento. Que operaciones realizan sobre el vector de boids compartido?
Toma el lock, itera boids y actualiza cada boid con b.run(boids), suelta el lock y hace sleep(5).

### Observa la funcion ofApp::draw(). Que operacion realiza sobre el vector compartido?
Toma el lock, recorre boids para dibujar (b.draw()), y libera el lock.

### Observa Flock::addBoid() y ofApp::mouseDragged(). Que operacion realizan?
Insercion en el contenedor compartido: mouseDragged llama flock.addBoid(x,y) y addBoid hace boids.emplace_back(...) bajo lock.

### Describe un escenario especifico y concreto donde la falta de sincronizacion podria causar un problema.
Mientras el hilo trabajador itera boids para actualizar vecindades, mouseDragged agrega un boid; si no hay lock, el vector puede reubicarse e invalidar el iterador del hilo trabajador, causando lecturas fuera de rango o cuelgue.

### Localiza todas las llamadas a lock() y unlock() dentro de la clase Flock (o donde se acceda al vector compartido).
En Flock::addBoid() (lock/unlock alrededor de emplace_back), en Flock::threadedFunction() (lock/unlock durante la actualizacion), y en ofApp::draw() usando flock.lock() / flock.unlock() para dibujar.

### Justificacion: explica como las llamadas a lock()/unlock() evitan que ocurra ese problema especifico.
El lock serializa el acceso: si el hilo trabajador posee el lock al iterar, addBoid() espera y no hay reubicacion del vector ni iteradores invalidos durante la actualizacion.

### Aunque los locks aseguran la correctitud, por que muchos hilos esperando el mismo lock (alta contencion) limita el beneficio de rendimiento del paralelismo?
Porque el acceso se vuelve secuencial: solo un hilo entra a la seccion critica, los demas esperan, aumentan los cambios de contexto y el lock se convierte en cuello de botella que reduce o anula la ganancia.


### Analiza el codigo del Flocking sin hilos y el Flocking con hilos. Que diferencias encuentras? Por que crees que es importante la sincronizacion en el segundo caso?
Sin hilos: el update y el draw ocurren en el hilo principal y acceden al mismo vector de boids de forma secuencial. Con hilos: Flock hereda de ofThread y un hilo trabajador actualiza boids en threadedFunction mientras el hilo principal dibuja; ambos tocan el mismo vector<Boid>. La sincronizacion (lock/unlock) es clave para evitar condiciones de carrera, invalidacion de iteradores y estados inconsistentes.

### Por que al agregar un nuevo boid la simulacion se ralentiza? Que ocurre si agregas muchos boids?
Porque las reglas de vecindad hacen el costo cercano a O(n^2) y cada insercion puede reubicar memoria; en la version con hilos ademas hay lock al insertar y lock durante la actualizacion y el dibujado, aumentando esperas. Con muchos boids sube el tiempo por cuadro y cae el FPS.

### Notaste que la version con hilos tiene un sleep(5) en el hilo trabajador. Por que crees que se ha anadido? Que pasaria si lo eliminamos?
Para ceder CPU y reducir contencion, evitando que el hilo de update acapare el lock y permitiendo que el dibujado respire. Si se elimina, el hilo trabajador corre sin pausa, sube el uso de CPU, aumenta la contencion sobre el lock y es probable que el render se vea mas trabado.

### Compara el rendimiento de ambos enfoques. Cual crees que es mas eficiente? Por que?
Con el diseno actual (un solo lock grueso alrededor de todo el update y locks en draw e inserciones), el enfoque sin hilos suele ser mas eficiente y estable: hay menos sobrecosto de sincronizacion y no se serializa trabajo por contencion que anula el paralelismo.

### El uso de lock y unlock en la version con hilos es crucial para evitar condiciones de carrera. Que pasaria si no se usaran? Como afectaria esto al comportamiento del programa?
Habria carreras: inserciones invalidando iteradores durante la iteracion, lecturas/escrituras inconsistentes y posibles fallos o resultados no deterministas (boids que saltan, conteos incorrectos, congelamientos esporadicos). Aunque cueste reproducirlo siempre, el riesgo es real.

<a name = "actividad5"> </a>
# Actividad 5

### Pega la parte clave de tu función modificada que calcula el píxel para el conjunto de Julia. Recuerda utilizar un bloque cpp

``` c++
for (int j = 0; j < h; ++j) {
    for (int i = 0; i < w; ++i) {
        double a = centerX + ((i - w * 0.5) / (double)w) * scale;
        double b = centerY + ((j - h * 0.5) / (double)h) * (scale * ((double)h / (double)w));
        double zx = a, zy = b;
        int iter = 0;
        while ((zx*zx + zy*zy <= 4.0) && (iter < maxIter)) {
            double xt = zx*zx - zy*zy + kx;
            zy = 2.0 * zx * zy + ky;
            zx = xt;
            ++iter;
        }
        ofColor c(0,0,0);
        if (iter < maxIter) {
            unsigned char v = (unsigned char)ofMap(iter, 0, maxIter, 0, 255, true);
            c.set(v, (unsigned char)(255 - v), (unsigned char)((v * 7) % 255));
        }
        pix.setColor(i, j, c);
    }
}
img.update();
```
### Muestra cómo mapeaste la posición del mouse a la constante k.

``` c++
void ofApp::mouseMoved(int x, int y){
    double aspect = (double)h / (double)w;
    kx = centerX + ((x - w * 0.5) / (double)w) * scale;
    ky = centerY + ((y - h * 0.5) / (double)h) * (scale * aspect);
    dirty = true;
    cv.notify_one();
}
```
### Reutilizacion de la estructura de hilos
Se reutilizo el mismo hilo trabajador y la misma condicion de espera con una bandera dirty. Unicamente se sustituyo la rutina de calculo (de Mandelbrot a Julia) y se anadio el par kx, ky. El resto de la sincronizacion y el doble buffer permanecen iguales.

### Recalculo al mover el mouse
Cada movimiento de mouse actualiza kx, ky y activa dirty; el hilo trabajador detecta dirty, recalcula el ofPixels y el hilo principal sube el resultado al ofImage en update().

### imagenes 

<img width="1010" height="754" alt="image" src="https://github.com/user-attachments/assets/d1e36515-f727-4519-a00a-d5f500d5d14a" />
<img width="1012" height="752" alt="image" src="https://github.com/user-attachments/assets/d833d2ad-c857-4f37-a19c-ecf8bc86ce3c" />
<img width="1007" height="752" alt="image" src="https://github.com/user-attachments/assets/53e138c1-51a4-4d82-9864-1e93cc4e7353" />
### que se me complico
Controlar la estabilidad del mapeo del mouse para explorar sin saltos, evitar recalculos excesivos marcando con dirty en lugar de regenerar cada frame, y asegurar que la copia de pixeles ocurra fuera de la zona critica para no bloquear el dibujo ni mostrar artefactos.

# Autoevaluacion 

Todas las actividades completas 

[evidencia](#actividad1)
[evidencia](#actividad2)
[evidencia](#actividad3)
[evidencia](#actividad4)
[evidencia](#actividad5)
nota: 5












