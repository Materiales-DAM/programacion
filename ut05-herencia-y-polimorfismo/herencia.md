---
cover: ../.gitbook/assets/image (8).png
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

# Herencia

La herencia es un concepto fundamental en la programación orientada a objetos (OOP, por sus siglas en inglés) que permite la creación de nuevas clases basadas en clases existentes. La herencia facilita la reutilización de código y la organización de las clases en una jerarquía, lo que ayuda a estructurar y gestionar el código de manera más eficiente.

## **Jerarquías de clases**

Las clases se organizan en una estructura jerárquica. La superclase ocupa un nivel superior, y las subclases se sitúan debajo. Cada nivel de la jerarquía hereda las características de la clase superior y puede agregar nuevas funcionalidades.

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption><p>Jerarquía de clases de animales</p></figcaption></figure>

### **Superclase (Clase Base o Padre)**&#x20;

Es la clase de la cual se heredan las propiedades y comportamientos. Contiene atributos y métodos comunes que son compartidos por una o más subclases

### **Subclase (Clase Derivada o Hija)**

Es una clase que hereda atributos y métodos de una superclase. Puede agregar nuevos atributos y métodos o modificar los existentes. La subclase aprovecha la funcionalidad ya presente en la superclase.

### **Herencia**

#### **Herencia de Campos**

Las subclases heredan los campos (atributos) de la superclase. Esto significa que pueden utilizar las variables definidas en la superclase sin tener que volver a declararlas en la subclase.

#### **Herencia de Métodos**

Al igual que con los campos, las subclases heredan los métodos de la superclase. Esto permite que las subclases utilicen los mismos métodos que la superclase y, si es necesario, sobrescribir o agregar nuevos métodos.

La herencia promueve la reutilización del código, ya que las clases derivadas pueden aprovechar la funcionalidad ya implementada en las clases base. Además, facilita la mantenibilidad del código, ya que los cambios realizados en la superclase se reflejan automáticamente en todas las subclases.

## Herencia en Java

En Java, la herencia se logra mediante la palabra clave `extends`. Una clase que hereda de otra se denomina "subclase" o "clase derivada", mientras que la clase de la que se hereda se llama "superclase" o "clase base". La subclase hereda atributos y comportamientos de la superclase, permitiendo la extensión y especialización del código.

Por ejemplo, para implementar la jerarquía de clases de animales empezaríamos con la clase Animal

```java
package org.example;

public class Animal {
    private String color;

    public Animal(String color) {
        this.color = color;
    }

    public String getColor() {
        return color;
    }

    public void setColor(String color) {
        this.color = color;
    }
    
    public void eat() {
        System.out.println("Estoy comiendo");
    }
}
```

Después pasamos a implementar las subclases Dog y Lion

```java
package org.example;

public class Dog extends Animal {
    private String owner;

    public Dog(String color, String owner) {
        super(color);
        this.owner = owner;
    }

    public String getOwner() {
        return owner;
    }

    public void setOwner(String owner) {
        this.owner = owner;
    }
    
    public void bark() {
        System.out.println("Guau, guau");
    }
}
```

```java
package org.example;

public class Lion extends Animal {
    private String jungleName;

    public Lion(String color, String jungleName) {
        super(color);
        this.jungleName = jungleName;
    }

    public String getJungleName() {
        return jungleName;
    }

    public void setJungleName(String jungleName) {
        this.jungleName = jungleName;
    }

    public void roar() {
        System.out.println("Roar, roar!!");
    }
}
```

La relación que se establece con el uso de la herencia es una relación de tipo "es un/a". En el ejemplo anterior estaríamos estableciendo la siguiente relación Dog es un Animal y Lion es un Animal.

En este ejemplo Animal sería la clase base, padre o superclase, mientras que Dog y LIon serían las subclases o clases hijas de Animal.

### Ventajas de la herencia

1. **Reutilización de Código:** La herencia permite aprovechar el código existente en la superclase, lo que reduce la duplicación y facilita el mantenimiento del programa.
2. **Estructura Lógica:** La herencia facilita la organización jerárquica de clases, reflejando la relación "es un/a" entre las entidades del mundo real que el programa modela.
3. **Polimorfismo:** Permite tratar objetos de las subclases como objetos de la superclase, lo que favorece la flexibilidad y extensibilidad del código.

### Inconvenientes de la herencia

1. **Acoplamiento:** La herencia puede llevar a un alto grado de acoplamiento entre clases, lo que dificulta los cambios en la superclase sin afectar a las subclases.
2. **Jerarquías Complejas:** A medida que la jerarquía de clases crece, puede volverse compleja y difícil de gestionar, especialmente si no se planifica cuidadosamente.
3. **Herencia Múltiple Limitada:** Java no admite herencia múltiple de clases, lo que puede limitar la capacidad de reutilización en ciertos casos.

En resumen, la herencia en Java es una herramienta poderosa para la creación de software modular y flexible, pero debe utilizarse con precaución para evitar problemas de diseño y mantenimiento a largo plazo. Un buen diseño de clases y el uso adecuado de la herencia contribuyen a la creación de sistemas más sólidos y fáciles de mantener
