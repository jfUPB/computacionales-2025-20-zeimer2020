# Bitácora de aprendizaje de la unidad 5

## 1.  **Diagnóstico inicial**

¿Qué es el encapsulamiento para ti? Describe una situación en la que te haya sido útil o donde hayas visto su importancia.

- restriccion que posee una variable o un metodo, por ejemplo cuando usabamos variables en escenarios concretos y solo queriamos usarlas en esos momentos especificos

¿Qué es la herencia? ¿Por qué un programador decidiría usarla? Da un ejemplo simple.

- herencia es cuando hacemos que una clase herede todas las caractreristicas de otra clase, haciendo que sea dueña tmb de todo atributo de la otra clase, por ejemplo si hacemos que la clase perro herede de la clase animal terrestre


¿Qué es el polimorfismo? Describe con tus palabras qué significa que un código sea “polimórfico”.

- cuando en clases tenemos el mismo metodo pero se definen de diferentes maneras entonces como tal hacen cosas distintas

#### parte 2

``` C#

using System;
using System.Collections.Generic;

public abstract class Figura
{
    private string nombre;

    public string Nombre
    {
        get { return nombre; }
        protected set { nombre = value; }
    }

    public Figura(string nombre)
    {
        this.Nombre = nombre;
    }

    public abstract void Dibujar();
}

public class Circulo : Figura
{
    public double Radio { get; private set; }

    public Circulo(double radio) : base("Círculo")
    {
        this.Radio = radio;
    }

    public override void Dibujar()
    {
        Console.WriteLine($"Dibujando un {Nombre} de radio {Radio}.");
    }
}

public class Rectangulo : Figura
{
    public double Base { get; private set; }
    public double Altura { get; private set; }

    public Rectangulo(double b, double h) : base("Rectángulo")
    {
        this.Base = b;
        this.Altura = h;
    }

    public override void Dibujar()
    {
        Console.WriteLine($"Dibujando un {Nombre} de {Base}x{Altura}.");
    }
}

public class Programa
{
    public static void Main()
    {
        List<Figura> misFiguras = new List<Figura>();

        misFiguras.Add(new Circulo(5.0));
        misFiguras.Add(new Rectangulo(4.0, 6.0));
        misFiguras.Add(new Circulo(10.0));

        foreach (Figura fig in misFiguras)
        {
            fig.Dibujar();
        }
    }
}
```
Encapsulamiento:

Señala una línea de código que sea un ejemplo claro de encapsulamiento y explica por qué lo es.

- `public abstract class Figura` debido a la palabra public se sabe que cualquier parte del codigo puede acceder a la clase, dandole un encapsulamiento publico

¿Por qué crees que el campo nombre es private pero la propiedad Nombre es public? ¿Qué problema se evita con esto?
Herencia:

- debido a los metodos accesores, esto permite entrar en variables privadas sin comprometer el encapsulamiento, evitando modificaciones indeseadas

¿Cómo se evidencia la herencia en la clase Circulo?

- se puede evidenciar al ver que circulo posee los atributos al ver `public class Circulo : Figura`

Un objeto de tipo Circulo, además de Radio, ¿Qué otros datos almacena en su interior gracias a la herencia?
Polimorfismo:

Observa el bucle foreach. La variable fig es de tipo Figura, pero a veces contiene un Circulo y otras un Rectangulo. Cuando se llama a fig.Dibujar(), el programa ejecuta la versión correcta. En tu opinión, ¿Cómo crees que funciona esto “por debajo”? No necesitas saber la respuesta correcta, solo quiero que intentes razonar cómo podría ser.

- el metodo `Dibujar()` es abstraco lo que significa que no tiene funcion exacta, debido a esto se comportara distinto segun que figura lo este usando, debido a esto cuando diga que dibujara un cuadrado lo hara correctamente con su lado y lado, con el rectangulo la base por la altura y el circulo el radio

#### parte 3

Memoria y herencia: cuando creas un objeto Rectangulo, este tiene Base, Altura y también Nombre. ¿Cómo te imaginas que se organizan esos tres datos en la memoria del computador para formar un solo objeto?

se guardan los datos del objeto en un espacio en la memoria exclusivo para ese objeto, cuando se crea el objeto a su vez se crea el espacio para estos datos


