# Bitácora de aprendizaje de la unidad 7

<a name = "actividad1"> </a>

# actividad 1

<img width="685" height="543" alt="image" src="https://github.com/user-attachments/assets/665d86f7-22ea-4734-985d-f093546daef9" />

preguntas:

para que es un frambuffer?
para que son los comandos que empiezan con gl?
que haceel buildshaderprogram?

<a name = "actividad2"> </a>

# actividad 2
Resumen

Descargamos tres dependencias externas (glad, glfw34 y glm-101-light), estas contienen librerías y archivos necesarios para poder crear un archivo usando OpenGL. Después de descargarlas, le edecimos a visual en dónde tenía que buscar los archivos importantes, para que no haya errores a la hora de compilar ni ejecutar los programas que allí creemos.

<a name = "actividad3"> </a>

# actividad 3

<img width="469" height="406" alt="image" src="https://github.com/user-attachments/assets/05905355-25ce-44b8-b3b1-3eeda1461173" />

esto es lo que pasa 

# respuesta a las preguntas iniciales

framebuffer: Memoria donde OpenGL dibuja cada cuadro.	Es lo que finalmente se muestra en pantalla.

comandos gl o contexto openGl: Entorno donde OpenGL guarda todo su estado.	Sin él, no se pueden ejecutar funciones de OpenGL.

<a name = "actividad4"> </a>

# Actiidad 4
# Experimentos 

### Si coloco Gl_Line y Gl_Points cambian el tipo de forma en la que se dibuja el triangulo, sin embargo se mantiene de alguna forma una referencia al triangulo original con Gl_triangles

### ¿Qué es el contexto OpenGL?: Es el contexto en el que se van a ejecutar ciertas acciones, con el fin de que la computadora dibuje algo.

### ¿Cuál es el rol de la biblioteca GLFW y qué ventaja tiene usarla?: Básicamente nos ayuda con funciones que nos sirven para crear la ventana donde se va a mostrar nuestro trabajo, sin necesidad de escribir nuevo código para cada caso específico.

### ¿Por qué crees que OpenGL necesita un contexto (recuerda la analogía del taller de arte)?: Según esa analogía, es porque sin el contexto, OpenGL no tiene donde trabajar (un artista sin su taller), por lo que no podríamos dibujar nada.

### ¿En últimas qué será el framebuffer y a qué te recuerda de las dos primeras unidades del curso?: El framebuffer termina siendo una porción de memoria, y me recuerda muchoa cómo dibujábamos al principio del curso en el lenguaje ensamblador, especificando la posición en memoria de los pixeles que queremos pintar.

### ¿Qué relación entre en el viewport y el framebuffer?: 
Según entendí, el viewport es la parte (en pantalla) que se va a pintar, lo que requiere informarle al framebuffer qué porción de memoria se requiere para esto.

### ¿En todo la analizado hasta ahora qué rol juega los drivers de la GPU y la GPU misma?: 
Básicamente, los drivers de la GPU contienen funciones, las cuales nos re sirven para poder dibujar más cosas, y la GPU es literalmente el artista que crea las obras que nosotros le pedimos.

### ¿Por qué crees que sea necesario activar el VSync? ¿Si no lo activas y la imagen es estática qué crees que pase, y si es dinámica?: 
Aquí desde mi ignorancia, si la imagen es estática, sería importante para que no empiece a titilar o a hacer cosas raras, y si es dinámica, para que se vea fluido el movimiento.

### En esta unidad estamos usando OpenGL moderno, pero ¿Qué es OpenGL Legacy? ¿Qué diferencias hay entre ambos?: 
Según entendí, la diferencia radica en el pipeline (no sé qué es eso). Mientras el moderno tiene un pipeline programable, el Legacy tiene un pipeline fijo (supongo que esto lo entenderé más adelante).

### ¿Que es el shader program? ¿Por que es importante en OpenGL moderno?
Es el programa que combina los shaders y le dice a la GPU como procesar vertices y pixeles. Es vital porque en OpenGL moderno todo el dibujo depende de estos programas, no hay funciones fijas para hacerlo.

### ¿Que crees que hace setupTriangle()? ¿Que es el VAO y el VBO?
setupTriangle() probablemente crea los buffers y configura la informacion del triangulo para que se pueda dibujar. El VBO guarda los datos de los vertices, y el VAO guarda la configuracion que indica como leer esos datos.

### ¿Si se usa el shader y VAO antes del loop es necesario repetirlo? ¿En que casos seria util hacerlo?
No es necesario repetirlo si no cambian, pero puede ser util si se usan varios shaders, varios objetos o si una funcion externa cambia el estado y quieres asegurarte de que todo siga correcto.

