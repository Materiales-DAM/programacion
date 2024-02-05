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

# Set\<E>

Las colecciones de tipo Set representan conjuntos de datos. No es posible definir el orden (o secuencia) en el que se encuentran dichos datos dentro de la colección sino que viene predefinida dependiendo de la misma)

<figure><img src="../.gitbook/assets/image (15).png" alt=""><figcaption><p>Un set es un conjunto de valores no secuenciales</p></figcaption></figure>

Algunas de las características de los Set son:

* Sirven para almacenar **datos no secuenciales**. &#x20;
* Cada instancia de un Set define el tipo de valores que almacena a través del parámetro de tipo E.&#x20;
* No es posible almacenar elementos repetidos.&#x20;
* Son colecciones optimizadas para buscar datos de forma eficiente.&#x20;
* Al no ser una secuencia, los elementos que alberga no tienen una posición (o índice) asociada.
* La ordenación interna de los datos depende del tipo de Set

## Métodos

* **add(E elemento)**: Este método agrega un elemento al conjunto si el conjunto no contiene ya el elemento. Devuelve `true` si el conjunto cambió como resultado de la llamada, es decir, si el elemento no estaba presente antes, y `false` si el conjunto ya contenía el elemento.
* **remove(Object objeto)**: Elimina un elemento específico del conjunto si está presente. Devuelve `true` si el conjunto contenía el elemento especificado.
* **contains(Object objeto)**: Comprueba si el conjunto contiene un elemento específico. Devuelve `true` si el conjunto contiene el elemento especificado.
* **size()**: Devuelve el número de elementos en el conjunto.
* **isEmpty()**: Devuelve `true` si el conjunto no contiene elementos.
* **clear()**: Elimina todos los elementos del conjunto.
* **addAll(Collection\<? extends E> coleccion)**: Agrega todos los elementos de una colección dada al conjunto.
* **removeAll(Collection\<?> coleccion)**: Elimina todos los elementos del conjunto que están contenidos en la colección especificada.

## Recorrer un Set

Debido a que los Set no mantienen un índice o un orden específico de los elementos que contienen, no es posible recorrerlos con un bucle for al uso.

```java
Set<Integer> numbers = new TreeSet<>();
numbers.add(-4);
numbers.add(3);
numbers.add(77);
numbers.add(90);

// El tamaño del Set se obtiene invocando el método size()
for(int i = 0; i < numbers.size(); i++) {
    // Esta línea no compila, no existe el método get de la posición i en los Set
    int number = numbers.get(i);
    System.out.println(number);
} 
```

La única opción para recorrer un Set con un bucle for-each

```java
Set<Integer> numbers = new HashSet<>();
numbers.add(-4);
numbers.add(3);
numbers.add(77);
numbers.add(90);

for(int number: numbers) {
    System.out.println(number);
} 
```

Si ejecutamos el código anterior veremos que el orden en el que aparecen los número no coincide con el orden en el que fueron insertados.

```
-4
3
90
77
```

## Implementaciones

### HashSet\<E>

lista

### TreeSet\<E>



