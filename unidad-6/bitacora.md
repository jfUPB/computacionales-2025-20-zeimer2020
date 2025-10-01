# Bitácora de aprendizaje de la unidad 6


### seek 
funcionamiento del programa:

# Actividad 1

##### ¿Cómo puedes interactuar con la aplicación? Menciona específicamente las teclas y qué efecto parecen tener sobre las partículas.

me permite realizar acciones como atraer las particulas con la A, alejarlas con la R, paralizarlas con la S y volver a la normalidad son la S, las funciones de atraccion y repeler se guian del mouse


##### ¿Observas los diferentes tipos de “partículas”? ¿Se comportan todas igual inicialmente?

no, cada una se comporta de manera diferente, las verdes son las mas rapidas, las rojas van a velocidad media y las azules son las mas lentas

##### Toma algunas capturas de pantalla de la aplicación en diferentes momentos (estado inicial, después de presionar ‘a’, ‘r’, ‘s’, ‘n’) y añádelas a tu bitácora.

Atraer
<img width="533" height="472" alt="image" src="https://github.com/user-attachments/assets/73d4907c-57e4-4dea-8de1-64fc5863b380" />
Nornal
<img width="980" height="617" alt="image" src="https://github.com/user-attachments/assets/0696f30f-c391-4ae8-95a7-3368c35c98e8" />
Stop despues de Repeler
<img width="993" height="571" alt="image" src="https://github.com/user-attachments/assets/1cbfd4c7-7f0a-4788-ab91-f374dc4cc37a" />

##### ¿Qué crees que está pasando “detrás de cámaras” cuando presionas las teclas? Formula una hipótesis inicial sobre cómo la aplicación cambia el comportamiento de las partículas.

cada vez que pulsamos una tecla llamamos un metodo o algun sector del codigo que modifica el comportamiento de las particulas, o tambien siplemente tenemos varios comportamientos y se activan una vez que pulsamos las diferentes teclas al momento de ejectuar el programa


Los observers lo que hacen es actualizarse cuando un objeto especifico cambia, por ejemplo tenemos una particula, si esa particula cambia y esta vinculada a los observers, todos estos se actualizaran en funcion del cambio realizado

# Actividad 2

Explica con tus propias palabras el propósito del patrón Observer. ¿Qué problema resuelve?
Dicho patron se encarga de usar o mas bien introducir polimorfismo, dejando que otras clasese que serian los observadores esten ahi tecnicamente suscritos (como dices en el ejemplo del github) a la clase que sea sujeto

Dibuja un diagrama que muestre la relación entre Subject, Observer, ofApp y Particle en el caso de estudio, indicando quién es el Sujeto y quiénes los Observadores.
<img width="721" height="619" alt="image" src="https://github.com/user-attachments/assets/ec60b1bc-7434-4a80-a919-a2ddb153114e" />


¿Qué ventajas crees que ofrece usar el patrón Observer en esta aplicación en comparación con, por ejemplo, que ofApp::update recorriera todas las partículas y les dijera directamente que cambien su comportamiento basado en una variable global? Piensa en términos de acoplamiento y extensibilidad.

Usar el patrón Observer reduce el acoplamiento porque las partIculas no dependen directamente de una variable global ni de que ofApp::update las controle, sino que reaccionan a notificaciones de un sujeto; esto facilita la extensibilidad, ya que se pueden añadir nuevos tipos de partIculas u observadores sin cambiar la lOgica central, manteniendo el cOdigo más limpio, modular y fAcil de mantener.

# Actividad 3 

##### Explica con tus propias palabras el propósito del patrón Factory Method (o Simple Factory, en este caso). ¿Qué problema principal aborda en la creación de objetos?

El Factory Method o Simple Factory sirve para separar la creacion de objetos de su uso. Evita repetir condicionales y configuraciones en todo el codigo, centralizando la logica de como se crean.

##### ¿Qué ventajas aporta el uso de ParticleFactory en ofApp::setup en comparación con instanciar y configurar las partículas directamente allí? Piensa en términos de organización del código (SRP - Single Responsibility Principle), legibilidad y facilidad para añadir nuevos tipos de partículas en el futuro.

