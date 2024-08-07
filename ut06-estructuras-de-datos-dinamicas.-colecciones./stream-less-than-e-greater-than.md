---
cover: ../.gitbook/assets/lambda.jpeg
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

# Stream\<E>

Los `Stream` en Java son una utilidad que permite realizar operaciones de procesamiento de datos de forma declarativa y **funcional** en colecciones de elementos. Los `Stream` permiten expresar operaciones como filtrado, mapeo, reducción... de manera más concisa y legible que el enfoque basado en bucles (programación estructurada).

Aquí hay algunos conceptos clave relacionados con los streams en Java:

1. **Fuente de datos** (source): Un stream en Java se crea a partir de una fuente de datos, que puede ser una colección (por ejemplo, List, Set, Map), un array, una entrada/salida (por ejemplo, un archivo) o incluso un generador de elementos.
2. **Operaciones intermedias**: Son operaciones que se aplican a un stream. Las operaciones intermedias incluyen métodos como `filter()`, `map()`, `sorted()`, `distinct()`, entre otros. Estas operaciones son lazy, es decir que no se ejecutan hasta que se llama a una operación terminal.
3. **Operaciones terminales**: Este tipo de operaciones finalizan el stream y producen un resultado. Las operaciones terminales pueden ser `forEach()`, `collect()`, `reduce()`, `count()`, `anyMatch()`, `allMatch()`, `noneMatch()`, entre otras. Una vez que se invoca una operación terminal, no se puede volver a usar el stream.

<figure><img src="../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

Veamos un ejemplo simple para ilustrar cómo funcionan los streams en Java:

Supongamos que tenemos una lista de números y queremos filtrar los números pares, duplicar cada número y luego imprimir los resultados:

```java
import java.util.Arrays;
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

## Lambdas (λ)

Las expresiones lambda son una característica que proporciona una forma más concisa y funcional de expresar funciones anónimas.

### Sintaxis

La sintaxis básica de una expresión lambda es la siguiente

<pre class="language-java"><code class="lang-java"><strong>(parametros) -> expresion
</strong></code></pre>

* `(parámetros)`: Lista de parámetros que toma la lambda. Puede ser vacía si no hay parámetros, un parámetro sin paréntesis si hay exactamente uno, o múltiples parámetros separados por comas dentro de paréntesis si hay más de uno.
* `->`: Operador de flecha que separa los parámetros de la expresión.
* `expresion`: Código que se ejecutará cuando la lambda sea invocada.

#### Ejemplos

1.  Lambda sin parámetros

    ```java
    () -> System.out.println("Hola, mundo")
    ```
2.  Lambda con un parámetro:

    ```java
    (nombre) -> System.out.println("Hola, " + nombre)
    ```
3.  Lambda con múltiples parámetros:

    ```java
    (x, y) -> x + y
    ```

#### Notación del tipo de lambda

Para expresar el tipo de lambda que necesitamos en cada lugar vamos a usar la siguiente notación:

* Primero ponemos entre paréntesis y separados por comas los tipos de los parámetros de la lambda
* Después de los paréntesis ponemos el símbolo ->
* Por último, ponemos el tipo de retorno

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

## Operaciones intermedias de Stream

Las operaciones intermedias se aplican a un `Stream` y devuelven otro `Stream`, lo que permite encadenar múltiples operaciones.

### **filter(A-> Boolean)**

Sirve para quitar elementos de un stream que no cumplan una condición determinada. El método que se utiliza es filter y recibe como parámetro una función lambda (E) -> Boolean.

```java
Stream<String> stream = Arrays.asList("Juan", "María", "Carlos").stream();

stream
    // Esta lambda (String) -> Boolean, comprueba que el parámetro nombre empieza por J
    .filter(nombre -> nombre.startsWith("J"))
    // Muestra todos los elementos del stream resultante usando una lambda (String) -> Void
    .forEach(nombre -> System.out.println(nombre));