El mecanismo del polimorfismo: pensemos de nuevo en la llamada fig.Dibujar(). El compilador solo sabe que fig es una Figura. ¿Cómo decide el programa, mientras se está ejecutando, si debe llamar al Dibujar del Circulo o al del Rectangulo? Lanza algunas ideas o hipótesis.

- verifica como se asignan los valores a cada figura y de ahi empieza a "dibujar" cada figura con sus respectivos valores

La barrera del encapsulamiento: ¿Cómo crees que el compilador logra que no puedas acceder a un miembro private desde fuera de la clase? ¿Es algo que se revisa cuando escribes el código, o es una protección que existe mientras el programa se ejecuta? ¿Por qué piensas eso?

- es una verificacion que se realiza segun lo que uno escriba en el programa y lo que se lea en el codigo una vez comppilado, eso teniendo en cuenta si colocamos private o public

#### Actividada 2

<img width="914" height="587" alt="image" src="https://github.com/user-attachments/assets/47d3afc4-831e-4518-9409-b19b0e437fcb" />
<img width="975" height="676" alt="image" src="https://github.com/user-attachments/assets/aa8b3e36-e9c9-474b-9cf3-a5e272217003" />

#### Actividad 3

Hipotesis del depurado: que me muestre los procesos actuales ocurriendo por la ejecucion del codigo
resultado: en efecto, paso eso, pero con subprocesos tambien
<img width="446" height="139" alt="image" src="https://github.com/user-attachments/assets/77f00787-79e4-448c-8f32-c51ec0c1d826" />

<img width="497" height="371" alt="image" src="https://github.com/user-attachments/assets/5403ef22-941e-4323-aff3-7bc5cb9f6a95" />


## 3.  **Registro de exploración:** 

### registro de informacion

el encapsulamiento que es:
es basicamente una forma en la que podemos ocultar datos y solo permitir su acceso mediante metodos, acciones o propiedades controladas, esto con la idea de que no se modifiquen de manera accidental o que ocurran errores con repecto a la identidad o valor de los datos almacenados.

la relacion entre los metodos virtuales y el polimorfismo es que los metodos virtuales son aquellos que permiten implementar el polmorfismo, esto permite que un mismo metodo se ejecute de manera distinta al ser invocado o llamado por asi decirlo

para implementar herencia solo colocamos : delante de una clase y asi esta clase heredara las caracteristicas de la clase que sigue de los :, esto ayuda para ahorrar tiempo y espacio en el codigo, util tambien para implementar polimorfismo

la herencia multiple se crea cuando despues de los : colocas mas de una clase, separadas por comas, asi ahorrar aun mas espacio

#### como colocar patciles? (empiezan el ensayo y error del apply)

para agregar nuevas particulas necesito crear una clase que herede de Particle, implementar sus metodos de update, draw y el isDead, ya luego instanciarla dentro de createRisingParticle o en cualquier evento donde quieras generarla

#### como generar tipos de explosiones

para anadir nuevos metodos de explosion, tengo que crear una clase que herede de ExplosionParticle, definir su logica de movimiento y dibujo, y sumarla en el switch/if de ofApp::update donde se eligen los tipos de explosion.

primer intento:
<img width="678" height="488" alt="image" src="https://github.com/user-attachments/assets/37bbfb63-e8fd-4cf9-b61b-a14c08a38627" />
intente hacer una explosion en espiral pero me fallo colocar la ubicacion entonces ahi se ven abajito el nuevo tipo de explosion


segundo intento, me di cuenta de que se me estaba olvidando hacer explotar los espirales, aunq opte por colocar toda la ejecucion del programa en la mitad de la pantalla
 <img width="804" height="390" alt="image" src="https://github.com/user-attachments/assets/f6f25818-157c-4257-87bc-06b1578a6010" />


tercer intento, esta vez coloque dos particulas nuevas como version final en las cuales una de ellas rebota por la pantalla, la otra da vueltas en espiral en el punto de origen y el nuevo tipo de explosion es en la que se desintegra en bolitas chiquitas 
<img width="1008" height="622" alt="image" src="https://github.com/user-attachments/assets/0279a75f-b1c0-4261-b6a7-d8b7b060f5c7" />


