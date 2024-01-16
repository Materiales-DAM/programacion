---
cover: ../../.gitbook/assets/polymorphism.png
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

# Polimorfismo de subtipos

El polimorfismo de subtipos en Java se refiere a la capacidad de un objeto de ser visto con la forma de cualquiera de sus . Esto se logra mediante la herencia y permite tratar objetos de las subclases como si fueran objetos de la clase base.

Veamos cómo funciona el polimorfismo con el ejemplo de los animales

```java
public class SubtypePolymorphism {
    public static void main(String[] args) {
        // Los objetos que estamos creando pueden ser vistos como el supertipo
        Animal tobi = new Dog("Tobi", "Bob Esponja");
        Animal simba = new Lion("Simba", "Serengeti");

        tobi.talk(); // Muestra "Guau, guau"
        simba.talk(); // Muestra "Roar, roar"
    }
}
```

Explicación:

1. La clase `Animal` es la clase base con un método llamado `talk`.
2. Las clases `Dog` y `Lion` son subclases de `Animal` que sobrescriben el método `talk` y tienen métodos específicos adicionales.
3. En el método `main`, se crean instancias de las subclases y se almacenan en referencias de tipo `Animal`. Esto demuestra el polimorfismo de subtipos, ya que las instancias de subclases se pueden tratar como instancias de la clase base.
4. Al llamar al método `talk`, se ejecuta la versión del método de la subclase correspondiente a cada instancia.

## Casting

El casting y el polimorfismo están estrechamente relacionados, especialmente cuando se trata de trabajar con clases y objetos en una jerarquía de herencia. Hay dos tipos de casting

### Casting implícito (upcasting)

Permite asignar automáticamente una instancia de una subclase a una referencia de la superclase, facilitando la creación de código más genérico y reutilizable. En este tipo de casting no es necesario indicar nada en el código, debido a que esta conversión nunca puede fallar.

<pre class="language-java"><code class="lang-java"><strong>// El objeto es de tipo Dog y la variable es de tipo Animal, se produce un casting 
</strong><strong>// implícito de Dog a Animal
</strong>Animal tobi = new Dog("Tobi", "Bob Esponja");
</code></pre>

La variable tobi es de tipo Animal, por lo que puedo sólo se pueden usar los métodos definidos en dicha clase, pero no los métodos específicos de Dog (a pesar de que el objeto es de ese tipo).&#x20;

<pre class="language-java"><code class="lang-java"><strong>tobi.talk();
</strong><strong>System.out.println(tobi.getName());
</strong><strong>
</strong><strong>// Este código no compila porque la variable tobi es de tipo Animal
</strong><strong>System.out.println(tobi.getOwner());
</strong></code></pre>

### Casting explícito (downcasting)

Permite convertir una referencia de la superclase a una referencia de la subclase cuando es necesario acceder a métodos específicos de la subclase. Para realizar este tipo de casting es necesario que el código lo indique explícitamente, esto se debe a que el programador debe ser consciente de que la operación que está realizando podría fallar si se hace casting al tipo incorrecto.

Como sabemos que tobi es un perro, podemos crear una nueva variable de tipo Dog y hacer un downcasting de tipos para poder acceder los métodos definidos en Dog.

<pre class="language-java"><code class="lang-java"><strong>// Esto es un casting explícito que va de Animal a Dog
</strong><strong>Dog tobiDog = (Dog) tobi;
</strong><strong>
</strong><strong>tobiDog.talk();
</strong><strong>System.out.println(tobiDog.getName());
</strong><strong>
</strong><strong>// Este código compila porque la variable tobiDog es de tipo Dog
</strong><strong>System.out.println(tobiDog.getOwner());
</strong></code></pre>

#### ClassCastException

En el ejemplo anterior estábamos seguros de que tobi era un perro, por lo que podíamos hacer el casting y funcionaba, pero ¿qué pasa si hacemos un casting a un tipo equivocado?

Veamos un ejemplo en el que creamos un array de animales y luego tratamos de convertirlos todos a perros.

