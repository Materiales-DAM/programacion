---
cover: ../../.gitbook/assets/image (1).png
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

# Interfaces

En Java, una interface es una colección de métodos abstractos (sin implementación) y constantes que pueden ser implementados por cualquier clase. Las interfaces permiten la definición de un conjunto de métodos que deberán ser definidos por aquellas clases que implementen dicho interface. Además, las interfaces permiten la creación de código que puede interactuar con objetos de diversas clases a través de la interfaz común.

En este sentido, los interfaces nos permiten separar el "qué" del "cómo", lo cual permite que unos componentes se puedan abstraer de lo que hacen sus dependencias (principio de **abstracción**).

## **Declaración de un interface**

Un interface puede contener:

* Definiciones de métodos: sólo se definirá la cabecera del método, sin implementación. Los métodos que se definan en un interface son públicos, por lo que no es necesario poner la palabra reservada `public`.&#x20;
* Constantes: se podrán declarar constantes poniendo su tipo, nombre y valor asignado. Las constantes son públicas, estáticas y final, por lo que no es necesario poner las palabras reservadas `public`, `static` ni `final`.

```java
public interface MiInterfaz {
    // Métodos abstractos (sin implementación)
    void metodoUno();
    int metodoDos(String parametro);
    
    // Constantes (públicas, estáticas y finales por defecto)
    int CONSTANTE = 42;
}
```

## **Implementación de interfaces**

Solo las clases pueden implementar interfaces, para ello añadiremos la palabra reservada implements a la cabecera de la clase.

Añadiremos la anotación `@Override` a los métodos que vienen definidos en la interface.&#x20;

```java
class MiClase implements MiInterfaz {
    // Implementación de los métodos de la interfaz
    @Override
    public void metodoUno() {
        // Código de implementación
    }
    
    @Override
    public int metodoDos(String parametro) {
        // Código de implementación
        return parametro.length();
    }
}
```

A diferencia de con la herencia, una clase puede implementar varias interfaces, permitiendo así la implementación de múltiples comportamientos:

```java
public interface OtraInterfaz {
    String metodoDeOtraInterfaz(String parametro);
}

class MiClase implements MiInterfaz, OtraInterfaz {
    // Implementación de métodos y constantes de ambas interfaces
    @Override
    public void metodoUno() {
        // Código de implementación
    }
    
    @Override
    public int metodoDos(String parametro) {
        // Código de implementación
        return parametro.length();
    }
    
    @Override
    public String metodoDeOtraInterfaz(String parametro) {
        // Código de implementación
        return parametro;
    }
}
```

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

## **Herencia entre interfaces**

Las interfaces pueden extender otras interfaces mediante la palabra clave `extends`:

```java
// Esta interfaz incluye metodoUno, metodoDos, CONSTANTE y metodoDeOtraInterfaz
interface OtraInterfaz extends MiInterfaz {

    String metodoDeOtraInterfaz(String parametro);
}
```

El interface `OtraInterfaz` heredará todos los métodos y constantes definidos en `MiInterfaz`

## **Default Methods**&#x20;

A partir de Java 8, las interfaces pueden tener métodos con implementación (conocidos como "default methods"). Estos métodos proporcionan una implementación predeterminada y pueden ser heredados por las clases que implementan la interfaz:

```java
interface MiInterfazConDefaultMethod {
    void metodoUno();
    
    default void metodoPorDefecto() {
        System.out.println("Implementación por defecto");
    }
}
```

