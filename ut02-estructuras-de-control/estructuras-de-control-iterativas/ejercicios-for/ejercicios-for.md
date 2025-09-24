---
cover: ../../../.gitbook/assets/control-structures.gif
coverY: 0
---

# Soluciones for

1\. Crea un programa que en el main:

```java
package org.example.forexercises;

import java.util.Scanner;

public class Ej1 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.println("Introduce un mensaje");
        String mensaje = sc.nextLine();

        System.out.println("Introduce el número de veces que quieres que se repita el mensaje");
        int num = sc.nextInt();
        sc.nextLine();

        for (int i = 0; i < num; i++) {
            System.out.println(mensaje);
        }
    }
} 
```

2\. Escribir un programa que pida dos números enteros e imprima todos los números que hay entre el más pequeño y el más grande:

```java
package org.example.forexercises;

import java.util.Scanner;

public class Ej2 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Introduce un número entero");
        int n1 = scanner.nextInt();
        scanner.nextLine();

        System.out.println("Introduce otro número entero");
        int n2 = scanner.nextInt();
        scanner.nextLine();

        int min;
        int max;
        if (n1 > n2) {
            min = n2;
            max = n1;
        } else {
            min = n1;
            max = n2;
        }

        for (int i = min; i <= max; i++) {
            System.out.println(i);
        }
    }
}

```

3\. Escribir un programa que pida un entero positivo y calcule el sumatorio de cero a ese número

```java
package org.example.forexercises;

import java.util.Scanner;

public class Ej3 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Introduce un entero positivo");
        int num = scanner.nextInt();
        scanner.nextLine();

        if (num > 0) {
            int sum = 0;
            for (int i = 0; i <= num; i++) {
                sum = sum + i;
            }
            System.out.println(sum);
        } else {
            System.out.println("El número introducido no es positivo");
        }
    }
}

```

4\. Escribir un programa que pida un entero positivo y calcule el factorial de uno a ese número

```java
package org.example.forexercises;

import java.util.Scanner;

public class Ej4 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Dime un numero: ");
        int num = scanner.nextInt();
        scanner.nextLine();

        int factorial = 1;
        for (int i = 1; i <= num; i++) {
            factorial = factorial * i;
        }
        System.out.println("Si multiplicas todos los numeros del 1 al " + num + " da de resultado: " + factorial);
    }
}
```

5\. Escribir un programa que permita al usuario ingresar dos años y luego imprima todos los años en ese rango, que sean bisiestos.

```java
```

6\. Escribe un programa que pregunte cuántos números se van a introducir, pida esos números y escriba cuántos negativos se han introducido.

```java
```

7\. Escribe un programa que pregunte cuántos números se van a introducir, pida esos números e imprima el máximo de entre los números introducidos

```java
```

8\. Escribe un programa que pregunte cuántos números se van a introducir, pida esos números y calcule la media de los mismo. La media se calcula sumando todos los números y dividiendo la suma entre la cantidad de números

```java
```

9\. Escribe un programa que solicite un número entero mayor que 1 y compruebe si este es primo o no. Un número primo solo es divisible por sí mismo y por el 1

```
5: 5 % 2 == 0, 5 % 3 == 0, 5 % 3 == 0, 5 % 4 == 0 TODO FALSE: es primo 
6: 6 % 2 == 0 TRUE -> NO ES PRIMO
```

```java
```
