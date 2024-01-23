---
cover: ../../.gitbook/assets/generics.jpg
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

# Genéricos

Los genéricos son una característica del lenguaje que permiten escribir código que puede trabajar con diferentes tipos de datos de manera segura y sin perder la flexibilidad del tipado estático. Los genéricos se introdujeron en Java 5 para proporcionar una forma de escribir código más robusto y reusable al tratar con colecciones de objetos y algoritmos.

La principal ventaja de los genéricos es que te permiten parametrizar clases, interfaces y métodos con uno o varios tipos genéricos sin perder la información de tipo en tiempo de compilación. Esto mejora la seguridad y legibilidad del código al evitar conversiones manuales y reducir la posibilidad de errores en tiempo de ejecución.

## Parámetros de tipo

Un parámetro de tipo, en el contexto de programación genérica, es un marcador o símbolo que se utiliza para representar un tipo sin especificar concreto. Permite que clases, interfaces y métodos sean definidos de manera más general, de modo que puedan trabajar con varios tipos de datos sin comprometer la seguridad de tipos.

En Java, los parámetros de tipo se especifican entre los signos de menor (`<`) y mayor (`>`) angular en la definición de una clase, interfaz o método genérico. Estos parámetros actúan como marcadores de posición para el tipo de dato que se utilizará cuando se utilice la clase, interfaz o método.

## Interfaces genéricas

Los interfaces genéricos definen uno o más parámetros de tipo en su cabecera. Por ejemplo, podríamos definir el interface `Reader<T>` que define un contrato para leer objetos de cualquier tipo, dependiendo de la `T` que especifiquemos en cada implementación.

```java
// Reader declara un parámetro de tipo llamado T, esta T será más tarde 
// definido con un tipo concreto en otra parte del código
public interface Reader<T> {
    // El método
    T read();
}
```

A partir de este interface, podemos crear clases que lo implementen especificando el tipo de objetos que van a leer.

```java
// En esta cabecera especificamos que la T de Reader es Circle (para esta clase)
public class CircleReader implements Reader<Circle> {
    
    // Este método devuelve Circle porque la T que se ha especificado en la cabecera es CIrcle
    @Override
    public Circle read() {
        // Aquí va la implementación del reader
        return null;
    }
}
```

Además, puede haber otras implementaciones de `Reader` que especifiquen otra `T`

```java
// En esta cabecera especificamos que la T de Reader es Dog (para esta clase)
public class DogReader implements Reader<Dog> {
    
    // Este método devuelve Dog porque la T que se ha especificado en la cabecera es CIrcle
    @Override
    public Dogrcle read() {
        // Aquí va la implementación del reader
        return null;
    }
}
```

Las interfaces genéricas son muy útiles para crear contratos genéricos que pueden reutilizarse en varios componentes, como es el caso de los readers.

### Polimorfismo genérico

Ahora podemos ver las instancias de `CircleReader` como `Reader<Circle>`, a esto se le denomina polimorfismo genérico

```java
// circleReader tiene las formas: Reader<Circle> y CircleReader
Reader<Circle> circleReader = new CircleReader();
// dogReader tiene las formas: Reader<Dog> y DogReader
Reader<Dog> dogReader = new DogReader();
```

## Clases genéricas

Al igual que con los interfaces, podemos crear clases genéricas añadiendo parámetros de tipos a la clase. En este tipo de programación genérica cada instancia de la clase genérica puede especificar una T distinta.

```java
// Esta clase Box me permite crear cajas que guardan un valor, el tipo del valor es 
// el genérico T, lo cual me permite crear cajas que almacenan todo tipo de valores
public class Box<T> {
    private T value;
    
    public Box(T value) {
        this.value = value;
    }
    
    public T unbox(){
        return value;
    }
    
    public void box(T value) {
        this.value = value;
    }
}

public class Main{
    public static void main(String[] args){
        // Creamos una caja con un entero dentro: T = Integer
        Box<Integer> intBox = new Box<>(45);
        // Creamos una caja con un String dentro: T = String
        Box<String> strBox = new Box<>("Hola mundo");

        // Cuando hago el unbox de la caja de entero me devuelve un int
        int number = intBox.unbox();
        System.out.println(number);

        // Cuando hago el unbox de la caja de String me devuelve un String
        String string = strBox.unbox();
        System.out.println(string);

        // En esta caja solo puedo meter valores enteros
        intBox.box(1);
        System.out.println(intBox.unbox());

        // En esta caja solo puedo meter valores String
        strBox.box("Adiós");
        System.out.println(strBox.unbox());
    }
}
```

Una vez creada una instancia de Box, no podemos cambiar el tipo de valores que almacena

