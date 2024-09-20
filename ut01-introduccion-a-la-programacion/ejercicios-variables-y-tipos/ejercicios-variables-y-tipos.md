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
3. Escribe un programa Multiplication que:
   * Pida al usuario un int (number1)
   * Pida al usuario otro int (number2)
   * Calcule la multiplicación de ambos números
   * Muestre en pantalla el resultado "El resultado de la multiplicación es \<resultado>"
4. Escribe un programa AreEqual que:
   * Pida al usuario un int (number1)
   * Pida al usuario otro int (number2)
   * Muestre en pantalla true cuando son iguales o false cuando no son iguales
5. Escribe un programa AreNotEqual que:
   * Pida al usuario un int (number1)
   * Pida al usuario otro int (number2)
   * Muestre en pantalla true cuando no son iguales o false cuando sí son iguales
