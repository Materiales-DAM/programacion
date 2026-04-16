---
cover: ../../.gitbook/assets/algorithm.jpg
coverY: 3.437014262938337
layout:
  width: default
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
  metadata:
    visible: true
  tags:
    visible: true
---

# Ordenación por burbuja

Imagina un acuario con burbujas de aire dentro del agua: las más ligeras ascienden hacia la superficie empujando a las más pesadas hacia el fondo. En una pasada, la burbuja más ligera de todas termina arriba. En pasadas sucesivas, las siguientes van subiendo.

Trasladado a un array de números:

* Recorremos el array comparando **elementos adyacentes**.
* Si están desordenados (el de la izquierda es mayor que el de la derecha, para orden ascendente), los **intercambiamos**.
* Tras una pasada completa, el **elemento mayor** queda garantizadamente al final.
* Repetimos con n - 1 veces.

El nombre viene precisamente de que los elementos grandes "burbujean" hacia el final (o, si lo miras al revés, los pequeños van subiendo hacia el principio).

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

## Ejercicios

1. Implementa un método `int[] bubbleSort(int[] numbers)` que dado un array de enteros lo devuelva ordenado de menor a mayor. La ordenación se debe hacer en el propio array de entrada, que es el mismo que se devuelve.
2.  Implementa un método `Student[] bubbleSort(Student[] numbers)` que dado un array de Student lo devuelva ordenado por apellidos y luego por nombre.  La ordenación se debe hacer en el propio array de entrada, que es el mismo que se devuelve.<br>

    ```java
    @Data
    public class Student{
        private String name;
        private String surname
    }
    ```
3. Realiza las siguientes optimizaciones sobre el ejercicio 1:
   1. Adaptabilidad: si el array ya está ordenado en una pasada, ya ha terminado. Si durante una pasada no se ha hecho ningún intercambio es que ya está ordenado
   2. La primera pasada deja el número de mayor tamaño en la última posición, la segunda al siguiente en la penúltima... entonces no es necesario comprobar últimas posiciones que ya sabemos que están ordenadas

