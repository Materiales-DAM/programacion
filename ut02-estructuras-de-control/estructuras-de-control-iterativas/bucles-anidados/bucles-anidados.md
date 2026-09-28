---
cover: ../../../.gitbook/assets/control-structures.gif
coverY: 0
---

# Soluciones Bucles anidados

1.  Realiza un programa que solicite un número entero positivo (n) y saque por pantalla lo siguiente:\
    1 2 3 4 … n\
    2 3 4 5 … n + 1\
    3 4 5 6 … n + 2\
    ...\
    n n+1 n+2 … n+n-1<br>

    ```java
    package org.ies.tierno.nested;

    import java.util.Scanner;

    public class Ej1 {
        public static void main(String[] args) {
            Scanner scanner = new Scanner(System.in);
            System.out.println("Introduce un número:");
            int n = scanner.nextInt();
            scanner.nextLine();

            for (int i = 0; i < n; i++) {
                for (int j = 0; j < n; j++) {
                    System.out.print((j + 1 + i) + " ");
                }
                System.out.println();
            }
        }
    }
    ```
2.  Escribe un programa que pida un número positivo (n) e imprima la siguiente serie\
    1\
    2 2\
    3 3 3\
    ...\
    n n n….. n<br>

    ```java
    package org.ies.tierno;

    import java.util.Scanner;

    public class Ejercicio2 {
        public static void main(String[] args) {
            Scanner scanner = new Scanner (System.in);
            System.out.println("Introduce un numero");
            int n = scanner.nextInt();
            scanner.nextLine();

            for (int i = 0; i < n; i++) {
                for (int j = 0; j <= i; j++) {
                    System.out.print(i + 1);
                }
                System.out.println();
            }
        }
    } 
    ```
3.  Escribe un programa que pida un número positivo (n) e imprima la siguiente serie\
    1\
    12\
    123\
    1234\
    12345<br>

    ```java
    ```
4.  Escribe un programa que pida un número positivo (n) e imprima la siguiente serien\
    n n n n …. n\
    …\
    2 2\
    1<br>

    ```java
    ```
5.  Escribe un programa que:

    1. Pida un número entero positivo (v1)
    2. Pida un número entero positivo (v2)
    3. Por cada número que hay entre v1 y v2, calcula el sumatorio de 0 al número
       * Sumatorio de 1: 1 + 0
       * Sumatorio de 2: 2 + 1 + 0
       * Sumatorio de 3: 3 + 2 + 1 + 0<br>

    ```java
    ```

