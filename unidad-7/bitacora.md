# Bitácora de aprendizaje de la unidad 7

# actividad 1

<img width="685" height="543" alt="image" src="https://github.com/user-attachments/assets/665d86f7-22ea-4734-985d-f093546daef9" />

preguntas:

para que es un frambuffer?
para que son los comandos que empiezan con gl?
que haceel buildshaderprogram?

# actividad 2
Resumen

Descargamos tres dependencias externas (glad, glfw34 y glm-101-light), estas contienen librerías y archivos necesarios para poder crear un archivo usando OpenGL. Después de descargarlas, le edecimos a visual en dónde tenía que buscar los archivos importantes, para que no haya errores a la hora de compilar ni ejecutar los programas que allí creemos.

# actividad 3

<img width="469" height="406" alt="image" src="https://github.com/user-attachments/assets/05905355-25ce-44b8-b3b1-3eeda1461173" />

esto es lo que pasa 

# respuesta a las preguntas iniciales

framebuffer: Memoria donde OpenGL dibuja cada cuadro.	Es lo que finalmente se muestra en pantalla.

comandos gl o contexto openGl: Entorno donde OpenGL guarda todo su estado.	Sin él, no se pueden ejecutar funciones de OpenGL.

# Actiidad 4
# Experimentos 

Si coloco Gl_Line y Gl_Points cambian el tipo de forma en la que se dibuja el triangulo, sin embargo se mantiene de alguna forma una referencia al triangulo original con Gl_triangles

¿Qué es el contexto OpenGL?: Es el contexto en el que se van a ejecutar ciertas acciones, con el fin de que la computadora dibuje algo.

¿Cuál es el rol de la biblioteca GLFW y qué ventaja tiene usarla?: Básicamente nos ayuda con funciones que nos sirven para crear la ventana donde se va a mostrar nuestro trabajo, sin necesidad de escribir nuevo código para cada caso específico.

¿Por qué crees que OpenGL necesita un contexto (recuerda la analogía del taller de arte)?: Según esa analogía, es porque sin el contexto, OpenGL no tiene donde trabajar (un artista sin su taller), por lo que no podríamos dibujar nada.

¿En últimas qué será el framebuffer y a qué te recuerda de las dos primeras unidades del curso?: El framebuffer termina siendo una porción de memoria, y me recuerda muchoa cómo dibujábamos al principio del curso en el lenguaje ensamblador, especificando la posición en memoria de los pixeles que queremos pintar.

¿Qué relación entre en el viewport y el framebuffer?: Según entendí, el viewport es la parte (en pantalla) que se va a pintar, lo que requiere informarle al framebuffer qué porción de memoria se requiere para esto.

¿En todo la analizado hasta ahora qué rol juega los drivers de la GPU y la GPU misma?: Básicamente, los drivers de la GPU contienen funciones, las cuales nos re sirven para poder dibujar más cosas, y la GPU es literalmente el artista que crea las obras que nosotros le pedimos.

¿Por qué crees que sea necesario activar el VSync? ¿Si no lo activas y la imagen es estática qué crees que pase, y si es dinámica?: Aquí desde mi ignorancia, si la imagen es estática, sería importante para que no empiece a titilar o a hacer cosas raras, y si es dinámica, para que se vea fluido el movimiento.

En esta unidad estamos usando OpenGL moderno, pero ¿Qué es OpenGL Legacy? ¿Qué diferencias hay entre ambos?: Según entendí, la diferencia radica en el pipeline (no sé qué es eso). Mientras el moderno tiene un pipeline programable, el Legacy tiene un pipeline fijo (supongo que esto lo entenderé más adelante).

¿Que es el shader program? ¿Por que es importante en OpenGL moderno?
Es el programa que combina los shaders y le dice a la GPU como procesar vertices y pixeles. Es vital porque en OpenGL moderno todo el dibujo depende de estos programas, no hay funciones fijas para hacerlo.

¿Que crees que hace setupTriangle()? ¿Que es el VAO y el VBO?
setupTriangle() probablemente crea los buffers y configura la informacion del triangulo para que se pueda dibujar. El VBO guarda los datos de los vertices, y el VAO guarda la configuracion que indica como leer esos datos.

¿Si se usa el shader y VAO antes del loop es necesario repetirlo? ¿En que casos seria util hacerlo?
No es necesario repetirlo si no cambian, pero puede ser util si se usan varios shaders, varios objetos o si una funcion externa cambia el estado y quieres asegurarte de que todo siga correcto.

¿Por que es importante glfwSwapBuffers()? ¿Que pasa si no se llama?
Cambia el buffer donde se dibujo por el que se muestra en pantalla. Si no se llama, la imagen nunca se actualiza y la ventana se queda congelada o negra, porque OpenGL solo dibujo en memoria sin mostrarlo.

# CPU y GPU

la CPU hace pocas taras pero muy complejas mientras que la GPU se encarga de multiples tareas, una gran variedad, sin embargo son simples, pero las hace al mismo tiempo.


¿Cuáles son los tres pasos claves del pipeline de OpenGL?
Transformación, rasterización y shading. Transformación convierte coordenadas a espacio de pantalla, rasterización convierte figuras en fragmentos, y shading calcula color y efectos visuales.

¿Qué significa el pipeline programable?
Que ahora el programador puede definir cómo se procesan vértices y fragmentos usando shaders, en lugar de depender de funciones fijas de OpenGL.

¿Qué diferencia hay entre el pipeline fijo y el programable?
El fijo usaba rutinas predefinidas por OpenGL; el programable permite personalizar el proceso con shaders escritos por el usuario.

¿Qué ventajas le ves a esto?
Mayor control, flexibilidad y posibilidad de crear efectos visuales avanzados o estilos únicos.
Si el pipeline es programable, ¿Qué tengo que programar?
Principalmente el vertex shader y el fragment shader, aunque se pueden usar más etapas como geometry o compute shaders.
Si fueras a describir el proceso de rasterización, ¿Qué dirías?
Convierte las primitivas (como triángulos) en fragmentos que luego se transforman en píxeles en pantalla.

¿Qué son los fragmentos? ¿Es lo mismo un fragmento que un pixel? ¿Por qué?
Un fragmento es un candidato a pixel, con datos como color y profundidad; solo se convierte en pixel si pasa las pruebas del pipeline (como el depth test).

Explica qué problema resuelve el Z-buffer y qué es el depth test.
El Z-buffer guarda la profundidad de cada fragmento; el depth test decide si un fragmento debe verse o quedar oculto detrás de otro.

¿Por qué se presenta el problema del aliasing? ¿Qué es el anti-aliasing?
El aliasing ocurre por la baja resolución al dibujar líneas o bordes; el anti-aliasing suaviza esos bordes mezclando colores cercanos.

¿Qué relación hay entre la iluminación y el fragment shader?
El fragment shader puede calcular la luz sobre cada fragmento. No es obligatorio usar iluminación, pero si no se usa, la escena se verá plana o sin volumen.

¿Qué implica para la GPU que una aplicación tenga múltiples fuentes de iluminación?
Más cálculos por fragmento, lo que aumenta la carga de procesamiento y puede reducir el rendimiento.













