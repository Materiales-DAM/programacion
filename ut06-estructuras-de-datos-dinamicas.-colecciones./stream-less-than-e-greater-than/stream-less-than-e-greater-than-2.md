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

# Operaciones intermedias

Las operaciones intermedias se aplican a un `Stream` y devuelven otro `Stream`, lo que permite encadenar múltiples operaciones.

## **Stream\<A> filter(A-> Boolean)**

Sirve para quitar elementos de un stream que no cumplan una condición determinada. El método que se utiliza es filter y recibe como parámetro una función lambda (E) -> Boolean.

```java
List<String> names = List.of("Juan", "María", "Carlos");

names
    .stream()
    // Esta lambda (String) -> Boolean, comprueba que el parámetro nombre empieza por J
    .filter(nombre -> nombre.startsWith("J"))
    // Muestra todos los elementos del stream resultante usando una lambda (String) -> Void
    .forEach(nombre -> System.out.println(nombre));
```

## Stream\<B> mmap(A->B)

Se utiliza para **transformar** los elementos de un `Stream<A>` aplicando una función a cada elemento y devolviendo un nuevo `Stream<B>` con los elementos transformados. El número de elementos del Stream resultante es el mismo que en el Stream original, ya que simplemente se aplica una transformación a cada uno de ellos.

Toma como parámetro una función lambda `(A) -> B`, donde `A` es el tipo del Stream original y `B` el del Stream resultante.

<pre class="language-java"><code class="lang-java">// En este caso tenemos una List para el que la A es String
List&#x3C;String> names = List.of("Juan", "María", "Carlos");
<strong>// El mapeo genera un Stream&#x3C;Integer> que luego es recolectado en una List&#x3C;Ingeger>
</strong><strong>List&#x3C;Integer> nameLengths = stream
</strong><strong>    .stream()
</strong>    // Transformamos cada nombre en el número de caracteres que lo componen
    // La lambda que se aplica es String -> Integer
    // Este map devuelve un Stream&#x3C;Integer>
    .map(nombre -> nombre.length())
    // Ahora ejecutamos una operación terminal para que muestre todos los elementos del stream resultante
    .collect(Collectors.toList());
</code></pre>

## Stream\<B> flatMap(A -> Stream\<B>)

Este método es de utilidad cuando la transformación que se va a aplicar a cada elemento del Stream produce una colección de valores.

Por ejemplo, si queremos obtener los tags de todos los productos de un Stream

```java
List<Product> products = List.of(
    new Product(1, "tornillo", Set.of("Ferretería", "Tornillo")),
    new Product(2, "tuerca", Set.of("Ferretería", "Tuerca")),
    new Product(3, "lápiz", Set.of("Papelería"))
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
List<Product> products = List.of(
    new Product(1, "tornillo", Set.of("Ferretería", "Tornillo")),
    new Product(2, "tuerca", Set.of("Ferretería", "Tuerca")),
    new Product(3, "lápiz", Set.of("Papelería"))
);

Set<String> tags = products
    .stream()
    // Aquí la B es String
    .flatMap(p -> p.getTags().stream())
    .collect(Collectors.toSet());
    
System.out.println(tags);
```

## **Stream\<A> sorted()**

Los elementos de un `Stream` se pueden ordenar utilizando el método sorted de la siguiente manera

```java
List<String> names = List.of("Juan", "María", "Carlos");
// Ordenará los String en orden alfabético
names
    .stream()
    .sorted();
    // Ahora ejecutamos una operación terminal para que muestre todos los elementos del stream resultante
    .forEach(nombre -> System.out.println(nombre));
```

También es posible especificar una ordenación distinta proviendo de un `Comparator<T>` al método sorted.

<pre class="language-java"><code class="lang-java"><strong>List&#x3C;String> names = List.of("Juan", "María", "Carlos");
</strong>// Ordenará los String en orden alfabético
names
    .stream()
    // Pasamos un comparador que ordena de alguna otra forma
    .sorted(new ReverseStringComparator());
    // Ahora ejecutamos una operación terminal para que muestre todos los elementos del stream resultante
    .forEach(nombre -> System.out.println(nombre));
</code></pre>

También es posible expresar el `Comparator` como una Lambda (E, E) -> Integer

<pre class="language-java"><code class="lang-java"><strong>List&#x3C;String> names = List.of("Juan", "María", "Carlos");
</strong>// Ordenará los String en orden alfabético
names
    .stream()
    // Expresamos el comparador con una Lambda (String, String) -> Integer
    .sorted((name1, name2) -> -name1.compareTo(name2));
    // Ahora ejecutamos una operación terminal para que muestre todos los elementos del stream resultante
    .forEach(nombre -> System.out.println(nombre));
</code></pre>

## **Stream\<A> limit(int)**

Este método hace el `Stream` resultante solo se quede con un número máximo de elementos

```java
List<String> names = List.of("Juan", "María", "Carlos");
names
    .stream()
    // Nos quedamos con los dos primeros elementos
    .limit(2)
    // Ahora ejecutamos una operación terminal para que muestre todos los elementos del stream resultante
    .forEach(nombre -> System.out.println(nombre));
```

## **Stream\<A> skip(int)**

Este método hace que el `Stream` resultante se salte un número determinado de elementos

```java
List<String> names = List.of("Juan", "María", "Carlos");
names
    .stream()
    // Nos saltamos los dos primeros elementos
    .skip(2)
    // Ahora ejecutamos una operación terminal para que muestre todos los elementos del stream resultante
    .forEach(nombre -> System.out.println(nombre));
```