aca pueden verse los tipos de particulas, las mas cercanas a los bordes son las que rebotan, las de la mitad dan vueltas en espiral y las demas son las normales
<img width="994" height="660" alt="image" src="https://github.com/user-attachments/assets/6835341d-ecb1-4f26-aff4-4a966803e4a7" />
aca se puede ver el nuevo tipo de explosion
<img width="573" height="548" alt="image" src="https://github.com/user-attachments/assets/e6f5e0de-b4a3-4381-9a11-7755e55743f5" />


## 4.  **Consolidación, autoevaluación y cierre:**
> [!CAUTION]
> Esta sección es OBLIGATORIA y central para tu evaluación

pues consideraria que 4,5 ya que no pude entener algunos conceptos y tuve que buscarlos directamente en internet, aunq puede hacerle varias modificaciones al codigo  tuve que tomar registro y sentarme a pensar en que me estaba equivocando, pedi ayuda a la IA para saber que era lo que estaba haciendo mal y asi poder sacar la "version final" 


codigo final

``` c++ .h
#pragma once
#include "ofMain.h"
#include <vector>

// -------------------------------------------------
// Clase base abstracta: Particle
// -------------------------------------------------
class Particle {
public:
	virtual ~Particle() { }
	virtual void update(float dt) = 0;
	virtual void draw() = 0;
	virtual bool isDead() const = 0;
	virtual bool shouldExplode() const { return false; }
	virtual glm::vec2 getPosition() const { return glm::vec2(0, 0); }
	virtual ofColor getColor() const { return ofColor(255); }
};

// -------------------------------------------------
// RisingParticle
// -------------------------------------------------
class RisingParticle : public Particle {
protected:
	glm::vec2 position;
	glm::vec2 velocity;
	ofColor color;
	float lifetime;
	float age;
	bool exploded;

public:
	RisingParticle(const glm::vec2 & pos, const glm::vec2 & vel, const ofColor & col, float life)
		: position(pos)
		, velocity(vel)
		, color(col)
		, lifetime(life)
		, age(0)
		, exploded(false) {
	}

	void update(float dt) override {
		position += velocity * dt;
		age += dt;
		velocity.y += 9.8f * dt * 8;
		float explosionThreshold = ofGetHeight() * 0.15 + ofRandom(-30, 30);
		if (position.y <= explosionThreshold || age >= lifetime) {
			exploded = true;
		}
	}

	void draw() override {
		ofSetColor(color);
		ofDrawCircle(position, 10);
	}

	bool isDead() const override { return exploded; }
	bool shouldExplode() const override { return exploded; }
	glm::vec2 getPosition() const override { return position; }
	ofColor getColor() const override { return color; }
};

// -------------------------------------------------
// SpiralParticle
// -------------------------------------------------
class SpiralParticle : public Particle {
private:
	glm::vec2 position;
	float angle;
	float radius;
	float angularSpeed;
	float radialSpeed;
	ofColor color;
	float age, lifetime;
	bool exploded;

public:
	SpiralParticle(const glm::vec2 & pos, const ofColor & col)
		: position(pos)
		, angle(ofRandom(TWO_PI))
		, radius(0)
		, angularSpeed(ofRandom(3, 6))
		, radialSpeed(ofRandom(50, 100))
		, color(col)
		, age(0)
		, lifetime(ofRandom(2, 3))
		, exploded(false) { }

	void update(float dt) override {
		age += dt;
		radius += radialSpeed * dt;
		angle += angularSpeed * dt;
		position.x += cos(angle) * radius * dt;
		position.y += sin(angle) * radius * dt;
		color.a = ofMap(age, 0, lifetime, 255, 0, true);

		if (age >= lifetime) {
			exploded = true;
		}
	}

	void draw() override {
		ofSetColor(color);
		ofDrawCircle(position, 6);
	}

	bool isDead() const override { return exploded; }
	bool shouldExplode() const override { return exploded; }
	glm::vec2 getPosition() const override { return position; }
	ofColor getColor() const override { return color; }
};

// -------------------------------------------------
// BouncingParticle
// -------------------------------------------------
class BouncingParticle : public Particle {
private:
	glm::vec2 position;
	glm::vec2 velocity;
	ofColor color;
	float age, lifetime;
	bool exploded;

public:
	BouncingParticle(const glm::vec2 & pos, const glm::vec2 & vel, const ofColor & col)
		: position(pos)
		, velocity(vel)
		, color(col)
		, age(0)
		, lifetime(ofRandom(2, 4))
		, exploded(false) { }

	void update(float dt) override {
		position += velocity * dt;
		age += dt;

		// Rebote en los bordes de la ventana
		if (position.x <= 0 || position.x >= ofGetWidth()) velocity.x *= -1;
		if (position.y <= 0 || position.y >= ofGetHeight()) velocity.y *= -1;

		if (age >= lifetime) {
			exploded = true;
		}
	}

	void draw() override {
		ofSetColor(color);
		ofDrawRectangle(position, 8, 8);
	}

	bool isDead() const override { return exploded; }
	bool shouldExplode() const override { return exploded; }
	glm::vec2 getPosition() const override { return position; }
	ofColor getColor() const override { return color; }
};

// -------------------------------------------------
// ExplosionParticle (base)
// -------------------------------------------------
class ExplosionParticle : public Particle {
protected:
	glm::vec2 position;
	glm::vec2 velocity;
	ofColor color;
	float age;
	float lifetime;
	float size;

public:
	ExplosionParticle(const glm::vec2 & pos, const glm::vec2 & vel, const ofColor & col, float life, float sz)
		: position(pos)
		, velocity(vel)
		, color(col)
		, age(0)
		, lifetime(life)
		, size(sz) {
	}

	void update(float dt) override {
		position += velocity * dt;
		age += dt;
		float alpha = ofMap(age, 0, lifetime, 255, 0, true);
		color.a = alpha;
	}

	bool isDead() const override { return age >= lifetime; }
};

// -------------------------------------------------
// CircularExplosion
// -------------------------------------------------
class CircularExplosion : public ExplosionParticle {
public:
	CircularExplosion(const glm::vec2 & pos, const ofColor & col)
		: ExplosionParticle(pos, glm::vec2(0, 0), col, 1.2f, ofRandom(16, 32)) {
		float angle = ofRandom(0, TWO_PI);
		float speed = ofRandom(80, 200);
		velocity = glm::vec2(cos(angle), sin(angle)) * speed;
	}

	void draw() override {
		ofSetColor(color);
		ofDrawCircle(position, size);
	}
};

// -------------------------------------------------
// RandomExplosion
// -------------------------------------------------
class RandomExplosion : public ExplosionParticle {
public:
	RandomExplosion(const glm::vec2 & pos, const ofColor & col)
		: ExplosionParticle(pos, glm::vec2(0, 0), col, 1.5f, ofRandom(16, 32)) {
		velocity = glm::vec2(ofRandom(-200, 200), ofRandom(-200, 200));
	}

	void draw() override {
		ofSetColor(color);
		ofDrawRectangle(position.x, position.y, size, size);
	}
};

// -------------------------------------------------
// StarExplosion
// -------------------------------------------------
class StarExplosion : public ExplosionParticle {
public:
	StarExplosion(const glm::vec2 & pos, const ofColor & col)
		: ExplosionParticle(pos, glm::vec2(0, 0), col, 1.3f, ofRandom(20, 40)) {
		float angle = ofRandom(0, TWO_PI);
		float speed = ofRandom(90, 180);
		velocity = glm::vec2(cos(angle), sin(angle)) * speed;
	}

	void draw() override {
		ofSetColor(color);
		int rays = 5;
		float outerRadius = size;
		float innerRadius = size * 0.5;
		ofPushMatrix();
		ofTranslate(position);
		for (int i = 0; i < rays; i++) {
			float theta = ofMap(i, 0, rays, 0, TWO_PI);
			float xOuter = cos(theta) * outerRadius;
			float yOuter = sin(theta) * outerRadius;
			float xInner = cos(theta + PI / rays) * innerRadius;
			float yInner = sin(theta + PI / rays) * innerRadius;
			ofDrawLine(0, 0, xOuter, yOuter);
			ofDrawLine(xOuter, yOuter, xInner, yInner);
		}
		ofPopMatrix();
	}
};

// -------------------------------------------------
// DisintegrationExplosion (nuevo modo)
// -------------------------------------------------
class DisintegrationExplosion : public ExplosionParticle {
public:
	DisintegrationExplosion(const glm::vec2 & pos, const ofColor & col)
		: ExplosionParticle(pos, glm::vec2(0, 0), col, 0.8f, ofRandom(2, 6)) {
		velocity = glm::vec2(ofRandom(-300, 300), ofRandom(-300, 300));
	}

	void draw() override {
		ofSetColor(color);
		ofDrawCircle(position, size);
	}
};

// -------------------------------------------------
// ofApp
// -------------------------------------------------
class ofApp : public ofBaseApp {
public:
	void setup();
	void update();
	void draw();
	void mousePressed(int x, int y, int button);
	void keyPressed(int key);

	std::vector<Particle *> particles;
	~ofApp();

private:
	void createRisingParticle();
};
```