En ofApp::setup, usar ParticleFactory hace que el metodo sea mas limpio. setup solo pide tipos de particula, y la fabrica se encarga de construirlas. Asi el codigo es mas ordenado y facil de extender.

##### Imagina que quieres añadir un nuevo tipo de partícula llamada "black_hole" que tiene tamaño grande, color negro y velocidad muy lenta. Describe los pasos que necesitarías seguir para implementar esto utilizando la ParticleFactory existente. ¿Tendrías que modificar ofApp::setup? ¿Por qué sí o por qué no?

Para agregar black_hole, creas la clase con sus valores (grande, negro, lento), la registras en la fabrica y listo. En setup no hay que cambiar la logica, solo pedir ese tipo si se quiere usar.

##### El método createParticle en el ejemplo es estático. ¿Qué implicaciones (ventajas/desventajas) tiene esto comparado con tener una instancia de ParticleFactory y un método de instancia createParticle()?.

Que createParticle sea estatico facilita llamarlo sin instancias y es mas simple. La desventaja es que limita configuracion y pruebas. Con una fabrica de instancia hay mas flexibilidad pero toca manejar el objeto.

# Actividad 4

##### Explica con tus propias palabras el propósito del patrón State. ¿Cuándo es útil aplicarlo?

El patron State sirve para manejar comportamientos diferentes de un objeto segun el estado en el que este. Es util cuando un objeto cambia de forma de actuar dinamicamente y no queremos llenar el codigo de condicionales.

##### Describe las ventajas de usar el patrón State en Particle en lugar de tener un miembro std::string estadoActual y usar un gran if/else if/else o switch dentro de Particle::update() para cambiar el comportamiento. Piensa en cohesión, extensibilidad (añadir nuevos estados) y el Principio Abierto/Cerrado (Open/Closed Principle).

Usar State en Particle es mejor que tener un string y un if/else gigante porque cada estado queda en su propia clase. Esto da mas cohesion, facilita agregar nuevos estados sin tocar los existentes (principio abierto/cerrado) y el codigo es mas limpio de leer y mantener.

##### ¿Qué responsabilidad tienen los métodos onEnter y onExit en el patrón State? Proporciona un ejemplo de por qué podrían ser útiles (incluso si no se usan mucho en todos los estados de este caso de estudio). Por ejemplo, ¿Qué podrías hacer en onEnter para AttractState o en onExit para StopState?

Los metodos onEnter y onExit se usan para definir acciones al entrar o salir de un estado. Por ejemplo, en AttractState el onEnter podria inicializar una fuerza de atraccion hacia un punto, y en StopState el onExit podria resetear la velocidad a cero antes de pasar a otro estado.

# Actividad 5

codigo 

``` el .h

#pragma once

#include "ofMain.h"
#include <string>
#include <vector>

class Observer {
public:
	virtual ~Observer() = default;
	virtual void onNotify(const std::string & event) = 0;
};

class Subject {
public:
	void addObserver(Observer * observer);
	void removeObserver(Observer * observer);

protected:
	void notify(const std::string & event);

private:
	std::vector<Observer *> observers;
};

class Particle;

class State {
public:
	virtual ~State() = default;
	virtual void update(Particle * particle) = 0;
	virtual void onEnter(Particle * particle) { }
	virtual void onExit(Particle * particle) { }
};

class Particle : public Observer {
public:
	Particle();
	~Particle() override;

	Particle(const Particle &) = delete;
	Particle & operator=(const Particle &) = delete;

	void update();
	void draw();
	void onNotify(const std::string & event) override;

	void setState(State * newState);

	ofVec2f position;
	ofVec2f velocity;
	float size;
	ofColor color;

private:
	void keepInsideWindow();
	State * state;
};

class NormalState : public State {
public:
	void update(Particle * particle) override;
	void onEnter(Particle * particle) override;
};

class AttractState : public State {
public:
	void update(Particle * particle) override;
};

class RepelState : public State {
public:
	void update(Particle * particle) override;
};

class StopState : public State {
public:
	void update(Particle * particle) override;
};

class BlackHoleState : public State {
public:
	void onEnter(Particle * particle) override;
	void update(Particle * particle) override;
};

class ParticleFactory {
public:
	static Particle * createParticle(const std::string & type);
};

class ofApp : public ofBaseApp, public Subject {
public:
	~ofApp() override;
	void setup() override;
	void update() override;
	void draw() override;
	void keyPressed(int key) override;

private:
	std::vector<Particle *> particles;
};
```

