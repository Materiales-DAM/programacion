---
cover: ../../.gitbook/assets/tree.png
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

# List\<E>

El ADT List define los métodos que deben implementar las colecciones que sirvan para representar una **secuencia de elementos**. En este tipo de colecciones **cada elemento tiene un índice** asociado que indica su posición en la lista.&#x20;

Por tanto, las listas son estructuras de datos que permite almacenar una **secuencia de elementos** y acceder a ellos mediante su posición relativa dentro de la lista (índice).

El interfaz List define un tipo genérico E que hace referencia al tipo de los elementos que almacena la lista.

```java
// Definimos una lista de cadenas de caracteres
List<String> listOfStrings = new LinkedList<>();
// Definimos una lista de enteros
List<Integer> listOfInts = new LinkedList<>();
```

## Métodos

* `add(E element)`: Agrega un elemento al final de la lista.
* `add(int index, E element)`: Agrega un elemento en una posición específica de la lista.
* `get(int index)`: Devuelve el elemento en la posición especificada de la lista.
* `remove(int index)`: Elimina el elemento en la posición especificada de la lista.
* `size()`: Devuelve el número de elementos en la lista.
* `isEmpty()`: Devuelve `true` si la lista está vacía, `false` de lo contrario.
* `contains(Object o)`: Devuelve `true` si la lista contiene el elemento especificado, `false` de lo contrario.
* `indexOf(Object o)`: Devuelve el índice de la primera ocurrencia del elemento especificado en la lista.

## Recorrer una lista

De forma similiar a como se hacía con los arrays, podemos recorrer una lista usando un bucle for que va iterando sobre la misma usando el índice (i).

```java
List<Integer> numbers = new LinkedList<>();
numbers.add(4);
numbers.add(3);
numbers.add(7);
numbers.add(9);

// El tamaño de la lista se obtiene invocando el método size(), en vez de lenght
for(int i = 0; i < numbers.size(); i++) {
    // Para sacar el valor en la posición i usamos el método get(i)
    int number = numbers.get(i);
    System.out.println(number);
} 
```

También es posible recorrer las listas con un for-each

```java
List<Integer> numbers = new ArrayList<>();
numbers.add(4);
numbers.add(3);
numbers.add(7);
numbers.add(9);

for(int number: numbers) {
    System.out.println(number);
} 
```

## Implementaciones

Los ADT son interfaces para los que la libería de colecciones de Java tiene varias implementaciones. Cada implementación presenta una serie de ventajas y desventajas con respecto a las demás. La elección de la colección más adecuada puede ser determinante en la eficiencia del programa resultante.

Las dos implementaciones más importantes de List son **ArrayList** y **LinkedList**.

### LinkedList\<E>

Es una implementación basada en la estructura de datos "**Lista enlazada**". Se trata  de una estructura de datos dinámica, es decir, adapta su tamaño a la cantidad de datos que se van añadiendo o quitando.&#x20;

```java
List<Integer> numbers = new LinkedList<>();
numbers.add(4);
numbers.add(3);
numbers.add(7);
numbers.add(9);

```

Las listas enlazadas almacenan los datos en **nodos**, cada nodo tiene un enlace al siguiente nodo de la lista.  La lista enlazada mantiene un enlace al primer nodo (head) y otro enlace al último (tail) para poder acceder a estas posiciones directamente.&#x20;

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption><p>LIsta enlazada con los números 10, 20 y 30</p></figcaption></figure>

Estas estructuras están optimizadas para insertar y quitar elementos de forma dinámica. No resultan tan convenientes para acceder a elementos por su índice, buscar un elemento u ordenarlos.

### ArrayList\<E>

Son estructuras de datos dinámicas, es decir, adaptan su tamaño a la cantidad de datos que se van añadiendo o quitando. Internamente utilizan arrays para almacenar los datos.&#x20;

```java
List<Integer> numbers = new ArrayList<>();
numbers.add(4);
numbers.add(3);
numbers.add(7);
numbers.add(9);
```

Su principal ventaja es que es posible leer cualquier posición muy rápidamente al tener acceso directo gracias al array. La desventaja es que resultan lentos a la hora de insertar y eliminar elementos ya que se hace necesario mover los datos por el array. Incluso en el peor de los casos si el tamaño del array es sobrepasado se necesita crear un nuevo array de mayor tamaño y copiar los datos al nuevo array.

## Eficiencia

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption><p>Eficiencia de LinkedLIst vs ArrayList</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption><p>Notación Big-O</p></figcaption></figure>

## LinkedList vs ArrayList

La elección entre `ArrayList` y `LinkedList` en Java depende de varios factores, incluyendo el tipo de operaciones que realizarás con la lista, el rendimiento esperado y los requisitos específicos de tu aplicación. Aquí hay algunas consideraciones para ayudarte a decidir cuándo usar `ArrayList` o `LinkedList`:

1. **Acceso por índice**:
   * Si necesitas un acceso rápido a elementos por índice, `ArrayList` es generalmente más eficiente. Esto se debe a que `ArrayList` almacena elementos en un array subyacente, lo que permite un acceso aleatorio a los elementos en tiempo constante.
   * Por otro lado, `LinkedList` no es tan eficiente para acceder a elementos por índice. Para acceder a un elemento en una posición específica, `LinkedList` debe recorrer la lista desde el principio o desde el final hasta alcanzar la posición deseada, lo que lleva tiempo lineal.
2. **Inserción y eliminación**:
   * `LinkedList` es más eficiente para inserciones y eliminaciones frecuentes en cualquier posición de la lista, especialmente cuando se trata de operaciones en el medio de la lista. Esto se debe a que `LinkedList` no requiere desplazamiento de elementos cuando se inserta o elimina un elemento en el medio de la lista, ya que cada elemento en `LinkedList` está enlazado con el siguiente y el anterior.
   * En contraste, `ArrayList` puede ser menos eficiente para inserciones y eliminaciones en posiciones intermedias, ya que puede requerir desplazar elementos en el array subyacente.
3. **Uso de memoria**:
   * `ArrayList` tiende a ocupar menos memoria que `LinkedList` debido a que `ArrayList` solo necesita almacenar los elementos en un array subyacente, mientras que `LinkedList` debe almacenar referencias a nodos enlazados, lo que puede ocupar más espacio.
   * Además, `ArrayList` no incurre en la sobrecarga de almacenar referencias de nodos adicionales como lo hace `LinkedList`.

En resumen, aquí hay algunas pautas generales:

* Usa `ArrayList` cuando necesites un acceso rápido a elementos por índice y cuando la mayoría de las operaciones involucren acceso y modificación al final de la lista.
* Usa `LinkedList` cuando necesites realizar inserciones y eliminaciones frecuentes en posiciones intermedias de la lista y cuando no necesites acceder a elementos por índice con tanta frecuencia.

En muchos casos, `ArrayList` es la opción que se elige de manera predeterminada debido a su rendimiento general y su eficiencia en el uso de memoria. Sin embargo, siempre es importante evaluar los requisitos específicos de la aplicación para determinar la mejor opción.
