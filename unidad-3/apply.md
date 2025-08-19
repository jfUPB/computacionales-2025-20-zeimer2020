# Unidad 3


## 🛠 Fase: Apply

### Actividad integradora apply

cofigo:

``` c++
#include <iostream>
#include <string>

class Personaje {
public:
    std::string nombre;
    int* estadisticas;

    Personaje(std::string n, int vida, int ataque, int defensa) {
        nombre = n;
        estadisticas = new int[3];
        estadisticas[0] = vida;
        estadisticas[1] = ataque;
        estadisticas[2] = defensa;
        std::cout << "Constructor: nace " << nombre << std::endl;
    }

    void imprimir() {
        std::cout << "Personaje " << nombre
            << " [Vida: " << estadisticas[0]
            << ", ATK: " << estadisticas[1]
            << ", DEF: " << estadisticas[2]
            << "]" << std::endl;
    }
};

void simularEncuentro() {
    std::cout << "\n--- Iniciando encuentro ---" << std::endl;
    Personaje heroe("Aragorn", 100, 20, 15);

    Personaje copiaHeroe = heroe;
    copiaHeroe.nombre = "Copia de Aragorn";

    std::cout << "Saliendo del encuentro..." << std::endl;
}

int main() {
    simularEncuentro();
    std::cout << "\nSimulación terminada." << std::endl;
    return 0;
}

```

primer error fuga de memoria:
Cuando creas un Personaje, este pide espacio en la memoria (heap) para guardar vida, ataque y defensa. El problema es que nunca devuelve ese espacio porque no hay destructor que lo libere. Entonces, cada vez que nace un personaje, queda un pedacito de memoria perdido. Con el tiempo el juego va gastando más y más RAM sin necesidad.

segundo error copia superficial en simularEncuentro:
Cuando haces Personaje copiaHeroe = heroe, lo que se copia no son las estadísticas nuevas, sino la misma dirección de memoria. O sea, heroe y copiaHeroe terminan usando el mismo espacio. Eso significa que si cambias un valor en uno, también se cambia en el otro. Y si más adelante los dos intentan borrar esa memoria, el programa se estrella.

``` c++
#include <string>
#include <iostream>

class Personaje {
public:
    Personaje(std::string n, int vida, int ataque, int defensa)
        : nombre(n), vida(vida), ataque(ataque), defensa(defensa) {
        std::cout << "Constructor: nace " << nombre << std::endl;
    }

    void imprimir() const {
        std::cout << "Personaje " << nombre
            << " [Vida: " << vida
            << ", ATK: " << ataque
            << ", DEF: " << defensa
            << "]" << std::endl;
    }

    const std::string& getNombre() const { return nombre; }
    int  getVida()   const { return vida; }
    int  getAtaque() const { return ataque; }
    int  getDefensa()const { return defensa; }

    void setNombre(const std::string& n) { nombre = n; }
    void setVida(int v) { vida = v; }
    void setAtaque(int a) { ataque = a; }
    void setDefensa(int d) { defensa = d; }

private:
    std::string nombre;
    int vida;
    int ataque;
    int defensa;
};

int main() {
    Personaje heroe("Aragorn", 100, 20, 15);
    heroe.imprimir();
    heroe.setVida(80);
    std::cout << "\nDespués de recibir daño...\n";
    heroe.imprimir();
    return 0;
}

```

El primer error de fuga de memoria ya esta corregido porque la clase ya no usa punteros ni new[]. Ahora las estadisticas viven como variables normales dentro del objeto, asi que cuando el objeto se destruye, la memoria se libera sola sin que quede nada perdido.

El segundo error de copia superficial tambien queda resuelto porque al copiar un personaje se copian directamente los valores de vida, ataque y defensa, no una direccion de memoria compartida. Cada objeto tiene sus propios datos, asi que modificar uno no afecta al otro y no existe riesgo de doble borrado.
