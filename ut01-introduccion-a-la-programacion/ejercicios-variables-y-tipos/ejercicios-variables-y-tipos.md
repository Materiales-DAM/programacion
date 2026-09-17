---
cover: ../../.gitbook/assets/java.jpeg
coverY: 0
---

# Soluciones variables y tipos

1.  Escribe un programa Increments que:



    ```java
    package org.ies.tierno;

    import java.util.Scanner;

    public class Increments {
        public static void main(String[] args) {
            Scanner scanner = new Scanner(System.in);
            System.out.println("Introduce un número:");
            double number = scanner.nextDouble();
            scanner.nextLine();

            number++;
            number++;

            System.out.println("El resultado es " +  number);
        }
    }
    ```
2.  Escribe un programa Division que:

    ```java
    package org.ies.tierno;

    import java.util.Scanner;

    public class Division {
        public static void main(String[] args) {
            Scanner scanner = new Scanner(System.in);
            System.out.println("Introduce el numerador: ");
            double numerator = scanner.nextDouble();
            scanner.nextLine();

            System.out.println("Introduce el denominador: ");
            double denominator = scanner.nextDouble();
            scanner.nextLine();

            double result = numerator / denominator;

            System.out.println("El resultado es " + result);
        }
    }

    ```
3.  Escribe un programa Multiplication que:

    ```java
    package org.ies.tierno;

    import java.util.Scanner;

    public class Multiplication {
        public static void main(String[] args) {
            Scanner scanner = new Scanner(System.in);
            System.out.println("Introduce un número: ");
            double numerator = scanner.nextDouble();
            scanner.nextLine();

            System.out.println("Introduce otro número: ");
            double denominator = scanner.nextDouble();
            scanner.nextLine();

            double result = numerator * denominator;

            System.out.println("El resultado es " + result);
        }
    }

    ```
4.  Escribe un programa AreEqual que:

    ```java
    ```
5.  Escribe un programa AreNotEqual que:

    ```java
    ```
