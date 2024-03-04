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

#### Ejemplos:

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

#### Uso de Lambdas con Streams

Las expresiones lambda se utilizan comúnmente con streams para realizar operaciones sobre colecciones de manera más concisa. Por ejemplo, para imprimir todos los elementos de una lista:

```java
List<String> nombres = Arrays.asList("Juan", "María", "Carlos");

nombres.forEach(nombre -> System.out.println(nombre));
```

#### Lambdas de más de una línea

Si el cuerpo de una función lambda tiene más de una línea se deben abrir llaves

```java
nombres.forEach(
       nombre -> {
             String upper = nombre.toUpperCase();
             System.out.println(upper);
       }
);
```

## Operaciones intermedias de Stream&#x20;

Las operaciones intermedias se aplican a un `Stream` y devuelven otro `Stream`, lo que permite encadenar múltiples operaciones.

### **filter**

Sirve para quitar elementos de un stream que no cumplan una condición determinada. El método que se utiliza es filter y recibe como parámetro una función lambda con un parámetro de tipo E y devuelve un boolean.

```java
Stream<String> stream = Arrays.asList("Juan", "María", "Carlos").stream();
// La lambda de filter tiene un parámetro s de tipo String y devuelve un boolean
// En este caso el stream solo mantendrá aquellos elementos que empiezan por J
stream
    .filter(nombre -> nombre.startsWith("J"))
    // Ahora ejecutamos una operación terminal para que muestre todos los elementos del stream resultante
    .foreach(nombre -> System.out.println(nombre));
```

### map

```java
stream.map(String::toUpperCase);
```

### flatMap

```java
stream.flatMap(String::toUpperCase);
```

### **sorted**

```java
stream.sorted();
```

### **limit**

```java
stream.limit(5);
```

### **skip**

```java
stream.skip(2);
```

## Operaciones Terminales

Las operaciones terminales producen un resultado final o llevan a cabo una acción final, y después de que se haya aplicado una operación terminal, el `Stream` ya no puede ser utilizado.

### **collect**

```java
List<String> resultList = stream.collect(Collectors.toList());
```

### reduce

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

