---
cover: ../../.gitbook/assets/java.jpeg
coverY: 0
---

# Soluciones variables y tipos

1.  Escribe un programa Increments que:



    ```java
    package org.example.variables;

    import java.util.Scanner;

    public class Increments {
        public static void main(String[] args) {
            Scanner scanner = new Scanner(System.in);
            System.out.println("Introduce un número real: ");
            double number = scanner.nextDouble();
            scanner.nextLine();
            System.out.println("Introduce tu nombre");
            String nombre = scanner.nextLine();
            number ++;
            number ++;
            System.out.println("Hola " + nombre + ", el resultado es " + number);
        }
    }
    ```
2.  Escribe un programa Division que:

    ```java
    package org.example.variables;

    import java.util.Scanner;

    public class Division {
        public static void main(String[] args) {
            Scanner scanner = new Scanner(System.in);
            System.out.println("Introduce el numerador");
            double numerator = scanner.nextDouble();
            scanner.nextLine();
            System.out.println("Introduce el denominador");
            double denominator = scanner.nextDouble();
            scanner.nextLine();

            double division = numerator / denominator;

            System.out.println("El resultado es " + division);
        }
    }

    ```
3.  Escribe un programa Multiplication que:

    ```java
    package org.example.variables;

    import java.util.Scanner;

    public class Multiplication {
        public static void main(String[] args) {
            Scanner scanner = new Scanner(System.in);
            System.out.println("Introduce un entero");
            int n1 = scanner.nextInt();
            scanner.nextLine();
            System.out.println("Introduce otro entero");
            int n2 = scanner.nextInt();
            scanner.nextLine();

            int res = n1 * n2;

            System.out.println("El resultado es " + res);
        }
    }

    ```
4.  Escribe un programa AreEqual que:

    ```java
    package org.example.variables;

    import java.util.Scanner;

    public class AreEqual {
        public static void main(String[] args) {
            // Creamos la utilidad scanner con la que después solicitamos datos al usuario
            Scanner scanner = new Scanner(System.in);

            // Pedimos al usuario el primer número a comparar
            System.out.println("Introduce el primer número a comparar");
            int num1 = scanner.nextInt();
            scanner.nextLine();
            // Pedimos al usuario el segundo número a comparar
            System.out.println("Introduce el segundo número a comparar");
            int num2 = scanner.nextInt();
            scanner.nextLine();

            // Comparamos los dos números para comprobar si son iguales y mostramos en pantalla si lo es o no
            boolean areEquals = num1 == num2;
            System.out.println("¿Son iguales? " + areEquals);
        }
    }
    ```
5.  Escribe un programa AreNotEqual que:

    ```java
    ```
