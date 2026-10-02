---
cover: ../../../.gitbook/assets/method.jpg
coverY: 0
---

# Soluciones de programas con métodos

1. Crea un programa que defina los siguientes métodos:
   1. Un método que calcule la suma de sus dos parámetros enteros y devuelva el resultado
   2.  Un método que reciba un entero por parámetro e imprima el texto “El resultado es: ” y el parámetro recibido. Este método no devolverá nada<br>

       En el main pide dos números enteros, e invoca el primer método pasando esos valores, después se invocará el segundo método con el resultado de la invocación del primero

       ```java
       package org.ies.tierno;

       import java.util.Scanner;

       public class E1 {
           public static void main(String[] args) {
               Scanner scanner = new Scanner(
       System.in
       );
               System.out.println("dame 2 enteros");
               int n1 = scanner.nextInt();
               scanner.nextLine();
               int n2 = scanner.nextInt();
               scanner.nextLine();
               int result = sum(n1, n2);
               printResult(result);
           }

           public static int sum(int n1, int n2) {
               return n1 + n2;
           }

           public static void printResult(int result) {
               System.out.println("El resultado es: " + result);
           }
       } 
       ```
2. Crea un programa que defina los siguientes métodos:
   1. Un método que calcule la multiplicación de sus dos parámetros enteros y devuelva el resultado
   2. Un método que reciba un entero por parámetro e imprima el texto “El resultado es: ” y el parámetro recibido. Este método no devolverá nada

En el main pide dos números enteros, e invoca el primer método pasando esos valores, después se invocará el segundo método con el resultado de la invocación del primero<br>

```java
package org.ies.tierno;

import java.util.Scanner;

public class Ej2 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Introduce un número");
        int n1 = scanner.nextInt();
        scanner.nextLine();
        System.out.println("Introduce otro número");
        int n2 = scanner.nextInt();
        scanner.nextLine();
        int result = mult(n1,n2);
        printResult(result);
    }
    
    public static int mult(int n1, int n2) {
        return n1*n2;
    }
    
    public static void printResult(int result) {
        System.out.println("El resultado es " + result);
    }
}
```

3. Crea un programa que muestre un menú con las siguientes opciones:

* Saluda: Pide al usuario su nombre y muestra en pantalla el texto `Hola, <nombre introducido>`. Por ejemplo, si introduce el nombre Bob aparecerá el texto `Hola, Bob`
* Grita: Pide al usuario su nombre y muestra en pantalla el texto `Cuidado <nombre introducido>!`. Por ejemplo, si introduce el nombre Bob aparecerá el texto`Cuidado, Bob!`
* Salir

Para implementar este programa crea los siguiente métodos:

* Un método que sirva para imprimir en pantalla el menú y lee la opción elegida por el usuario, al final devuelve la opción elegida
* Un método `askName()` que pide al usuario su nombre y lo devuelve
* Un método que contiene todo el código de la opción "Saluda": Pide al usuario su nombre y muestra en pantalla el texto `Hola, <nombre introducido>`. Por ejemplo, si introduce el nombre Bob aparecerá el texto `Hola, Bob`
* Un método que contiene todo el código de la opción Grita: Pide al usuario su nombre y muestra en pantalla el texto `Cuidado <nombre introducido>!`. Por ejemplo, si introduce el nombre Bob aparecerá el texto`Cuidado, Bob!`
* Un método que implementa el bucle del menú interactivo e invoca a los métodos anteriores para realizar las distintas tareas
*   En el método `main` se invocará al método que implementa el bucle del menú interactivo.<br>

    ```java
    package org.ies.tierno;

    import java.util.Scanner;

    public class Ej3 {
        private static Scanner scanner = new Scanner(System.in);

        public static void main(String[] args) {
            menu();
        }

        public static int chooseOption() {
            System.out.println("Elige una opción:");
            System.out.println("1. Saluda");
            System.out.println("2. Grita");
            System.out.println("3. Salir");
            int option = scanner.nextInt();
            scanner.nextLine();
            return option;
        }

        public static String askName() {
            System.out.println("Introduce el nombre:");
            return scanner.nextLine();
        }

        public static void hello() {
            String name = askName();
            System.out.println("Hola, " + name);
        }

        public static void shout() {
            String name = askName();
            System.out.println("Cuidado, " + name + "!");
        }

        public static void menu() {
            int option;
            do {
                option = chooseOption();
                if (option == 1) {
                    hello();
                } else if (option == 2) {
                    shout();
                } else if (option == 3) {
                    System.out.println("Saliendo...");
                } else {
                    System.out.println("Opción inválida");
                }

            } while (option != 3);
        }
    }

    ```

