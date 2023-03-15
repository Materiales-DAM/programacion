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
}
```

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