### ¿Por que es importante glfwSwapBuffers()? ¿Que pasa si no se llama?
Cambia el buffer donde se dibujo por el que se muestra en pantalla. Si no se llama, la imagen nunca se actualiza y la ventana se queda congelada o negra, porque OpenGL solo dibujo en memoria sin mostrarlo.

## CPU y GPU

la CPU hace pocas taras pero muy complejas mientras que la GPU se encarga de multiples tareas, una gran variedad, sin embargo son simples, pero las hace al mismo tiempo.

### ¿Cuáles son los tres pasos claves del pipeline de OpenGL?
Transformación, rasterización y shading. Transformación convierte coordenadas a espacio de pantalla, rasterización convierte figuras en fragmentos, y shading calcula color y efectos visuales.

### ¿Qué significa el pipeline programable?
Que ahora el programador puede definir como se procesan vértices y fragmentos usando shaders, en lugar de depender de funciones fijas de OpenGL

¿Qué diferencia hay entre el pipeline fijo y el programable?
El fijo usaba rutinas predefinidas por OpenGL; el programable permite personalizar el proceso con shaders escritos por el usuario

### ¿Qué ventajas le ves a esto?
Mayor control, flexibilidad y posibilidad de crear efectos visuales avanzados o estilos únicos
### Si el pipeline es programable, ¿Qué tengo que programar?
Principalmente el vertex shader y el fragment shader, aunque se pueden usar más etapas como geometry o compute shaders
### Si fueras a describir el proceso de rasterización, ¿Qué dirías?
Convierte las primitivas (como triángulos) en fragmentos que luego se transforman en píxeles en pantalla

### ¿Qué son los fragmentos? ¿Es lo mismo un fragmento que un pixel? ¿Por qué?
Un fragmento es un candidato a pixel, con datos como color y profundidad, solo se convierte en pixel si pasa las pruebas del pipeline (como el depth test)

### Explica qué problema resuelve el Z-buffer y qué es el depth test.
El Z-buffer guarda la profundidad de cada fragmento, el depth test decide si un fragmento debe verse o quedar oculto detrAs de otro

### ¿Por qué se presenta el problema del aliasing? ¿Qué es el anti-aliasing?
El aliasing ocurre por la baja resolucion al dibujar lineas o bordes, el anti-aliasing suaviza esos bordes mezclando colores cercanos

### ¿Qué relación hay entre la iluminación y el fragment shader?
El fragment shader puede calcular la luz sobre cada fragmento. No es obligatorio usar iluminación, pero si no se usa, la escena se verá plana o sin volumen

### ¿Qué implica para la GPU que una aplicación tenga múltiples fuentes de iluminación?
Mas calculos por fragmento, lo que aumenta la carga de procesamiento y puede reducir el rendimiento

### Dibujar un triangulo en OpenGL: 
crear ventana y contexto OpenGL, cargar los vertices del triangulo en un VBO y describirlos con un VAO; escribir y 
compilar vertex y fragment shader; enlazar el shader program; configurar viewport; en el loop, limpiar pantalla, usar el programa, ligar el VAO y llamar glDrawArrays.

Usar un shader en OpenGL: escribir el codigo GLSL (vertex y fragment), compilar cada shader y revisar errores, enlazarlos en un shader program, obtener locations de atributos y uniforms, definir atributos con glVertexAttribPointer y pasar valores con glUniform, luego glUseProgram antes de dibujar

<img width="381" height="438" alt="image" src="https://github.com/user-attachments/assets/5cdee12a-0abe-44d7-96dc-1b37fc0abeb8" />

<a name = "actividad5"> </a>

# Actividad 5
### Modifica el código del triángulo para que sea interactivo.
### Incluye una captura de pantalla del triángulo interactivo funcionando en tu máquina.


<img width="171" height="249" alt="image" src="https://github.com/user-attachments/assets/635da914-0d9a-44bd-b915-6759541974d9" />
<img width="201" height="193" alt="image" src="https://github.com/user-attachments/assets/0f251408-6a9f-42d0-9473-4db05d90ff16" />
<img width="255" height="170" alt="image" src="https://github.com/user-attachments/assets/8f4f777b-4fdc-4efb-bcac-67a936f34a9f" />
<img width="253" height="186" alt="image" src="https://github.com/user-attachments/assets/6959a10c-8d0e-4ab3-ae91-884886a3b122" />


### Explica el proceso de normalización de las coordenadas del mouse y cómo se relaciona con el sistema de coordenadas de OpenGL
El mouse entrega pixeles con origen arriba izquierda, primero convierto mx y my a rango cero a uno dividiendo por ancho y alto, luego paso a NDC e invierto el eje y con las reglas x ndc igual mx dividido por ancho por dos menos uno y ndc igual uno menos my dividido por alto por dos, asi el sistema queda centrado y esos valores se pueden usar como uniform para color u offset