4. Crea un programa de menú interactivo que permita al usuario realizar las siguientes operaciones:

* Sumar dos números: los pide, los suma y muestra el resultado en pantalla.
* Restar dos números: los pide, los resta y muestra el resultado en pantalla.
* Multiplicar dos números: los pide, los multiplica y muestra el resultado en pantalla.
* Salir

Implementa el programa creando métodos para:.

* Mostrar menú y elegir opción
* Un método que ejecute la opción sumar
* Un método que ejecute la opción restar
* Un método que ejecute la opción multiplicar
* Un método que implemente el bucle del menú
*   En el `main` invoca el método del bucle del menú.<br>

    ```java
    package org.ies.tierno;

    import java.util.Scanner;

    public class Ej4 {
        private static Scanner scanner = new Scanner(System.in);

        public static void main(String[] args) {
            menu();
        }

        public static int chooseOption() {
            System.out.println("Escoge una opción: ");
            System.out.println("1. Sumar: ");
            System.out.println("2. Restar: ");
            System.out.println("3. Multiplicar: ");
            System.out.println("4. Salir: ");
            int option = scanner.nextInt();
            scanner.nextLine();
            return option;
        }

        public static void sum() {
            System.out.print("Introduce el primer número: ");
            int n1 = scanner.nextInt();
            scanner.nextLine();
            System.out.print("Introduce otro número: ");
            int n2 = scanner.nextInt();
            scanner.nextLine();
            int sum = n1 + n2;
            System.out.println("El resultado es: " + sum);
        }

        public static void sus() {
            System.out.print("Introduce el primer número: ");
            int n1 = scanner.nextInt();
            scanner.nextLine();
            System.out.print("Introduce otro número: ");
            int n2 = scanner.nextInt();
            scanner.nextLine();
            int res = n1 - n2;
            System.out.println("El resultado es: " + res);
        }

        public static void multiply() {
            System.out.print("Introduce el primer número: ");
            int n1 = scanner.nextInt();
            scanner.nextLine();
            System.out.print("Introduce otro número: ");
            int n2 = scanner.nextInt();
            scanner.nextLine();
            int mult = n1 * n2;
            System.out.println("El resultado es: " + mult);
        }

        public static void menu() {
            int option;
            do {
                option = chooseOption();
                if (option == 1) {
                    sum();
                } else if (option == 2) {
                    sus();
                } else if (option == 3) {
                    multiply();
                } else if (option == 4) {
                    System.out.println("Saliendo...");
                } else {
                    System.out.println("Opción inválida");
                }
            } while (option != 4);
        }
    } 
    ```

5\. Escribe un programa con estos métodos:

* Un método que dado un entero, devuelva el sumatorio de cero a ese número. Por ejemplo, si se pasa el 6, el resultado será 0 +1 +2 +3 +4 +5+ 6.
* Un método que dado un número entero, devuelve el factorial de ese número. Por ejemplo, si se pasa el 6, el resultado será 1 \* 2 \* 3 \* 4 \* 5 \* 6
* Un método que dados cuatro números enteros, calcula la media y la devuelve.
* Un método que muestre las siguientes opciones,:
  * Sumatorio
  * Factorial
  * Media
  * Salir
* Un método que imprima el menú y pida una opción al usuario, luego la devuelve
*   En el `main` se creará el menú interactivo usando lo anterior<br>

    ```java
    ```
