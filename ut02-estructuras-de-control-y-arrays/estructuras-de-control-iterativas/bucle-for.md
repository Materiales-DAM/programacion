---
cover: ../../.gitbook/assets/control-structures.gif
coverY: 0
---

# Bucle For

Esta estructura iterativa nos permite **repetir la ejecución de un bloque de código un número determinado de veces**. Su sintaxis puede resultar poco intuitiva en un principio, pero en cuanto se comprende la mécanica resulta bastante sencilla de utilizar.

Su funcionamiento se basa en el uso de una variable de tipo **contador**, normalmente llamada `i`, que se inicializa con un valor (normalmente 0) que se va incrementando en cada iteración del bucle hasta llegar a un valor determinado (`n`). De esta forma, conseguimos que el bloque de código del bucle for se ejecute n veces.

```java
for (sentencia1; sentencia2 ; sentencia3) {
    // El código que se va a ejecutar varias veces
}
```

* La **sentencia1** se ejecuta sólo una vez, sirve para **inicializar el contador** (normalmente a 0)
* La **sentencia2** debe ser una **** [**expresión condicional**](../../ut01-introduccion-a-la-programacion/expresiones-y-operadores.md#operadores-condicionales)**,** el bucle se repetirá hasta que esta condición deje de cumplirse.
* La **sentencia3** se invoca al finalizar cada iteración, sirve para **modificar el valor del contador**, normalente incrementandolo en 1 (`i++`)

<figure><img src="../../.gitbook/assets/for_loop.jpg" alt=""><figcaption></figcaption></figure>

Por ejemplo, si queremos un bucle que se repita 10 veces:

```java
int n = 10;
// Creamos un bucle for:
//     - Se inicializa una variable entera i con valor inicial 0
//     - Se define la condición de finalización del bucle (i < n)
//     - Se define que al final de cada iteración se aumentará en 1 el valor de i
for (int i = 0; i < n ; i++) {
    // Aquí va el código que se va a repetir
    System.out.println("Iteración " + i);
}

```

En este ejemplo, la sentencia `System.out.println("Iteración " + i);` se va a ejecutar 10 veces, tantas como iteraciones se van a producir al ejecutar el código. La salida del programa será:

```
Iteración 0
Iteración 1
Iteración 2
Iteración 3
Iteración 4
Iteración 5
Iteración 6
Iteración 7
Iteración 8
Iteración 9

Process finished with exit code 0
```

Una vez el contador i llegue al valor 10, la condición `i < n` deja de cumplirse y termina la ejecución del bucle.

Para más información sobre el bucle for pincha [aquí](https://www.w3schools.com/java/java\_for\_loop.asp)
