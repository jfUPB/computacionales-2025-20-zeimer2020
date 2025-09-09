# Bitácora de aprendizaje de la unidad 5

## 1.  **Diagnóstico inicial**

¿Qué es el encapsulamiento para ti? Describe una situación en la que te haya sido útil o donde hayas visto su importancia.

- restriccion que posee una variable o un metodo, por ejemplo cuando usabamos variables en escenarios concretos y solo queriamos usarlas en esos momentos especificos

¿Qué es la herencia? ¿Por qué un programador decidiría usarla? Da un ejemplo simple.

- herencia es cuando hacemos que una clase herede todas las caractreristicas de otra clase, haciendo que sea dueña tmb de todo atributo de la otra clase, por ejemplo si hacemos que la clase perro herede de la clase animal terrestre


¿Qué es el polimorfismo? Describe con tus palabras qué significa que un código sea “polimórfico”.

- cuando en clases tenemos el mismo metodo pero se definen de diferentes maneras entonces como tal hacen cosas distintas

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



## 2.  **La pregunta inicial**


## 3.  **Registro de exploración:** 
> Aquí documentas cada ciclo de pregunta -> hipótesis -> experimento -> hallazgo -> reflexión.
> Debe ser rico en evidencia visual (código, capturas del depurador con anotaciones, diagramas).

## 4.  **Consolidación, autoevaluación y cierre:**
> [!CAUTION]
> Esta sección es OBLIGATORIA y central para tu evaluación