``` el .cpp
#include "ofApp.h"
#include <algorithm>

void Subject::addObserver(Observer * observer) {
	if (!observer) return;
	if (std::find(observers.begin(), observers.end(), observer) == observers.end()) {
		observers.push_back(observer);
	}
}

void Subject::removeObserver(Observer * observer) {
	if (!observer) return;
	observers.erase(std::remove(observers.begin(), observers.end(), observer), observers.end());
}

void Subject::notify(const std::string & event) {
	for (Observer * observer : observers) {
		observer->onNotify(event);
	}
}

Particle::Particle()
	: state(nullptr) {
	position = ofVec2f(ofRandomWidth(), ofRandomHeight());
	velocity = ofVec2f(ofRandom(-0.5f, 0.5f), ofRandom(-0.5f, 0.5f));
	size = ofRandom(2.0f, 5.0f);
	color = ofColor(255);

	state = new NormalState();
	state->onEnter(this);
}

Particle::~Particle() {
	if (state) {
		state->onExit(this);
		delete state;
		state = nullptr;
	}
}

void Particle::setState(State * newState) {
	if (state) {
		state->onExit(this);
		delete state;
	}
	state = newState;
	if (state) {
		state->onEnter(this);
	}
}

void Particle::update() {
	if (state) {
		state->update(this);
	}
	keepInsideWindow();
}

void Particle::draw() {
	ofPushStyle();
	ofSetColor(color);
	ofDrawCircle(position, size);
	ofPopStyle();
}

void Particle::onNotify(const std::string & event) {
	if (event == "attract") {
		setState(new AttractState());
	} else if (event == "repel") {
		setState(new RepelState());
	} else if (event == "stop") {
		setState(new StopState());
	} else if (event == "normal") {
		setState(new NormalState());
	}
}

void Particle::keepInsideWindow() {
	const float W = static_cast<float>(ofGetWidth());
	const float H = static_cast<float>(ofGetHeight());

	if (position.x < 0.0f) {
		position.x = 0.0f;
		velocity.x *= -1.0f;
	} else if (position.x > W) {
		position.x = W;
		velocity.x *= -1.0f;
	}
	if (position.y < 0.0f) {
		position.y = 0.0f;
		velocity.y *= -1.0f;
	} else if (position.y > H) {
		position.y = H;
		velocity.y *= -1.0f;
	}
}

void NormalState::onEnter(Particle * particle) {
	particle->velocity.set(ofRandom(-0.5f, 0.5f), ofRandom(-0.5f, 0.5f));
}

void NormalState::update(Particle * particle) {
	particle->position += particle->velocity;
}

static void steer(Particle * particle, const ofVec2f & toward, float accel, float vmax, float posScale) {
	ofVec2f dir = toward - particle->position;
	float len = dir.length();
	if (len > 1e-6f) {
		dir /= len;
		particle->velocity += dir * accel;
	}
	particle->velocity.limit(vmax);
	particle->position += particle->velocity * posScale;
}

void AttractState::update(Particle * particle) {
	ofVec2f mouse(ofGetMouseX(), ofGetMouseY());
	steer(particle, mouse, 0.05f, 3.0f, 0.2f);
}

void RepelState::update(Particle * particle) {
	ofVec2f mouse(ofGetMouseX(), ofGetMouseY());
	ofVec2f away = particle->position - mouse;
	float len = away.length();
	if (len > 1e-6f) {
		away /= len;
		particle->velocity += away * 0.05f;
	}
	particle->velocity.limit(3.0f);
	particle->position += particle->velocity * 0.2f;
}

void StopState::update(Particle * particle) {
	particle->velocity *= 0.80f;
	if (particle->velocity.lengthSquared() < 1e-4f) {
		particle->velocity.set(0.0f, 0.0f);
	}
	particle->position += particle->velocity;
}

void BlackHoleState::onEnter(Particle * particle) {
	particle->velocity *= 0.1f;
}

void BlackHoleState::update(Particle * particle) {
	particle->velocity *= 0.95f;
	if (particle->velocity.lengthSquared() < 1e-6f) {
		particle->velocity.set(0.0f, 0.0f);
	}
	particle->position += particle->velocity;
}

Particle * ParticleFactory::createParticle(const std::string & type) {
	Particle * particle = new Particle();

	if (type == "star") {
		particle->size = ofRandom(2.0f, 4.0f);
		particle->color = ofColor(255, 0, 0);
	} else if (type == "shooting_star") {
		particle->size = ofRandom(3.0f, 6.0f);
		particle->color = ofColor(0, 255, 0);
		particle->velocity *= 3.0f;
	} else if (type == "planet") {
		particle->size = ofRandom(5.0f, 8.0f);
		particle->color = ofColor(0, 0, 255);
	} else if (type == "black_hole") {
		particle->size = ofRandom(12.0f, 16.0f);
		particle->color = ofColor(0);
		particle->setState(new BlackHoleState());
	}
	return particle;
}

ofApp::~ofApp() {
	for (Particle * p : particles) {
		removeObserver(p);
		delete p;
	}
	particles.clear();
}

void ofApp::setup() {
	ofBackground(0);
	particles.reserve(100 + 5 + 10 + 2);

	for (int i = 0; i < 100; ++i) {
		Particle * p = ParticleFactory::createParticle("star");
		particles.push_back(p);
		addObserver(p);
	}
	for (int i = 0; i < 5; ++i) {
		Particle * p = ParticleFactory::createParticle("shooting_star");
		particles.push_back(p);
		addObserver(p);
	}
	for (int i = 0; i < 10; ++i) {
		Particle * p = ParticleFactory::createParticle("planet");
		particles.push_back(p);
		addObserver(p);
	}
	for (int i = 0; i < 2; ++i) {
		Particle * p = ParticleFactory::createParticle("black_hole");
		particles.push_back(p);
		addObserver(p);
	}
}

void ofApp::update() {
	for (Particle * p : particles) {
		p->update();
	}
}

void ofApp::draw() {
	for (Particle * p : particles) {
		p->draw();
	}
}

void ofApp::keyPressed(int key) {
	switch (key) {
	case 's':
		notify("stop");
		break;
	case 'a':
		notify("attract");
		break;
	case 'r':
		notify("repel");
		break;
	case 'n':
		notify("normal");
		break;
	default:
		break;
	}
}
```

como aplique cada patron 


Factory: use el factory para crear la particula nueva pasandole el tipo "black_hole". Alli le puse tamaño grande, color negro y le asigne su estado inicial BlackHoleState. De esta forma toda la configuracion queda centralizada y solo la pido por nombre en setup.

Observer: la black_hole se registra como observer igual que las demas. Cuando ofApp manda un evento con notify, esta particula recibe la notificacion en onNotify y puede cambiar de estado sin estar directamente ligada a la logica del app.

State: la black_hole empieza en BlackHoleState. El state define como se mueve lentamente y controla su velocidad en update. Si cambian los eventos, setState la puede pasar a otros estados, evitando condicionales largos y haciendo mas facil extender el codigo.

### Autoevaluacion

mi nota debe ser 4.5 debido a que

actividad 1: esta completa con todo realizado 
[evidencia](#Actividad1)

actividad 2: hice todo menos una actividad entonces por eso es 4.5
[evidencia](#Actividad2)

actividad 3: todo esa completo
[evidencia](#Actividad3)

actividad 4: todo completo
[evidencia](#Actividad4)

actividad 5: arriba se ve como todo esta completo tambien
[evidencia](#Actividad5)






