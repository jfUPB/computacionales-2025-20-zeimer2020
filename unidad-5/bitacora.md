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
> Aquí documentas cada ciclo de pregunta -> hipótesis -> experimento -> hallazgo -> reflexión.
> Debe ser rico en evidencia visual (código, capturas del depurador con anotaciones, diagramas).

## 4.  **Consolidación, autoevaluación y cierre:**
> [!CAUTION]
> Esta sección es OBLIGATORIA y central para tu evaluación