<pre class="language-java"><code class="lang-java"><strong>// Creamos un array con tres animales, dos son perros y uno un león
</strong><strong>Animal[] animals = {
</strong><strong>    new Dog("Tobi", "Bob Esponja"),
</strong><strong>    new Dog("Beethoven", "Peppa Pig"),
</strong><strong>    new Lion("Simba", "Serengeti"),
</strong><strong>};
</strong><strong>
</strong><strong>for(Animal animal: animals) {
</strong><strong>    // Este casting funciona en las dos primeras iteraciones, pero provoca una excepción en la tercera
</strong><strong>    Dog dog = (Dog) animal;
</strong><strong>    System.out.println(dog.getOwner());
</strong><strong>}
</strong></code></pre>

El código anterior compila, pero provoca una excepción de tipo ClassCastException cuando es ejecutado. Esta excepción no está indicando que se ha tratado de ejecutar un casting ilegal durante la ejecución del programa, en este caso porque estamos intentando convertir un objeto de tipo Lion a Dog y eso no es posible. La traza de la excepción tendrá un aspecto de este tipo

```log
Exception in thread "main" java.lang.ClassCastException: class org.ies.animals.model.Lion cannot be cast to class org.ies.animals.model.Dog (org.ies.animals.model.Lion and org.ies.animals.model.Dog are in unnamed module of loader 'app')
	at org.ies.animals.Main.main(Main.java:19)

```

#### instanceof

Cuando no sepamos con seguridad de qué tipo es el objeto para el que queremos hacer casting podemos usar la construcción instanceof para estar seguros

<pre class="language-java"><code class="lang-java"><strong>for(Animal animal: animals) {
</strong><strong>    if(animal instanceof Dog) {
</strong><strong>        // Entra en las dos primeras iteraciones
</strong><strong>        Dog dog = (Dog) animal;
</strong><strong>        System.out.println(dog.getOwner());
</strong><strong>    } else if(animal instanceof Lion) {
</strong><strong>        // Entra en la tercera iteración
</strong><strong>        Lion lion = (Lion) animal;
</strong><strong>        System.out.println(lion.getJungeName());
</strong><strong>    }
</strong><strong>}
</strong></code></pre>

## En resumen

El polimorfismo de subtipos en Java proporciona varias ventajas y capacidades que mejoran la flexibilidad y la eficiencia en el diseño de programas orientados a objetos. Aquí hay un resumen de las cosas que se pueden hacer gracias al polimorfismo de subtipos en Java:

1. **Tratar objetos de subclases como objetos de la clase base:**
   * Las instancias de subclases pueden ser asignadas a referencias de la clase base, lo que facilita el tratamiento uniforme de objetos de diferentes tipos dentro de una jerarquía de herencia.
2. **Sustitución dinámica de métodos:**
   * Permite que los métodos de una clase base sean sobrescritos en las subclases, y la versión correcta del método se elige en tiempo de ejecución según el tipo real del objeto.
3. **Casting implícito (upcasting):**
   * Permite asignar automáticamente una instancia de una subclase a una referencia de la superclase, facilitando la creación de código más genérico y reutilizable.
4. **Casting explícito (downcasting):**
   * Permite convertir una referencia de la superclase a una referencia de la subclase cuando es necesario acceder a métodos específicos de la subclase.
5. **Extensibilidad y mantenibilidad del código:**
   * Facilita la creación de programas extensibles, ya que nuevas subclases pueden agregarse sin modificar el código existente. Esto promueve la reutilización y mantenimiento del código.
6. **Desarrollo basado en abstracción:**
   * Permite trabajar con abstracciones más generales, como interfaces o clases base abstractas, sin preocuparse por los detalles específicos de implementación en las subclases.
7. **Mejora la legibilidad y claridad del código:**
   * Al utilizar polimorfismo, el código puede expresar de manera más clara y concisa las relaciones entre las clases, mejorando la comprensión y mantenimiento del software.

Por tanto, el polimorfismo de subtipos en Java facilita el diseño de programas más dinámicos y flexibles al permitir tratar objetos de manera uniforme, independientemente de su tipo concreto. Esto conduce a un código más modular, extensible y fácil de entender.
