---
cover: ../.gitbook/assets/lambda.jpeg
coverY: 0
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
import java.util.List;

public class Main {
    public static void main(String[] args) {
        List<Integer> numeros = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

        numeros.stream()
               .filter(n -> n % 2 == 0)  // Filtrar números pares
               .map(n -> n * 2)           // Duplicar cada número
               .forEach(n -> System.out.println(n));  // Imprimir los resultados
    }
}
```

En este ejemplo, `numeros.stream()` se crea un stream a partir de la lista de números. Luego, llamamos a `filter()` para mantener solo los números pares, después usamos `map()` para duplicar cada número y finalmente usamos `forEach()` para imprimir los resultados. Todas las operaciones intermedias se están expresando a través de una construcción denominada Lambda
