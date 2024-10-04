---
cover: ../../../.gitbook/assets/control-structures.gif
coverY: 0
---

# Soluciones for

1\. Crea un programa que en el main:

```java
package forExercises;

import java.util.Scanner;

public class For1 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Introduce un número");
        int n = scanner.nextInt();
        scanner.nextLine();

        System.out.println("Introduce un mensaje");
        String message = scanner.nextLine();

        for (int i = 0; i < n; i++) {
            System.out.println(message);
        }
    }
}
```

2\. Escribir un programa que pida dos números enteros e imprima todos los números que hay entre el más pequeño y el más grande:

```java
package forExercises;

import java.util.Scanner;

public class For2 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Introduce un número");
        int n1 = scanner.nextInt();
        scanner.nextLine();

        System.out.println("Introduce otro número");
        int n2 = scanner.nextInt();
        scanner.nextLine();
        if (n2 > n1) {
            for (int i = n1; i <= n2; i++) {
                System.out.println(i);
            }
        } else {
            for (int i = n2; i <= n1; i++) {
                System.out.println(i);
            }
        }
    }
}
```

3\. Escribir un programa que pida un entero positivo y calcule el sumatorio de cero a ese número

```java
package forExercises;

import java.util.Scanner;

public class For3 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Introduce un número positivo");
        int n = scanner.nextInt();
        scanner.nextLine();

        if (n < 0) {
            System.out.println("Error, el número introducido es negativo");
        } else {
            int summatory = 0;
            for (int i = 0; i <= n; i++) {
                // Esto es equivalente a summatory = summatory + i
                summatory += i;
            }
            System.out.println("El sumatorio es " + summatory);
        }
    }
}
```

4\. Escribir un programa que pida un entero positivo y calcule el factorial de uno a ese número

```java
package forExercises;

import java.util.Scanner;

public class For4 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Introduce un número positivo");
        int n = scanner.nextInt();
        scanner.nextLine();

        if (n < 0) {
            System.out.println("Error, el número introducido es negativo");
        } else {
            int factorial = 1;
            for (int i = 1; i <= n; i++) {
                // Esto es equivalente a factorial = factorial * i
                factorial *= i;
            }
            System.out.println("El factorial es " + factorial);
        }
    }
}
```

5\. Escribir un programa que permita al usuario ingresar dos años y luego imprima todos los años en ese rango, que sean bisiestos.

```java
package forExercises;

import java.util.Scanner;

public class For5 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Introduce un año");
        int n1 = scanner.nextInt();
        scanner.nextLine();

        System.out.println("Introduce otro año");
        int n2 = scanner.nextInt();
        scanner.nextLine();
        if (n2 > n1) {
            for (int i = n1; i <= n2; i++) {
                if(i % 4 == 0 && i % 100 != 0) {
                    System.out.println(i);
                }
            }
        } else {
            for (int i = n2; i <= n1; i++) {
                if(i % 4 == 0 && i % 100 != 0) {
                    System.out.println(i);
                }
            }
        }
    }
}
```

6\. Escribe un programa que pregunte cuántos números se van a introducir, pida esos números y escriba cuántos negativos se han introducido.

```java
package forExercises;

import java.util.Scanner;

public class For6 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("¿Cuántos números va a introducir?");
        int n = scanner.nextInt();
        scanner.nextLine();

        int negatives = 0;

        for (int i = 0; i < n; i++) {
            System.out.println("Introduce un número");
            int number = scanner.nextInt();
            scanner.nextLine();
            if (number < 0) {
                negatives++;
            }
        }
        System.out.println("Ha introducido " + negatives + " negativos");
    }
}
```

7\. Escribe un programa que pregunte cuántos números se van a introducir, pida esos números e imprima el máximo de entre los números introducidos

8\. Escribe un programa que pregunte cuántos números se van a introducir, pida esos números y calcule la media de los mismo. La media se calcula sumando todos los números y dividiendo la suma entre la cantidad de números

9\. Escribe un programa que solicite un número entero mayor que 1 y compruebe si este es primo o no. Un número primo solo es divisible por sí mismo y por el 1

```
5: 5 % 2 == 0, 5 % 3 == 0, 5 % 3 == 0, 5 % 4 == 0 TODO FALSE: es primo 
6: 6 % 2 == 0 TRUE -> NO ES PRIMO
```
