---
cover: ../../.gitbook/assets/image (8).png
coverY: 0
layout:
  cover:
    visible: true
    size: hero
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Clases abstractas

Las clases abstractas son un concepto fundamental en la programación orientada a objetos (POO). En términos simples, una clase abstracta sirve como un modelo o plantilla para otras clases. A diferencia de una clase común, una clase abstracta **no puede ser instanciada**; en cambio, se utiliza como base para derivar clases concretas.

Aquí hay algunos puntos clave sobre las clases abstractas:

1. **No se pueden instanciar:** No puedes crear objetos directamente a partir de una clase abstracta. Debes derivar una clase concreta que implemente (defina) los métodos abstractos de la clase base.
2. **Permte definir métodos abstractos:** Una clase abstracta generalmente incluye uno o más métodos abstractos. Un método abstracto es un método que se declara en la clase abstracta pero no se implementa en ella. La implementación real se deja a las clases concretas que heredan de la clase abstracta.
3. **Puede contener métodos concretos:** Además de los métodos abstractos, una clase abstracta puede contener métodos concretos (métodos con implementación) que son compartidos por las clases derivadas.
4. **Promueven la reutilización de código:** Al definir una clase abstracta, puedes establecer un conjunto común de métodos que deben implementarse en las clases derivadas. Esto fomenta la reutilización del código y ayuda a mantener una estructura coherente en las clases hijas.

Si volvemos al ejemplo anterior, veremos que la clase Animal puede ser definida como abstracta. Esto es posible porque todo animal es de una especie en concreto, por lo que no tiene sentido crear un animal genérico sin especie



<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

La jerarquía de clases quedaría de la siguiente manera haciendo Animal abstracta

```java
// Clase abstracta Animal
abstract class Animal {
    private String name;

    // Constructor
    public Animal(String name) {
        this.name = name;
    }

    // Método abstracto que debe ser implementado por las clases derivadas
    abstract void saySomething();

    // Método concreto compartido por todas las clases derivadas
    public void sleep() {
        System.out.println(nombre + " está durmiendo.");
    }
}

// Clase concreta Lion que extiende Animal
class Lion extends Animal {
    // Constructor
    public Lion(String name) {
        super(name);
    }

    // Implementación del método abstracto saySomething
    void saySomething() {
        System.out.println("Rugido del león.");
    }
}

// Clase concreta Dog que extiende Animal
class Dog extends Animal {
    // Constructor
    public Dog(String name) {
        super(name);
    }

    // Implementación del método abstracto saySomething
    void saySomething() {
        System.out.println("Ladrido del perro.");
    }
}

// Clase principal para probar el código
public class Main {
    public static void main(String[] args) {
        // Crear instancias de Lion y Dog
        Lion leon = new Lion("Simba");
        Dog perro = new Dog("Buddy");

        // Llamar a métodos compartidos y específicos de cada clase
        leon.saySomething();
        leon.sleep();

        perro.saySomething();
        perro.sleep();
    }
}
```

En este ejemplo:

* `Animal` es una clase abstracta que tiene un método abstracto `saySomething()` y un método concreto `sleep()`.
* `Lion` y `Dog` son clases concretas que extienden `Animal` y proporcionan implementaciones específicas para el método `saySomething()`.
* En la clase principal (`Main`), se crean instancias de `Lion` y `Dog` y se llaman a sus métodos para mostrar cómo heredan y pueden utilizar tanto los métodos compartidos como los específicos de su propia clase.
