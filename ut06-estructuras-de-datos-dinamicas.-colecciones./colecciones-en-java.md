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

# Colecciones en Java

El lenguaje de programación Java incluye una extensa librería de estructuras de datos llamada Java Collections (colecciones Java).&#x20;

Cada tipo concreto de colección implementa una determinada estructura de datos que está optimizada para un conjunto determinado de operaciones.

Además, las colecciones se agrupan en **Tipos Abstractos de datos (ADTs por sus siglas en inglés)** que son interfaces genéricos que definen un conjunto de operaciones que se pueden realizar sobre una colección.

## Abstract Data Types (ADT)

<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption><p>Jerarquía de colecciones en Java</p></figcaption></figure>

### List\<E>

Se caracterizan por almacenar datos de manera **secuencial**, es decir, en un orden determinado que no viene dado por el dato en sí sino por cómo han sido insertados en la colección.  En estas colecciones se **permite la repetición de elementos**. Su principal utilidad viene relacionada con datos en los que se quiere mantener un orden dado y/o puede haber repetición de datos.&#x20;

Por ejemplo, una lista de comentarios que se ha hecho en un post de Facebook, queremos que queden en el orden en el que se hicieron.

<figure><img src="../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

Algunas de las características de los List son:

* Sirven para almacenar datos secuenciales
* Permiten la repetición de datos
* Cada instancia de un List define el tipo de valores que almacena a través del parámetro de tipo E.
* Sirven para almacenar secuencias de datos, en las que se desea poder modificar el orden de los elementos libremente.&#x20;

### Set\<E>

Las colecciones de tipo Set representan conjuntos de datos. No es posible definir el orden (o secuencia) en el que se encuentran dichos datos dentro de la colección sino que viene predefinida dependiendo de la misma)

<figure><img src="../.gitbook/assets/image (15).png" alt=""><figcaption><p>Un set es un conjunto de valores no secuenciales</p></figcaption></figure>

Algunas de las características de los Set son:

* Sirven para almacenar **datos no secuenciales**. &#x20;
* Cada instancia de un Set define el tipo de valores que almacena a través del parámetro de tipo E.&#x20;
* No es posible almacenar elementos repetidos.&#x20;
* Son colecciones optimizadas para buscar datos de forma eficiente.&#x20;
* Al no ser una secuencia, los elementos que alberga no tienen una posición (o índice) asociada.
* La ordenación interna de los datos depende del tipo de Set

### Map\<K, V>

Los mapas son colecciones asociativas, que permiten almacenar clave-valor. Al igual que los Set, representan conjuntos de valores no secuenciales, es decir no se puede establecer una ordenación.

Algunas características de los mapas son:

* Son colecciones que permiten asociar pares de valores (clave y valor)
* No puede haber dos pares con la misma clave.
* Cada instancia de Map define el tipo de las claves (K) y el tipo de los valores (V).
* Estas colecciones están optimizadas para la realización de búsquedas por la clave.



### Queue\<E>





