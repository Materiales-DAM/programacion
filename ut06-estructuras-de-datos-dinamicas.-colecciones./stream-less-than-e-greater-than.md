---
cover: ../.gitbook/assets/tree.png
coverY: 94.60266666666666
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

# Stream\<E>

Los `Stream` en Java son una utilidad que permite realizar operaciones de procesamiento de datos de forma declarativa y **funcional** en colecciones de elementos. Los `Stream` permiten expresar operaciones como filtrado, mapeo, reducción y agrupación de manera más concisa y legible que el enfoque basado en bucles (programación estructurada).

Aquí hay algunos conceptos clave relacionados con los streams en Java:

1. **Fuente de datos** (source): Un stream en Java se crea a partir de una fuente de datos, que puede ser una colección (por ejemplo, List, Set, Map), un array, una entrada/salida (por ejemplo, un archivo) o incluso un generador de elementos.
2. **Operaciones intermedias**: Son operaciones que se aplican a un stream. Las operaciones intermedias incluyen métodos como `filter()`, `map()`, `sorted()`, `distinct()`, entre otros. Estas operaciones son lazy, es decir que no se ejecutan hasta que se llama a una operación terminal.
3. **Operaciones terminales**: Este tipo de operaciones finalizan el stream y producen un resultado. Las operaciones terminales pueden ser `forEach()`, `collect()`, `reduce()`, `count()`, `anyMatch()`, `allMatch()`, `noneMatch()`, entre otras. Una vez que se invoca una operación terminal, no se puede volver a usar el stream.

<figure><img src="../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

Veamos un ejemplo simple para ilustrar cómo funcionan los streams en Java:

Supongamos que tenemos una lista de números y queremos filtrar los números pares, duplicar cada número y luego imprimir los resultados:

```java
javaCopy codeimport java.util.Arrays;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        List<Integer> numeros = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

        numeros.stream()
               .filter(n -> n % 2 == 0)  // Filtrar números pares
               .map(n -> n * 2)           // Duplicar cada número
               .forEach(System.out::println);  // Imprimir los resultados
    }
}
```

En este ejemplo, `numeros.stream()` se crea un stream a partir de la lista de números. Luego, llamamos a `filter()` para mantener solo los números pares, después usamos `map()` para duplicar cada número y finalmente usamos `forEach()` para imprimir los resultados. Todas las operaciones intermedias se están expresando a través de una construcción denominada Lambda

## Lambdas

Las expresiones lambda son una característica que proporciona una forma más concisa y funcional de expresar funciones anónimas.

### Sintaxis

La sintaxis básica de una expresión lambda es la siguiente

```java
(parametros) -> expresion
```

* `(parámetros)`: Lista de parámetros que toma la lambda. Puede ser vacía si no hay parámetros, un parámetro sin paréntesis si hay exactamente uno, o múltiples parámetros separados por comas dentro de paréntesis si hay más de uno.
* `->`: Operador de flecha que separa los parámetros de la expresión.
* `expresion`: Código que se ejecutará cuando la lambda sea invocada.

#### Ejemplos

1.  Lambda sin parámetros

    ```java
    () -> System.out.println("Hola, mundo");
    ```
2.  Lambda con un parámetro:

    ```java
    (nombre) -> System.out.println("Hola, " + nombre);
    ```
3.  Lambda con múltiples parámetros:

    ```java
    (x, y) -> x + y
    ```

#### Notación del tipo de lambda

Para expresar el tipo de lambda que necesitamos en cada lugar vamos a usar la siguiente notación:

* Primero ponemos entre paréntesis y separados por comas los tipos de los parámetros de la lambda
* Después de los paréntesis ponemos el símbolo ->
* Por último, ponemos el tipo de retorno&#x20;

Ejemplos:

* () -> String: no tiene parámetros y devuelve un String
* (Integer) -> String: tiene un parámetro de tipo Integer y devuelve un String
* (String) -> Void: tiene un parámetro de tipo String y no devuelve nada ( es void)
* (Integer, String) -> Integer: tiene dos parámetros: el primero es de tipo Integer y el segundo de tipo String. Además, devuelve un Integer.

#### Uso de Lambdas con Streams

Las expresiones lambda se utilizan comúnmente con streams para realizar operaciones sobre colecciones de manera más concisa. Por ejemplo, para imprimir todos los elementos de una lista:

```java
List<String> nombres = Arrays.asList("Juan", "María", "Carlos");

// Esta lambda es de tipo (String) -> Void
nombres.forEach(nombre -> System.out.println(nombre));
```

#### Lambdas de más de una línea

Si el cuerpo de una función lambda tiene más de una línea se deben abrir llaves

```java
var nombresMayusculas = nombres
       // Lambda de tipo (String) -> String
       .map(
              nombre -> {
                     String upper = nombre.toUpperCase();
                     return upper;
              }
       );
```

## Operaciones intermedias de Stream&#x20;

Las operaciones intermedias se aplican a un `Stream` y devuelven otro `Stream`, lo que permite encadenar múltiples operaciones.

### **filter**

Sirve para quitar elementos de un stream que no cumplan una condición determinada. El método que se utiliza es filter y recibe como parámetro una función lambda (E) -> Boolean.

