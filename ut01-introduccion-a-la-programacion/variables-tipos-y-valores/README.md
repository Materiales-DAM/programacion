---
cover: ../../.gitbook/assets/java.jpeg
coverY: 0
---

# Variables, tipos y valores

Los programas informáticos se dedican en gran medida a la manipulación de datos. Para poder manejar los datos necesitamos poder almacenarlos en algún sitio. Las **variables** son elementos de un programa que permiten almacenar un dato y darle un nombre. Cada variable tiene un **nombre**, un **tipo** y un **valor**.

**El nombre de una variable lo elige el programador** y debe ser descriptivo del dato que va a almacenar.

El **tipo** de una variable depende de las **características de los datos** que va a albergar la variable. Por ejemplo, si queremos que la variable almacene un número entero podemos usar el tipo `int`, si por el contrario queremos que almacene texto podemos usar el tipo `String`.&#x20;

El **valor** de una variable es el dato concreto que le ha sido asignado, por ejemplo el número `3`.

```java
// La siguiente sentencia declara una variable cuyo nombre es myNumber, su tipo
// es int y tiene el valor asignado 3.
int myNumber = 3;
// Cuando se ejecute la siguiente sentencia aparecerá en pantalla un 3
System.out.println(myNumber);
```

Crea una clase llamada `MyNumberProgram` que defina un método `main` con las dos sentencias anteriores.
