---
cover: ../../.gitbook/assets/control-structures.gif
coverY: 0
---

# Bucle while

Esta estructura iterativa nos permite **repetir la ejecución de un bloque de código un número indeterminado de veces**. Su sintaxis resulta más simple que la de un bucle for.

```java
// Este bucle va a ejecutarse mientras la condición se cumpla
while (condition) {
    // Todo este bloque de código se repite mientras se cumpla la condición
    // code
}
```

El bucle se repetirá hasta qe la condición deje de cumplirse. El bloque de código de los bucles while se ejecutará de **0 a varias veces**, dependiendo de cuando deje de cumplirse la condición.

<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Bucle while</p></figcaption></figure>

A diferencia del bucle for, en esta estructura no resulta obvio cuántas iteraciones va a haber. Veamos un ejemplo concreto.

```java
// Inicializamos la variable i con el valor 5
int i = 5;
// El bucle va a ejecutarse mientras i sea menos de 1000
while(i < 1000) {
    // Mostramos en pantalla el valor de i
    System.out.println(i);
    // Modificamos el valor de i, duplicándolo
    i = i * 2;
}

System.out.println("El valor final de i es " + i);
```

En el ejemplo anterior la salida será:

```
5
10
20
40
80
160
320
640
El valor final de i es 1280

Process finished with exit code 0
```

Se han ejecutado _8_ iteraciones. En la última iteración, el valor de `i` pasa de _640_ a _1280_, esto hace que la condición `i < 1000` deje de cumplirse por lo que el bucle finaliza.