```

### map(A->B)

Se utiliza para **transformar** los elementos de un `Stream<A>` aplicando una función a cada elemento y devolviendo un nuevo `Stream<B>` con los elementos transformados. El número de elementos del Stream resultante es el mismo que en el Stream original, ya que simplemente se aplica una transformación a cada uno de ellos.

Toma como parámetro una función lambda `(A) -> B`, donde `A` es el tipo del Stream original y `B` el del Stream resultante.

<pre class="language-java"><code class="lang-java">// En este caso tenemos un  Stream para el que la A es String
Stream&#x3C;String> stream = Arrays.asList("Juan", "María", "Carlos").stream();
<strong>// El mapeo genera un Stream&#x3C;Integer> que luego es recolectado en una List&#x3C;Ingeger>
</strong><strong>List&#x3C;Integer> nameLengths = stream
</strong>    // Transformamos cada nombre en el número de caracteres que lo componen
    // La lambda que se aplica es String -> Integer
    // Este map devuelve un Stream&#x3C;Integer>
    .map(nombre -> nombre.length())
    // Ahora ejecutamos una operación terminal para que muestre todos los elementos del stream resultante
    .collect(Collectors.toList());
</code></pre>

### flatMap(A -> Stream\<B>)

Este método es de utilidad cuando la transformación que se va a aplicar a cada elemento del Stream produce una colección de valores.

Por ejemplo, si queremos obtener los tags de todos los productos de un Stream

```java
List<Product> products = Arrays.asList(
    new Product(1, "tornillo", new HashSet<>(Arrays.asList("Ferretería", "Tornillo"))),
    new Product(2, "tuerca", new HashSet<>(Arrays.asList("Ferretería", "Tuerca"))),
    new Product(3, "lápiz", new HashSet<>(Arrays.asList("Papelería")))
);

Set<Set<String>> tags = products
    .stream()
    .map(p -> p.getTags())
    .collect(Collectors.toSet());
    
System.out.println(tags);
```

Como podemos observar, si aplicamos el método map lo que obtenemos es un Set de Sets de tags, habrá un Set independiente por cada producto en el Stream original. Sin embargo, lo que queremos obtener es un Set\<String> con los tags de todos los productos.

Para poder hacer esto necesitamos el método `flatMap` que recibe una lambda (A) -> Stream\<B> .

```java
List<Product> products = Arrays.asList(
    new Product(1, "tornillo", new HashSet<>(Arrays.asList("Ferretería", "Tornillo"))),
    new Product(2, "tuerca", new HashSet<>(Arrays.asList("Ferretería", "Tuerca"))),
    new Product(3, "lápiz", new HashSet<>(Arrays.asList("Papelería")))
);

Set<String> tags = products
    .stream()
    .flatMap(p -> p.getTags().stream())
    .collect(Collectors.toSet());
    
System.out.println(tags);
```

### **sorted**

Los elementos de un `Stream` se pueden ordenar utilizando el método sorted de la siguiente manera

```java
Stream<String> stream = Arrays.asList("Juan", "María", "Carlos").stream();
// Ordenará los String en orden alfabético
stream
    .sorted();
    // Ahora ejecutamos una operación terminal para que muestre todos los elementos del stream resultante
    .forEach(nombre -> System.out.println(nombre));
```

También es posible especificar una ordenación distinta proviendo de un `Comparator<T>` al método sorted.

<pre class="language-java"><code class="lang-java"><strong>Stream&#x3C;String> stream = Arrays.asList("Juan", "María", "Carlos").stream();
</strong>// Ordenará los String en orden alfabético
stream
    // Pasamos un comparador que ordena de alguna otra forma
    .sorted(new ReverseStringComparator());
    // Ahora ejecutamos una operación terminal para que muestre todos los elementos del stream resultante
    .forEach(nombre -> System.out.println(nombre));
</code></pre>

También es posible expresar el `Comparator` como una Lambda (E, E) -> Integer

<pre class="language-java"><code class="lang-java"><strong>Stream&#x3C;String> stream = Arrays.asList("Juan", "María", "Carlos").stream();
</strong>// Ordenará los String en orden alfabético
stream
    // Expresamos el comparador con una Lambda (String, String) -> Integer
    .sorted((name1, name2) -> -name1.compareTo(name2));
    // Ahora ejecutamos una operación terminal para que muestre todos los elementos del stream resultante
    .forEach(nombre -> System.out.println(nombre));
</code></pre>

### **limit**

Este método hace el `Stream` resultante solo se quede con un número máximo de elementos

```java
Stream<String> stream = Arrays.asList("Juan", "María", "Carlos").stream();
// Ordenará los String en orden alfabético
stream
    // Nos quedamos con los dos primeros elementos
    .limit(2)
    // Ahora ejecutamos una operación terminal para que muestre todos los elementos del stream resultante
    .forEach(nombre -> System.out.println(nombre));
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
    .forEach(nombre -> System.out.println(nombre));
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

