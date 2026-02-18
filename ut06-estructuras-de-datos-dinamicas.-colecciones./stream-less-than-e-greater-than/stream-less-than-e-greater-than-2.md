---
cover: ../../.gitbook/assets/lambda.jpeg
coverY: 0
---

# Operaciones intermedias

Las operaciones intermedias se aplican a un `Stream` y devuelven otro `Stream`, lo que permite encadenar múltiples operaciones.

## **`Stream<A> filter(A-> Boolean)`**

Sirve para quitar elementos de un stream que no cumplan una condición determinada. El método que se utiliza es `filter` y recibe como parámetro una función lambda `(E) -> Boolean`.

<pre class="language-java"><code class="lang-java">List&#x3C;String> names = List.of("Juan", "María", "Carlos");

names
    .stream()
    // Esta lambda (String) -> Boolean, comprueba que el parámetro nombre empieza por J
<strong>    .filter(nombre -> nombre.startsWith("J"))
</strong>    // Muestra todos los elementos del stream resultante usando una lambda (String) -> Void
    .forEach(nombre -> System.out.println(nombre));
</code></pre>

## `Stream<B> map(A->B)`

Se utiliza para **transformar** los elementos de un `Stream<A>` aplicando una función a cada elemento y devolviendo un nuevo `Stream<B>` con los elementos transformados. El número de elementos del `Stream` resultante es el mismo que en el `Stream` original, ya que simplemente se aplica una transformación a cada uno de ellos.

Toma como parámetro una función lambda `(A) -> B`, donde `A` es el tipo del `Stream` original y `B` el del `Stream` resultante.

<pre class="language-java"><code class="lang-java">// En este caso tenemos una List para el que la A es String
List&#x3C;String> names = List.of("Juan", "María", "Carlos");
// El mapeo genera un Stream&#x3C;Integer> que luego es recolectado en una List&#x3C;Ingeger>
List&#x3C;Integer> nameLengths = names
    .stream()
    // Transformamos cada nombre en el número de caracteres que lo componen
    // La lambda que se aplica es String -> Integer
    // Este map devuelve un Stream&#x3C;Integer>
<strong>    .map(nombre -> nombre.length())
</strong>    // Ahora ejecutamos una operación terminal para que muestre todos los elementos del stream resultante
    .collect(Collectors.toList());
</code></pre>

## `Stream<B> flatMap(A -> Stream<B>)`

Este método es de utilidad cuando la transformación que se va a aplicar a cada elemento del `Stream` produce una colección de valores.

Por ejemplo, si queremos obtener los tags de todos los productos de un `Stream`

<pre class="language-java"><code class="lang-java">List&#x3C;Product> products = List.of(
    new Product(1, "tornillo", Set.of("Ferretería", "Tornillo")),
    new Product(2, "tuerca", Set.of("Ferretería", "Tuerca")),
    new Product(3, "lápiz", Set.of("Papelería"))
);

<strong>Set&#x3C;Set&#x3C;String>> tags = products
</strong>    .stream()
<strong>    .map(p -> p.getTags())
</strong>    .collect(Collectors.toSet());
    
System.out.println(tags);
</code></pre>

Como podemos observar, si aplicamos el método `map` lo que obtenemos es un `Set` de `Set` de tags, habrá un `Set` independiente por cada producto en el `Stream` original. Sin embargo, lo que queremos obtener es un `Set<String>` con los tags de todos los productos.

Para poder hacer esto necesitamos el método `flatMap` que recibe una lambda `(A) -> Stream<B>` .

<pre class="language-java"><code class="lang-java">List&#x3C;Product> products = List.of(
    new Product(1, "tornillo", Set.of("Ferretería", "Tornillo")),
    new Product(2, "tuerca", Set.of("Ferretería", "Tuerca")),
    new Product(3, "lápiz", Set.of("Papelería"))
);

<strong>Set&#x3C;String> tags = products
</strong>    .stream()
    // Aquí la B es String
<strong>    .flatMap(p -> p.getTags().stream())
</strong>    .collect(Collectors.toSet());
    
System.out.println(tags);
</code></pre>

## **`Stream<A> sorted()`**

Los elementos de un `Stream` se pueden ordenar utilizando el método `sorted` de la siguiente manera

<pre class="language-java"><code class="lang-java">List&#x3C;String> names = List.of("Juan", "María", "Carlos");
// Ordenará los String en orden alfabético
names
    .stream()
<strong>    .sorted()
</strong>    // Ahora ejecutamos una operación terminal para que muestre todos los elementos del stream resultante
    .forEach(nombre -> System.out.println(nombre));
</code></pre>

También es posible especificar una ordenación distinta proviendo de un `Comparator<T>` al método sorted.

<pre class="language-java"><code class="lang-java"><strong>List&#x3C;String> names = List.of("Juan", "María", "Carlos");
</strong>// Ordenará los String en orden alfabético
names
    .stream()
    // Pasamos un comparador que ordena de alguna otra forma
<strong>    .sorted(new ReverseStringComparator())
</strong>    // Ahora ejecutamos una operación terminal para que muestre todos los elementos del stream resultante
    .forEach(nombre -> System.out.println(nombre));
</code></pre>

También es posible expresar el `Comparator` como una Lambda `(E, E) -> Integer`

<pre class="language-java"><code class="lang-java"><strong>List&#x3C;String> names = List.of("Juan", "María", "Carlos");
</strong>// Ordenará los String en orden alfabético
names
    .stream()
    // Expresamos el comparador con una Lambda (String, String) -> Integer
<strong>    .sorted((name1, name2) -> -name1.compareTo(name2))
</strong>    // Ahora ejecutamos una operación terminal para que muestre todos los elementos del stream resultante
    .forEach(nombre -> System.out.println(nombre));
</code></pre>

## **`Stream<A> limit(int)`**

Este método hace el `Stream` resultante solo se quede con un número máximo de elementos

<pre class="language-java"><code class="lang-java">List&#x3C;String> names = List.of("Juan", "María", "Carlos");
names
    .stream()
    // Nos quedamos con los dos primeros elementos
<strong>    .limit(2)
</strong>    // Ahora ejecutamos una operación terminal para que muestre todos los elementos del stream resultante
    .forEach(nombre -> System.out.println(nombre));
</code></pre>

## **`Stream<A> skip(int)`**

Este método hace que el `Stream` resultante se salte un número determinado de elementos

<pre class="language-java"><code class="lang-java">List&#x3C;String> names = List.of("Juan", "María", "Carlos");
names
    .stream()
    // Nos saltamos los dos primeros elementos
<strong>    .skip(2)
</strong>    // Ahora ejecutamos una operación terminal para que muestre todos los elementos del stream resultante
    .forEach(nombre -> System.out.println(nombre));
</code></pre>