```java
Stream<String> stream = Arrays.asList("Juan", "María", "Carlos").stream();

stream
    // Esta lambda (String) -> Boolean, comprueba que el parámetro nombre empieza por J
    .filter(nombre -> nombre.startsWith("J"))
    // Muestra todos los elementos del stream resultante usando una lambda (String) -> Void
    .foreach(nombre -> System.out.println(nombre));
```

### map

Se utiliza para **transformar** los elementos de un `Stream<A>` aplicando una función a cada elemento y devolviendo un nuevo `Stream<B>` con los elementos transformados. El número de elementos del Stream resultante es el mismo que en el Stream original, ya que simplemente se aplica una transformación a cada uno de ellos.

Toma como parámetro una función lambda `(A) -> B`, donde `A` es el tipo del Stream original y `B` el del Stream resultante.&#x20;

<pre class="language-java"><code class="lang-java">// En este caso tenemos un  Stream para el que la A es String
Stream&#x3C;String> stream = Arrays.asList("Juan", "María", "Carlos").stream();
<strong>// El mapeo genera un Stream&#x3C;Integer> que luego es recolectado en una List&#x3C;Ingeger>
</strong><strong>List&#x3C;Integer> nameLengths = stream
</strong>    // Transformamos cada nombre en el número de caracteres que lo componen
    // La lambda que se aplica es String -> Integer
    // Este map devuelve un Stream&#x3C;Integer>
    .map(nombre -> nombre.length())
    // Ahora ejecutamos una operación terminal para que muestre todos los elementos del stream resultante
    .collect(Collerctors.toList());
</code></pre>

### flatMap

```java
stream.flatMap(String::toUpperCase);
```

### **sorted**

Los elementos de un `Stream` se pueden ordenar utilizando el método sorted de la siguiente manera

```java
Stream<String> stream = Arrays.asList("Juan", "María", "Carlos").stream();
// Ordenará los String en orden alfabético
stream
    .sorted();
    // Ahora ejecutamos una operación terminal para que muestre todos los elementos del stream resultante
    .foreach(nombre -> System.out.println(nombre));
```

También es posible especificar una ordenación distinta proviendo de un `Comparator<T>` al método sorted.

```java
Stream<String> stream = Arrays.asList("Juan", "María", "Carlos").stream();
// Ordenará los String en orden alfabético
stream
    // Pasamos un comparador que ordena de alguna otra forma
    .sorted(new ReverseStringComparator());
    // Ahora ejecutamos una operación terminal para que muestre todos los elementos del stream resultante
    .foreach(nombre -> System.out.println(nombre));
```

### **limit**

Este método hace el `Stream` resultante solo se quede con un número máximo de elementos

```java
Stream<String> stream = Arrays.asList("Juan", "María", "Carlos").stream();
// Ordenará los String en orden alfabético
stream
    // Nos quedamos con los dos primeros elementos
    .limit(2)
    // Ahora ejecutamos una operación terminal para que muestre todos los elementos del stream resultante
    .foreach(nombre -> System.out.println(nombre));
```

### **skip**

Este método hace que el `Stream` resultante se salte un número determinado de elementos

```java
Stream<String> stream = Arrays.asList("Juan", "María", "Carlos").stream();
// Ordenará los String en orden alfabético
stream
    // Nos saltamos los dos primeros elementos
    .skip(2)
    // Ahora ejecutamos una operación terminal para que muestre todos los elementos del stream resultante
    .foreach(nombre -> System.out.println(nombre));
```

## Operaciones Terminales

Las operaciones terminales producen un resultado final o llevan a cabo una acción final, y después de que se haya aplicado una operación terminal, el `Stream` ya no puede ser utilizado.

### **collect**

Se utiliza para recopilar los elementos de un stream en una estructura de datos específica, como una lista (`List`), un conjunto (`Set`), un mapa (`Map`), etc.

La clase Collectors incluye métodos que permiten recopilar los elementos de un Stream en los diferentes ADT.

```java
Stream<String> names = Arrays.asList("Juan", "María", "Carlos").stream();

List<String> namesList = 
    names
        .stream()
        // Nos saltamos los dos primeros elementos
        .skip(2)
        // Los elementos del stream resultante se cargan en una lista
        .collect(Collectors.toList());
        

Set<String> namesSet = 
    names
        .stream()
        // Nos saltamos los dos primeros elementos
        .skip(2)
        // Los elementos del stream resultante se cargan en un Set
        .collect(Collectors.toSet());
```

### reduce

Permite combinar los elementos del `Stream<T>` en un solo valor de tipo `Optional<T>`. Para ello, es necesario pasar una función de. La función de reducción toma dos parámetros del tipo que contiene la colección y devuelve un único resultado del mismo tipo.

Después de hacer un reduce, obtenemos un objeto de tipo Optiona\<T>l

```java
Optional<String> reduced = stream.reduce((s1, s2) -> s1 + s2);
```

### **foreach**

```java
stream.forEach(v -> System.out.println(v));
```

### **findFirst**

```java
Optional<String> firstElement = stream.findFirst();
```

