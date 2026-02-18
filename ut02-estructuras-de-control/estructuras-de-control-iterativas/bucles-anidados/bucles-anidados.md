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
    package org.example.nestedloops;

    import java.util.Scanner;

    public class Ej1 {
        public static void main(String[] args) {
            Scanner scanner = new Scanner(System.in);
            int n;
            do {
                System.out.println("Introduce un número positivo");
                n = scanner.nextInt();
                scanner.nextLine();
            } while (n < 1);

            for (int i = 0; i < n; i++) {
                for (int j = 0; j < n; j++) {
                    System.out.print(i + 1 + j);
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
    package org.example.nestedloops;

    import java.util.Scanner;

    public class Ej2 {
        public static void main(String[] args) {
            Scanner scanner = new Scanner(System.in);
            int n;
            do {
                System.out.println("Introduce un número positivo");
                n = scanner.nextInt();
                scanner.nextLine();
            } while (n < 1);

            for (int i = 0; i < n; i++) {
                for (int j = 0; j < i + 1; j++) {
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
    package org.example.nestedloops;

    import java.util.Scanner;

    public class Ej3 {
        public static void main(String[] args) {
            Scanner scanner = new Scanner(System.in);
            int n;
            do {
                System.out.println("Introduce un número positivo");
                n = scanner.nextInt();
                scanner.nextLine();
            } while (n < 1);

            for (int i = 0; i <= n; i++) {
                for (int j = 0; j < i; j++) {
                    System.out.print(j + 1);
                }
                System.out.println();
            }
        }
    }

    ```
4.  Escribe un programa que pida un número positivo (n) e imprima la siguiente serien\
    n n n n …. n\
    …\
    2 2\
    1<br>

    ```java
    package org.example.nestedloops;

    import java.util.Scanner;

    public class Ej4 {
        public static void main(String[] args) {
            Scanner scanner = new Scanner(System.in);
            int n;
            do {
                System.out.println("Introduce un número positivo");
                n = scanner.nextInt();
                scanner.nextLine();
            } while (n < 1);

            for (int i = n; i > 0 ; i--) {
                for (int j = 0; j < i; j++) {
                    System.out.print(i);
                }
                System.out.println();
            }
        }
    }
    ```
5. Escribe un programa que:
   1. Pida un número entero positivo (v1)
   2. Pida un número entero positivo (v2)
   3. Por cada número que hay entre v1 y v2, calcula el sumatorio de 0 al número
      * Sumatorio de 1: 1 + 0
      * Sumatorio de 2: 2 + 1 + 0
      *   Sumatorio de 3: 3 + 2 + 1 + 0<br>

          ```java
          package org.example.nestedloops;

          import java.util.Scanner;

          public class Ej5 {
              public static void main(String[] args) {
                  Scanner scanner = new Scanner(System.in);
                  int n1;
                  do {
                      System.out.println("Introduce un número positivo");
                      n1 = scanner.nextInt();
                      scanner.nextLine();
                  } while (n1 < 1);


                  int n2;
                  do {
                      System.out.println("Introduce otro número mayor que " + n1);
                      n2 = scanner.nextInt();
                      scanner.nextLine();
                  } while (n2 < n1);

                  for (int i = n1; i <= n2; i++) {
                      int sum = 0;
                      for (int j = 1; j <= i; j++) {
                          sum += j;
                      }
                      System.out.println("El sumatorio de " + i + " es: " + sum);
                  }
              }
          }

          ```

