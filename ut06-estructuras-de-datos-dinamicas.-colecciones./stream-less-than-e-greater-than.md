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

Los `Stream` en Java son una característica introducida en Java 8 que permite realizar operaciones de procesamiento de datos de forma declarativa y funcional en colecciones de elementos. Los `Stream` permiten expresar operaciones como filtrado, mapeo, reducción y agrupación de manera más concisa y legible que los enfoques tradicionales.

Aquí tienes un tutorial detallado sobre cómo trabajar con `Stream` en Java:

#### 1. Creación de Streams:

Puedes crear un Stream a partir de diferentes fuentes de datos, como colecciones, arreglos o métodos de generación.

**a. Desde colecciones:**

```java
javaCopy codeList<String> myList = Arrays.asList("a", "b", "c", "d");

Stream<String> stream = myList.stream();
```

**b. Desde arreglos:**

```java
javaCopy codeString[] array = {"a", "b", "c", "d"};

Stream<String> stream = Arrays.stream(array);
```

**c. Métodos de generación:**

```java
javaCopy codeStream<String> generatedStream = Stream.generate(() -> "elemento").limit(5);
```

#### 2. Operaciones Intermedias:

Las operaciones intermedias se aplican a un `Stream` y devuelven otro `Stream`, lo que permite encadenar múltiples operaciones.

**a. Filtrado:**

```java
javaCopy codestream.filter(s -> s.startsWith("a"));
```

**b. Mapeo:**

```java
javaCopy codestream.map(String::toUpperCase);
```

**c. Ordenamiento:**

```java
javaCopy codestream.sorted();
```

**d. Limitar:**

```java
javaCopy codestream.limit(5);
```

**e. Saltar:**

```java
javaCopy codestream.skip(2);
```

#### 3. Operaciones Terminales:

Las operaciones terminales producen un resultado final o llevan a cabo una acción final, y después de que se haya aplicado una operación terminal, el `Stream` ya no puede ser utilizado.

**a. Recolección:**

```java
javaCopy codeList<String> resultList = stream.collect(Collectors.toList());
```

**b. Reducción:**

```java
javaCopy codeOptional<String> reduced = stream.reduce((s1, s2) -> s1 + s2);
```

**c. Iteración:**

```java
javaCopy codestream.forEach(System.out::println);
```

**d. Encontrar primer elemento:**

```java
javaCopy codeOptional<String> firstElement = stream.findFirst();
```

#### 4. Encadenamiento de Operaciones:

Puedes encadenar múltiples operaciones intermedias y terminales para formar una secuencia de operaciones.

```java
javaCopy codeList<String> result = myList.stream()
                            .filter(s -> s.startsWith("a"))
                            .map(String::toUpperCase)
                            .collect(Collectors.toList());
```

#### 5. Operaciones Paralelas:

Los Streams en Java 8 también admiten operaciones paralelas, lo que permite el procesamiento simultáneo de elementos.

```java
javaCopy codeList<String> result = myList.parallelStream()
                            .filter(s -> s.startsWith("a"))
                            .collect(Collectors.toList());
```

#### 6. Cierre Automático:

Los Streams pueden cerrarse automáticamente al final de las operaciones terminales.

#### 7. Evitar Efectos Secundarios:

Los Streams favorecen un estilo de programación funcional y desalientan el uso de efectos secundarios.

#### Conclusión:

Los `Stream` en Java proporcionan una forma potente y elegante de realizar operaciones de procesamiento de datos en colecciones. Con un código más conciso y legible, los Streams permiten expresar transformaciones y operaciones de datos de manera más intuitiva y eficiente. Es importante comprender las operaciones intermedias y terminales, así como también cómo pueden encadenarse y combinarse para lograr el comportamiento deseado. Además, la capacidad de procesamiento paralelo proporciona un aumento significativo en el rendimiento para conjuntos de datos grandes.
