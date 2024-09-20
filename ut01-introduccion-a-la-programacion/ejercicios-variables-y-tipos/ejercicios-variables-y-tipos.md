---
cover: ../../.gitbook/assets/java.jpeg
coverY: 0
---

# Soluciones variables y tipos

1.  Escribe un programa Increments que:



    ```java
    import java.util.Scanner;

    public class Increments {
        public static void main(String[] args) {
            Scanner scanner = new Scanner(System.in);

            System.out.println("Introduce un número con decimales");
            double number = scanner.nextDouble();
            scanner.nextLine();
            
            number++;
            number++;

            System.out.println("El resultado es " + number);
        }
    }
    ```
2.  Escribe un programa Division que:

    ```java
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
            
            double result = numerator / denominator;

            System.out.println("El resultado es " + result);
        }
    }
    ```
3.  Escribe un programa Multiplication que:

    ```java
    import java.util.Scanner;

    public class Multiplication {
        public static void main(String[] args) {
            Scanner scanner = new Scanner(System.in);
            System.out.println("Introduce un número entero");
            int n1 = scanner.nextInt();
            scanner.nextLine();

            System.out.println("Introduce otro número entero");

            int n2 = scanner.nextInt();
            scanner.nextLine();

            int res = n1 * n2;

            System.out.println("El resultado es " + res);
        }
    }
    ```
4.  Escribe un programa AreEqual que:

    ```java
    import java.util.Scanner;

    public class AreEqual {
        public static void main(String[] args) {
            Scanner scanner = new Scanner(System.in);

            System.out.println("Introduce un número entero");
            int num1 = scanner.nextInt();
            scanner.nextLine();

            System.out.println("Introduce otro número entero");
            int num2 = scanner.nextInt();
            scanner.nextLine();

            boolean res = num1 == num2;

            System.out.println("Los números son iguales: " + res);
        }
    }
    ```
5. Escribe un programa AreNotEqual que:
   * Pida al usuario un int (number1)
   * Pida al usuario otro int (number2)
   * Muestre en pantalla true cuando no son iguales o false cuando sí son iguales