### Explica el proceso de normalización a coordenadas de dispositivo (NDC) y cómo se relaciona con el sistema de coordenadas de OpenGL
Tras las transformaciones de modelo vista proyeccion y la division por w los vertices quedan en el cubo de menos uno a mas uno en x y z, lo que esta dentro se rasteriza y el viewport lo mapea a pixeles de pantalla mientras lo que queda fuera se recorta

<a name = "actividad6"> </a>

# Actividad 6

<img width="253" height="227" alt="image" src="https://github.com/user-attachments/assets/4d37fed9-e723-4c71-a405-757f51ba73b3" />
<img width="265" height="285" alt="image" src="https://github.com/user-attachments/assets/076c63c8-aeae-4bcc-8ecd-6f9d57e1c474" />

### Basicamente cambia de tamaño segun que tan a la derecha o a la izquierda este el triangulo

Explica como usaste la funcion de tiempo para el color ciclico, que rango produce y como afecta el color final
Uso t igual glfwGetTime dentro del loop y aplico 0.5 mas 0.5 por sin de t para cada canal con frecuencias y fases distintas, sin produce valores entre menos uno y uno y al escalar queda entre cero y uno, esos valores alimentan ourColor y generan un cambio suave y repetitivo en rgb

### Describe brevemente los cambios que realizaste en el codigo C++ donde obtienes el tiempo, como y donde actualizas el uniform

Obtengo el tiempo con glfwGetTime en el loop principal, calculo rgb con funciones sin usando t y fases distintas, obtengo la location de ourColor con glGetUniformLocation y actualizo cada frame con glUniform4f antes de dibujar