### reduce(A, (A, A) -> A)

Permite combinar los elementos del `Stream<T>` en un solo valor de tipo `Optional<T>`. Para ello, es necesario pasar una lambda `(T, T) -> T`, dicha función toma dos parámetros del tipo que contiene la colección y devuelve un único resultado del mismo tipo, esta función se aplica una y otra vez reduciendo el número de valores que contiene el Stream hasta obtener un único valor

Después de hacer un reduce, obtenemos un objeto de tipo Optional\<T>, este Optional indica que si el Stream estaba vacío no obtendremos ningún resultado.

```java
Stream<Integer> numbers = Arrays.asList(3, 4, 2, 5).stream();
// Se suman todos los números en numbers hasta obtener el total
Optional<Integer> sum = numbers.reduce((s1, s2) -> s1 + s2);
```

El resultado del `reduce` devolverá un `Optional.empty` cuando no hay ningún elemento en el stream al que se le aplica el reduce.&#x20;

```java
Stream<Integer> numbers = Arrays.asList().stream();
// sum es Optional.empty
Optional<Integer> sum = numbers.reduce((s1, s2) -> s1 + s2);
```

Es posible pasar un parámetro adicional al método reduce que consiste en un valor inicial que se aplicará a la primera operación de reducción que se aplique. Cuando se pasa este parámetro el resultado ya no es un Optional\<T> sino un T, ya que en caso de que el stream esté vacío se devolverá el elemento identidad.

```java
Stream<Integer> numbers = Arrays.asList(3, 4, 2, 5).stream();
// Se suman todos los números en numbers hasta obtener el total
//  identidad= 0, stream =(3, 4, 2, 5)
// reduce (0,3) = 3
// reduce (3, 4) = 7
// reduce (7,2) = 9
// reduce (9,5) = 14
// sum = 14
Integer sum = numbers.reduce(0, (s1, s2) -> s1 + s2);
```

El resultado del `reduce` devolverá el valor identidad cuando no hay ningún elemento en el stream al que se le aplica el reduce.&#x20;

```java
Stream<Integer> numbers = Arrays.asList().stream();
// sum es 0
Integer sum = numbers.reduce(0, (s1, s2) -> s1 + s2);
```

### **foreach(A -> Void)**

Esta operación terminal recibe una lambda (A) -> Void, es decir no devuelve nada. Se suele utilizar para mostrar datos en pantall, modificar algún objeto definido en el scope en el que se ejecuta... &#x20;

```java
// Ejemplo de uso de forEach para mostrar datos en pantalla
Stream<String> names = Arrays.asList("Juan", "María", "Carlos").stream();
names.forEach(name -> System.out.println(name));
```

<pre class="language-java"><code class="lang-java">// Ejemplo de uso de forEach para concatenar los nombres separados por comas
Stream&#x3C;String> names = Arrays.asList("Juan", "María", "Carlos").stream();
<strong>// Para poder acceder a sentence desde la lambda, debe ser final
</strong><strong>final StringBuilder sentence = new StringBuilder();
</strong>
// Añadimos a sentence cada nombre, separando con un espacio
names.forEach(name -> sentence.append(" " + name));

System.out.println(sentence.toString());
</code></pre>

### **findFirst()**

```java
// Devuelve un Optional con el primer elemento del stream
// Si el stream está vacío, devuelve Optional.empty
Optional<String> firstElement = stream.findFirst();
```

### **max( (A,A) -> A )**

```java
// Devuelve un Optional con el nif más alto, ordenado alfabéticamente
Optional<Student> maxNifStudent = stream
    .max((student1, student2) -> student1.getNif().compareTo(student2.getNif()));
```

### **min( (A,A) -> A )**

```java
// Devuelve un Optional con el nif más bajo, ordenado alfabéticamente
Optional<Student> minNifStudent = stream
    .min((student1, student2) -> student1.getNif().compareTo(student2.getNif()));
```