```c++ cpp
#include "ofApp.h"

// --------------------------------------------------------------
void ofApp::setup() {
	ofSetFrameRate(60);
	ofBackground(0);
}

// --------------------------------------------------------------
void ofApp::update() {
	float dt = ofGetLastFrameTime();

	for (int i = 0; i < particles.size(); i++) {
		particles[i]->update(dt);
	}

	for (int i = particles.size() - 1; i >= 0; i--) {
		if (particles[i]->shouldExplode()) {
			int explosionType = (int)ofRandom(4); // ahora hay 4 tipos
			int numParticles = (int)ofRandom(20, 30);
			for (int j = 0; j < numParticles; j++) {
				if (explosionType == 0) {
					particles.push_back(new CircularExplosion(particles[i]->getPosition(), particles[i]->getColor()));
				} else if (explosionType == 1) {
					particles.push_back(new RandomExplosion(particles[i]->getPosition(), particles[i]->getColor()));
				} else if (explosionType == 2) {
					particles.push_back(new StarExplosion(particles[i]->getPosition(), particles[i]->getColor()));
				} else {
					particles.push_back(new DisintegrationExplosion(particles[i]->getPosition(), particles[i]->getColor()));
				}
			}
			delete particles[i];
			particles.erase(particles.begin() + i);
		} else if (particles[i]->isDead()) {
			delete particles[i];
			particles.erase(particles.begin() + i);
		}
	}
}

// --------------------------------------------------------------
void ofApp::draw() {
	for (int i = 0; i < particles.size(); i++) {
		particles[i]->draw();
	}
}

// --------------------------------------------------------------
void ofApp::createRisingParticle() {
	// Generar desde la mitad de la pantalla
	float minX = ofGetWidth() * 0.35;
	float maxX = ofGetWidth() * 0.65;
	float spawnX = ofRandom(minX, maxX);
	glm::vec2 pos(spawnX, ofGetHeight() * 0.5);

	glm::vec2 target(ofGetWidth() / 2 + ofRandom(-300, 300), ofGetHeight() * 0.10 + ofRandom(-30, 30));
	glm::vec2 direction = glm::normalize(target - pos);
	glm::vec2 vel = direction * ofRandom(250, 350);

	ofColor col;
	col.setHsb(ofRandom(255), 220, 255);
	float lifetime = ofRandom(1.5, 3.5);

	float choice = ofRandom(1.0);
	if (choice < 0.5) {
		particles.push_back(new RisingParticle(pos, vel, col, lifetime));
	} else if (choice < 0.75) {
		particles.push_back(new SpiralParticle(pos, col));
	} else {
		particles.push_back(new BouncingParticle(pos, vel, col));
	}
}

// --------------------------------------------------------------
void ofApp::mousePressed(int x, int y, int button) {
	createRisingParticle();
}

// --------------------------------------------------------------
void ofApp::keyPressed(int key) {
	if (key == ' ') {
		for (int i = 0; i < 1000; i++) {
			createRisingParticle();
		}
	}
	if (key == 's') {
		ofSaveScreen("screenshot_" + ofToString(ofGetFrameNum()) + ".png");
	}
}

// --------------------------------------------------------------
ofApp::~ofApp() {
	for (int i = 0; i < particles.size(); i++) {
		delete particles[i];
	}
	particles.clear();
}
```