``` C++
#include <iostream>
#include <cmath>
#include <glad/glad.h>
#include <GLFW/glfw3.h>


// Callback: ajusta el viewport cuando cambie el tamaño de la ventana
void framebuffer_size_callback(GLFWwindow* window, int width, int height) {
	glViewport(0, 0, width, height);
}

// Procesa entrada simple: cierra con ESC
void processInput(GLFWwindow* window) {
	if (glfwGetKey(window, GLFW_KEY_ESCAPE) == GLFW_PRESS)
		glfwSetWindowShouldClose(window, true);
}

// Tamaño de las ventanas
const unsigned int SCR_WIDTH = 400;
const unsigned int SCR_HEIGHT = 400;

// Fuentes de los shaders
const char* vertexShaderSrc = R"glsl(
    #version 460 core
    layout(location = 0) in vec3 aPos;
    uniform vec2 offset;
    uniform float uScale;
    void main() {
        vec3 newPos = aPos * uScale;
        newPos.x += offset.x;
        newPos.y += offset.y;
        gl_Position = vec4(newPos, 1.0);
    }
)glsl";

const char* fragmentShaderSrc = R"glsl(
    #version 460 core
    out vec4 FragColor;
    uniform vec4 ourColor;
    void main() {
        FragColor = ourColor;
    }
)glsl";

// IDs globales
unsigned int VAO, VBO;
unsigned int shaderProg;

// Compila y linkea un programa de shaders, retorna su ID
unsigned int buildShaderProgram() {
	int success;
	char log[512];

	unsigned int vs = glCreateShader(GL_VERTEX_SHADER);
	glShaderSource(vs, 1, &vertexShaderSrc, nullptr);
	glCompileShader(vs);
	glGetShaderiv(vs, GL_COMPILE_STATUS, &success);
	if (!success) {
		glGetShaderInfoLog(vs, 512, nullptr, log);
		std::cerr << "ERROR VERTEX SHADER:\n" << log << "\n";
	}

	unsigned int fs = glCreateShader(GL_FRAGMENT_SHADER);
	glShaderSource(fs, 1, &fragmentShaderSrc, nullptr);
	glCompileShader(fs);
	glGetShaderiv(fs, GL_COMPILE_STATUS, &success);
	if (!success) {
		glGetShaderInfoLog(fs, 512, nullptr, log);
		std::cerr << "ERROR FRAGMENT SHADER:\n" << log << "\n";
	}

	unsigned int prog = glCreateProgram();
	glAttachShader(prog, vs);
	glAttachShader(prog, fs);
	glLinkProgram(prog);
	glGetProgramiv(prog, GL_LINK_STATUS, &success);
	if (!success) {
		glGetProgramInfoLog(prog, 512, nullptr, log);
		std::cerr << "ERROR LINKING PROGRAM:\n" << log << "\n";
	}

	glDeleteShader(vs);
	glDeleteShader(fs);
	return prog;
}

// Crea un VAO/VBO con los datos de un triángulo
void setupTriangle() {
	float vertices[] = {
		-0.5f, -0.5f, 0.0f,
		 0.5f, -0.5f, 0.0f,
		 0.0f,  0.5f, 0.0f
	};
	glGenVertexArrays(1, &VAO);
	glGenBuffers(1, &VBO);

	glBindVertexArray(VAO);
	glBindBuffer(GL_ARRAY_BUFFER, VBO);
	glBufferData(GL_ARRAY_BUFFER, sizeof(vertices), vertices, GL_STATIC_DRAW);
	glVertexAttribPointer(0, 3, GL_FLOAT, GL_FALSE, 3 * sizeof(float), (void*)0);
	glEnableVertexAttribArray(0);
	glBindVertexArray(0);
}


int main()
{
	// 1) Inicializar GLFW
	if (!glfwInit()) {
		std::cerr << "Fallo al inicializar GLFW\n";
		return -1;
	}
	glfwWindowHint(GLFW_CONTEXT_VERSION_MAJOR, 4);
	glfwWindowHint(GLFW_CONTEXT_VERSION_MINOR, 6);
	glfwWindowHint(GLFW_OPENGL_PROFILE, GLFW_OPENGL_CORE_PROFILE);

	// 2) Crear ventana
	GLFWwindow* mainWindow = glfwCreateWindow(SCR_WIDTH, SCR_HEIGHT, "Ventana", nullptr, nullptr);
	if (!mainWindow) {
		std::cerr << "Error creando ventana1\n";
		glfwTerminate();
		return -1;
	}

	// 3) Lee el tamaño del framebuffer
	int bufferWidth, bufferHeight;
	glfwGetFramebufferSize(mainWindow, &bufferWidth, &bufferHeight);

	// 4) Callbacks 
	glfwSetFramebufferSizeCallback(mainWindow, framebuffer_size_callback);


	// 5) Cargar GLAD y recursos en contexto de window1
	glfwMakeContextCurrent(mainWindow);

	if (!gladLoadGLLoader((GLADloadproc)glfwGetProcAddress)) {
		std::cerr << "Fallo al cargar GLAD (contexto1)\n";
		return -1;
	}

	// 6) Habilita el V-Sync
	glfwSwapInterval(1);

	// 7) Compila y linkea shaders
	shaderProg = buildShaderProgram();

	// 8) Genera el contenido a mostrar
	setupTriangle();

	// 9) Configura el viewport
	glViewport(0, 0, bufferWidth, bufferHeight);


	// 10) Loop principal
	while (!glfwWindowShouldClose(mainWindow))
	{
		// 11) Manejo de eventos
		glfwPollEvents();


		// 12) Procesa la entrada
		processInput(mainWindow);

		// 13) Configura el color de fondo y limpia el framebuffer
		glClearColor(0.2f, 0.3f, 0.3f, 1.0f);
		glClear(GL_COLOR_BUFFER_BIT);

		// 14) Indica a OpenGL que use el shader program
		glUseProgram(shaderProg);
		int offsetLocation = glGetUniformLocation(shaderProg, "offset");
		int colorLocation = glGetUniformLocation(shaderProg, "ourColor");
		int scaleLocation = glGetUniformLocation(shaderProg, "uScale");

		// 15) Activa el VAO y dibuja el triángulo
		double xpos, ypos;
		glfwGetCursorPos(mainWindow, &xpos, &ypos);

		float x = (float)xpos / (float)SCR_WIDTH;
		x < 0 ? x = 0 : x;
		x > 1 ? x = 1 : x;

		float y = (float)ypos / (float)SCR_HEIGHT;
		y < 0 ? y = 0 : y;
		y > 1 ? y = 1 : y;

		float t = (float)glfwGetTime();
		float r = 0.5f + 0.5f * std::sin(t * 1.0f);
		float g = 0.5f + 0.5f * std::sin(t * 1.3f + 1.0f);
		float b = 0.5f + 0.5f * std::sin(t * 1.7f + 2.0f);
		glUniform4f(colorLocation, r, g, b, 1.0f);

		glUniform2f(offsetLocation, x * 2 - 1, 1 - y * 2);

		float scale = 0.5f + x;
		glUniform1f(scaleLocation, scale);

		glBindVertexArray(VAO);
		glDrawArrays(GL_TRIANGLES, 0, 3);

		// 16) Intercambia buffers y muestra el contenido
		glfwSwapBuffers(mainWindow);
	}

	// 17) Limpieza
	glfwMakeContextCurrent(mainWindow);
	glDeleteVertexArrays(1, &VAO);
	glDeleteBuffers(1, &VBO);
	glDeleteProgram(shaderProg);

	glfwDestroyWindow(mainWindow);
	glfwTerminate();
	return 0;
}


```

# Autoevaluacion

1: [evidencias](#actividad1)
2:[evidencias](#actividad2)
3:[evidencias](#actividad3)
4:[evidencias](#actividad4)
5:[evidencias](#actividad5)
6:[evidencias](#actividad6)

nota: 5








