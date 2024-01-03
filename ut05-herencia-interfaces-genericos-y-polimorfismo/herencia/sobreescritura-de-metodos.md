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

# Sobreescritura de métodos

La sobreescritura de métodos en Java permite a una subclase proporcionar una implementación específica para un método que está definido en su superclase. Esto se aplica a métodos abstractos y métodos heredados de una clase base. Aquí hay una explicación detallada de los conceptos mencionados:

## **Implementación de Métodos Abstractos**

Como hemos visto anteriormente,  un método abstracto es un método declarado en una clase abstracta que no tiene implementación en esa clase. Las clases abstractas se utilizan para proporcionar una estructura común para las subclases, pero las subclases deben implementar los métodos abstractos.

```java
// Clase abstracta Animal
abstract class Animal {
    private String name;

    // Constructor
    public Animal(String name) {
        this.name = name;
    }

    // Método abstracto que debe ser implementado por las clases derivadas
    public abstract void saySomething();

    // Método concreto compartido por todas las clases derivadas
    public void sleep() {
        System.out.println(nombre + " está durmiendo.");
    }
}
```

Cuando una subclase hereda de una superclase, debe proporcionar su propia implementación para los métodos abstractos que hereda. La sobreescritura se realiza utilizando la misma firma (nombre, tipo de retorno, y lista de parámetros) que el método en la superclase.

```java
// Clase concreta Lion que extiende Animal
class Lion extends Animal {
    
     private String jungleName;

    public Lion(String name, String jungleName) {
        super(name);
        this.jungleName = jungleName;
    }

    public String getJungleName() {
        return jungleName;
    }

    public void setJungleName(String jungleName) {
        this.jungleName = jungleName;
    }

    // Es obligatorio imlementar el métood saySomething en la clase Lion
    @Override
    public void saySomething() {
        System.out.println("Roar, roar!!");
    }

}
```

## **Sobreescritura de métodos no abstractos**

Además de implementar los métodos abstractos, las subclases pueden sobrescribir métodos que ya tienen una implementación en la clase base. Esto permite que las subclases proporcionen una implementación específica sin cambiar  la superclase.

```java
// Clase concreta Lion que extiende Animal
class Lion extends Animal {
    
     private String jungleName;

    public Lion(String name, String jungleName) {
        super(name);
        this.jungleName = jungleName;
    }

    public String getJungleName() {
        return jungleName;
    }

    public void setJungleName(String jungleName) {
        this.jungleName = jungleName;
    }

    // Es obligatorio imlementar el métood saySomething en la clase Lion
    @Override
    public void saySomething() {
        System.out.println("Roar, roar!!");
    }
    
    // Cuando se invoque el método sleep de un león se ejecutará este código, no el de la clase Animal
    @Override
    public void sleep() {
        System.out.println("El león " + getName() +" está durmiendo en " + jungleName);
    }

}
```

### **Modificador `final`**

En Java, el modificador `final` se utiliza para evitar que una clase, método o variable sea modificado o extendido. Cuando se aplica a un método, impide que las subclases lo sobrescriban.

```java
abstract class Animal {
    private String name;

    // Constructor
    public Animal(String name) {
        this.name = name;
    }

    // Método abstracto que debe ser implementado por las clases derivadas
    public abstract void saySomething();

    // Método final que no puede ser sobreescrito
    public final void sleep() {
        System.out.println(nombre + " está durmiendo.");
    }
}

class Lion extends Animal {
    
     private String jungleName;

    public Lion(String name, String jungleName) {
        super(name);
        this.jungleName = jungleName;
    }

    public String getJungleName() {
        return jungleName;
    }

    public void setJungleName(String jungleName) {
        this.jungleName = jungleName;
    }

    // Es obligatorio imlementar el métood saySomething en la clase Lion
    @Override
    public void saySomething() {
        System.out.println("Roar, roar!!");
    }
    
    // Este código NO COMPILA, da error porque sleep() es final en Animal y por tanto
    // no se puede sobreescribir
    @Override
    public void sleep() {
        System.out.println("El león " + getName() +" está durmiendo en " + jungleName);
    }

}
```

## **Malas prácticas en la sobreescritura de métodos**

* Es aconsejable usar la anotación `@Override` al sobrescribir métodos. Aunque no es obligatorio, ayuda al compilador a detectar errores.
* Es aconsejable hacer final aquellos métodos que no se desean sobreescribir
* Sobreescribir métodos no abstractos da lugar a programas difíciles de analizar y debuguear, siempre hay una formas de diseñar el programa sin utilizar esta técnica.
