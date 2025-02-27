---
cover: ../../.gitbook/assets/lambda.jpeg
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

# Operaciones terminales

Las operaciones terminales producen un resultado final o llevan a cabo una acción final, y después de que se haya aplicado una operación terminal, el `Stream` ya no puede ser utilizado.

## **collect**

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

## reduce(A, (A, A) -> A)

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

## **foreach(A -> Void)**

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

## **findFirst()**

```java
// Devuelve un Optional con el primer elemento del stream
// Si el stream está vacío, devuelve Optional.empty
Optional<String> firstElement = stream.findFirst();
```

## **max( (A,A) -> A )**

```java
// Devuelve un Optional con el nif más alto, ordenado alfabéticamente
Optional<Student> maxNifStudent = stream
    .max((student1, student2) -> student1.getNif().compareTo(student2.getNif()));
```

## **min( (A,A) -> A )**

```java
// Devuelve un Optional con el nif más bajo, ordenado alfabéticamente
Optional<Student> minNifStudent = stream
    .min((student1, student2) -> student1.getNif().compareTo(student2.getNif()));
```
