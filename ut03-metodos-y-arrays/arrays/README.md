---
cover: ../../.gitbook/assets/arrays.png
coverY: 0
layout:
  cover:
    visible: true
    size: full
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

# Arrays

Un array Java es una estructura de datos que nos permite almacenar varios valoresde un mismo tipo. Cuando creamos un array debemos definir el número de valores que va a contener, una vez creado ya no podemos cambiar su tamaño.



<figure><img src="../../.gitbook/assets/arrays.png" alt=""><figcaption><p>Array de enteros de longitud 6</p></figcaption></figure>

## El tipo array

Para declarar variables de tipo array debemos combinar dos cosas:

* El tipo de los valores que va a contener el array
* Los símbolos `[]` que señalan que es un array.

Por tanto, tendremos muchos tipos de arrays:

```java
// Este tipo es un array de enteros
int[] intArray;
// Este tipo es un array de double
double[] doubleArray;
// Este tipo es un array de boolean
boolean[] boolArray;
// Este tipo es un array de String
String[] stringArray;
```

## Creación de arrays

Para poder crear un array debemos saber que tamaño (el número de valores que podrá guardar) va a tener el array.&#x20;

```java
// Crea un array con 4 posiciones, este array podrá almacenar 4 números enteros
int[] numbers = new int[4];
```

El array `numbers` se ha creado, ahora llega el momento de guardar valores dentro del mismo.&#x20;

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Array vacío de 4 posiciones</p></figcaption></figure>

Cada valor que queramos almacenar debe ocupar una posición distinta dentro del array.

```java
// La primera posición del array está en el índice 0. Vamos a almacenar el valor 5
numbers[0] = 5;
// En la siguiente posición (índice 1), almacenamos el valor 1
numbers[1] = 1;
// En la siguiente posición (índice 2), almacenamos el valor 7
numbers[2] = 7;
// En la siguiente posición (índice 3), almacenamos el valor 9
numbers[3] = 9;
```

Ahora tenemos un array que almacena los siguientes valores:

<figure><img src="../../.gitbook/assets/image (4) (1) (1).png" alt=""><figcaption><p>Array de enteros con 4 valores</p></figcaption></figure>

En cualquier momento, podemos modificar el valor almacenado en una posición asignando un nuevo valor en el índice correspondiente

```java
// En esta posición estaba el valor 7, después de esta sentencia se sustitutye por 10
number[2] = 10;
```

Ahora el array numbers almacena

<img src="../../.gitbook/assets/file.excalidraw (1).svg" alt="" class="gitbook-drawing">

### Creación inline de un array

Si queremos crear un array que contenga unos valores que conocemos de antemano, es posible hacerlo en una sola línea de la siguiente manera

<pre class="language-java"><code class="lang-java">// Esta sentencia crea un array de tamaño 4 y asinga cada valor a una posición 

<strong>String[] names = {"Bob", "Peppa", "Pocoyo", "George"};
</strong></code></pre>

El código anterior sería equivalente a

```java
// Se crea un array de String vacío de tamaño 4
String[] names = new String[4];

// El la posición 0 se almacena el valor "Bob"
names[0] = "Bob";
// El la posición 1 se almacena el valor "Peppa"
names[1] = "Peppa";
// El la posición 2 se almacena el valor "Pocoyo"
names[2] = "Pocoyo";
// El la posición 3 se almacena el valor "George"
names[3] = "George";
```

El array resultante en ambos casos sería

<figure><img src="../../.gitbook/assets/image (3) (1) (1) (1).png" alt=""><figcaption><p>Array de nombres</p></figcaption></figure>

## Acceder los valores del array

Para usar alguno de los valores de un array vamos a utilizar el índice

```java
int[] numbers = {4, 2, 7, 9};
System.out.println("En la posición 0 está el número " + numbers[0]);
System.out.println("En la posición 1 está el número " + numbers[1]);
System.out.println("En la posición 2 está el número " + numbers[2]);
System.out.println("En la posición 3 está el número " + numbers[3]);
```

### ArrayIndexOutOfBoundsException

Los arrays tienen un tamaño fijo, y por tanto un número determinado de huecos o posiciones en los que podemos almacenar valores. Entonces, ¿qué pasa si tratamos de acceder a una posición que no existe?

Por ejemplo, si tenemos el siguiente array

```java
int[] numbers = {4, 2, 7, 9};
```

<figure><img src="../../.gitbook/assets/image (4) (1) (1) (1).png" alt=""><figcaption><p>Array de números</p></figcaption></figure>

Tiene 4 valores, por lo que las únicas posiciones válidas son: 0, 1, 2 y 3. Si tratamos de acceder a una posición que no existe el programa terminará mostrando la excepción `ArrayIndexOutOfBoundsException`

<pre class="language-java"><code class="lang-java"><strong>// La posición 0 existe, por lo que esta sentencia funciona sin problemas
</strong>System.out.println("El número de la posición 0 es " + numbers[0]);
// La posición 5 no existe, la última es la 3. Cuando se ejecuta esta sentencia ocurre una excepción
System.out.println("El número de la posición 5 es " + numbers[5]);
</code></pre>

Cuando se ejecuta el segundo `println`, el programa termina abruptamente mostrando el siguiente error en la consola

```log
Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: Index 5 out of bounds for length 4
	at ArrayExample.main(ArrayExample.java:7)
```
