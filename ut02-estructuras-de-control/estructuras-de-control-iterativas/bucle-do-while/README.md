---
cover: ../../../.gitbook/assets/control-structures.gif
coverY: 0
---

# Bucle do-while

Es una variación del bucle while, la diferencia es que en este caso la condición se comprueba al finalizar cada iteración, en lugar de antes. Esta característica garantiza que en los bucle do-while **SIEMPRE** se va a ejecutar **AL MENOS UNA ITERACIÓN**.

Su sintaxis es similar a la de un while pero en distinto orden:

```java
// Este tipo de bucle empieza con la palabra do
do {
    // Este bloque de código se repite al menos una vez y 
    // hasta que se deje de cumplir la condición
} while (condition);
```

Por tanto, este tipo de bucle será útil cuando queramos asegurar que al menos se va a ejecutar una iteración.

<figure><img src="../../../.gitbook/assets/image (1).png" alt=""><figcaption><p>Bucle do-while</p></figcaption></figure>

Este tipo de bucle es muy útil para implementar [menús interactivos](menus-interactivos.md).

### IncrementUntil1000DoWhile

Veamos el ejemplo anterior implementado con do-while:

```java
// Inicializamos la variable i con el valor 5
int i = 5;
// El bucle va a ejecutarse mientras i sea menor de 1000
do {
    // Mostramos en pantalla el valor de i
    System.out.println(i);
    // Modificamos el valor de i, duplicándolo
    i = i * 2;
} while (i < 1000);

System.out.println("El valor final de i es " + i);
```

El resultado de ejecutar este programa es el mismo que con un bucle while:

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

Entonces, si el resultado es el mismo ¿para qué sirve este otro tipo de bucle? Su utilizada viene exclusivamente cuando queremos que la primera iteración se ejecute siempre, aunque no se cumpla la condición desde el principio.

### IncrementUntil0DoWhile

```java
// Inicializamos la variable i con el valor 5
int i = 5;
// El bucle va a ejecutarse mientras i sea menor de 0
do {
    // Mostramos en pantalla el valor de i
    System.out.println(i);
    // Modificamos el valor de i, duplicándolo
    i = i * 2;
} while (i < 0);

System.out.println("El valor final de i es " + i);
```

En este programa la salida sería:

```
5
El valor final de i es 10

Process finished with exit code 0
```

### IncrementUntil0While

Mientras que en la versión con el bucle while sería

```java
// Inicializamos la variable i con el valor 5
int i = 5;
// El bucle va a ejecutarse mientras i sea menor de 0
while (i < 0){
    // Mostramos en pantalla el valor de i
    System.out.println(i);
    // Modificamos el valor de i, duplicándolo
    i = i * 2;
}

System.out.println("El valor final de i es " + i);
```

Y la salida sería:

```
El valor final de i es 5

Process finished with exit code 0
```
