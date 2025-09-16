---
cover: ../../.gitbook/assets/tree.png
coverY: 94.60266666666666
---

# HashSet\<E>

Esta colección implementa la estructura de datos hashtable. Se trata de una estructura dinámica no lineal.

Para elemento que se va a almacenar se obtiene un código llamado el hashCode, dicho código es un número entero (long) que se intenta que sea lo más único posible por cada valor. A partir del hashCode los datos se almacenan de la siguietne manera:

* Se crea especie de tabla, cada fila tiene un índice y puede almacenar varios valore
* Cada vez que se va a insertar un valor, se obtiene su hashCode y se utiliza para seleccionar una fila (llamada bucket) en la que se va a insertar el valor.
* Dentro de cada bucket se almacena una lista de elementos.

<figure><img src="../../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

Algunas caracterísitcas de esta estructura de datos son:

* Son adecuados cuando el orden de los datos que contiene es irrelevante.
* Están optimizadas para el acceso, inserción y eliminación de datos.
* Es vital que los elementos que se almacenan en un HashSet tengan el método hashCode correctamente implementado.
* Tienen muy buen comportamiento en operaciones de búsqueda, inserción y eliminación con una complejidad de O(1)
* Para poder utilizar esta colección es importante que el orden de los elementos sea irrelevante en el programa, ya que no se respetará el orden de inserción.

## Eficiencia

Los HashSet son tremenadmente eficientes cuando el método hashCode está bien implementado, este método debe tratar de evitar al máximo las colisiones entre distintos objetos.

<figure><img src="../../.gitbook/assets/image (23).png" alt=""><figcaption><p>Eficiencia de los HashSet</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption><p>Notación Big-O</p></figcaption></figure>
