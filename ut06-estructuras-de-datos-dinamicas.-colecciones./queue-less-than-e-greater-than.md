---
cover: ../.gitbook/assets/tree.png
coverY: 94.60266666666666
---

# Queue\<E>

Una cola (Queue) en Java es una estructura de datos que sigue el principio FIFO (First-In, First-Out), lo que significa que el primer elemento agregado a la cola será el primero en ser eliminado. La interfaz `Queue` en Java es parte del paquete `java.util` y proporciona una serie de métodos para realizar operaciones comunes en una cola. Aquí hay una descripción de algunos de los métodos más comunes en la interfaz `Queue`:

1. **add(E elemento)**: Agrega un elemento al final de la cola. Si la cola no puede aceptar el elemento, lanzará una excepción (`IllegalStateException` o `NullPointerException` si la cola no permite elementos `null`).
2. **poll()**: Elimina y devuelve el elemento en la cabeza de la cola. Si la cola está vacía, devuelve `null`.
3. **peek()**: Devuelve el elemento en la cabeza de la cola sin eliminarlo. Si la cola está vacía, devuelve `null`.
4. **isEmpty()**: Devuelve `true` si la cola está vacía, de lo contrario, devuelve `false`.
5. **size()**: Devuelve el número de elementos presentes en la cola.

<figure><img src="../.gitbook/assets/image (1) (1).png" alt=""><figcaption><p>Firt In First Out en una cola</p></figcaption></figure>

Estos son solo algunos de los métodos proporcionados por la interfaz `Queue`. La elección de qué método usar depende de tus necesidades específicas. Es importante tener en cuenta que `Queue` es una interfaz, por lo que necesitarás una clase que la implemente, como `LinkedList` o `PriorityQueue`.

La clase `LinkedList` implementa la interfaz `Queue` y es una elección común para implementar colas en Java debido a su eficiencia en la inserción y eliminación de elementos al principio y al final de la lista.

La clase `PriorityQueue` también implementa la interfaz `Queue`, pero ordena los elementos en función de un comparador o del orden natural de los elementos (si son comparables).

En resumen, la interfaz `Queue` en Java proporciona una estructura de datos conveniente para trabajar con datos en un orden específico y ofrece una variedad de métodos para agregar, eliminar y consultar elementos en la cola.

```java
import java.util.Queue;
import java.util.concurrent.ArrayBlockingQueue;

public class QueueExample {
    public static void main(String[] args) {
        // Creamos una cola utilizando ArrayBlockingQueue con capacidad de almacenar 10 valores
        Queue<String> cola = new ArrayBlockingQueue<>(10);

        // Agregamos elementos a la cola
        cola.offer("Elemento 1");
        cola.offer("Elemento 2");
        cola.offer("Elemento 3");

        // Mostramos los elementos de la cola
        System.out.println("Elementos en la cola:");
        for (String elemento : cola) {
            System.out.println(elemento);
        }

        // Eliminamos un elemento de la cola
        String elementoEliminado = cola.poll();
        System.out.println("Elemento eliminado: " + elementoEliminado);

        // Mostramos el primer elemento de la cola sin eliminarlo
        String primerElemento = cola.peek();
        System.out.println("Primer elemento de la cola: " + primerElemento);

        // Mostramos el tamaño de la cola
        System.out.println("Tamaño de la cola: " + cola.size());

        // Verificamos si la cola está vacía
        if (cola.isEmpty()) {
            System.out.println("La cola está vacía");
        } else {
            System.out.println("La cola no está vacía");
        }
    }
}
```
