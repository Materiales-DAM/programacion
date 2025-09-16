---
cover: ../.gitbook/assets/tree.png
coverY: 94.60266666666666
---

# Iteradores

Un iterador es un objeto que permite recorrer una colección de elementos de manera secuencial. Proporciona métodos para acceder y manipular los elementos de la colección sin exponer la estructura interna de la misma. Los iteradores son ampliamente utilizados en Java para recorrer colecciones como listas, conjuntos y mapas.

La interfaz principal que define un iterador en Java es `java.util.Iterator`. Esta interfaz define los siguientes métodos principales:

1. `boolean hasNext()`: Este método verifica si todavía hay elementos por recorrer en la colección. Devuelve `true` si hay más elementos, y `false` si no los hay.
2. `E next()`: Este método devuelve el próximo elemento en la iteración y avanza el iterador hacia adelante en la colección. Si no hay más elementos, este método lanzará una excepción de tipo `NoSuchElementException`.
3. `void remove()`: Este método elimina el último elemento devuelto por el iterador de la colección. No todos los iteradores admiten esta operación. Si el iterador no admite la operación de eliminación o si la colección ha sido modificada de manera inesperada (fuera del iterador), este método lanzará una excepción de tipo `IllegalStateException`.

Aquí tienes un ejemplo simple de cómo se podría usar un iterador para recorrer una lista en Java:

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("Uno");
        list.add("Dos");
        list.add("Tres");

        // Obtener un iterador para la lista
        Iterator<String> iterator = list.iterator();

        // Recorrer la lista utilizando el iterador
        while (iterator.hasNext()) {
            String elem = iterator.next();
            System.out.println(elem);
        }
    }
}
```

En este ejemplo, creamos una lista de String y la llenamos con algunos elementos. Luego obtenemos un iterador para esta lista usando el método `iterator()`. Finalmente, recorremos la lista usando un bucle `while`, verificando si el iterador ha llegado al último elemento con el método`hasNext()` y obteniendo el próximo elemento con `next()`.
