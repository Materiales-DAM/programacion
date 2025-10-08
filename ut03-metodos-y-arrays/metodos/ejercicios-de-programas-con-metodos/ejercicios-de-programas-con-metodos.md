---
cover: ../../../.gitbook/assets/method.jpg
coverY: 0
---

# Soluciones de programas con métodos

1. Crea un programa que defina los siguientes métodos:
   1. Un método que calcule la suma de sus dos parámetros enteros y devuelva el resultado
   2.  Un método que reciba un entero por parámetro e imprima el texto “El resultado es: ” y el parámetro recibido. Este método no devolverá nada\


       En el main pide dos números enteros, e invoca el primer método pasando esos valores, después se invocará el segundo método con el resultado de la invocación del primero

       ```java
       package org.ies.tierno;

       import java.util.Scanner;

       public class Ej1 {
           public static Scanner scanner = new Scanner(System.in);

           public static void main(String[] args) {
               int n1 = askNumber();
               int n2 = askNumber();
               int res = addition(n1, n2);
               print(res);
           }

           public static int askNumber() {
               System.out.println("Introduce un número entero");
               int n = scanner.nextInt();
               scanner.nextLine();
               return n;
           }

           public static int addition(int n1, int n2) {
               int res = n1 + n2;
               return res;
           }

           public static void print(int res) {
               System.out.println("El resultado es: " + res);
           }
       } 
       ```
2. Crea un programa que defina los siguientes métodos:
   1. Un método que calcule la multiplicación de sus dos parámetros enteros y devuelva el resultado
   2. Un método que reciba un entero por parámetro e imprima el texto “El resultado es: ” y el parámetro recibido. Este método no devolverá nada

En el main pide dos números enteros, e invoca el primer método pasando esos valores, después se invocará el segundo método con el resultado de la invocación del primero\


```java
package org.ies.tierno;

import java.util.Scanner;

public class Ej2 {
    public static Scanner scanner = new Scanner(System.in);

    public static void main(String[] args) {
        int n1 = askNumber();
        int n2 = askNumber();
        int res = multiply(n1, n2);
        print(res);
    }

    public static int askNumber() {
        System.out.println("Introduce un número entero");
        int n = scanner.nextInt();
        scanner.nextLine();
        return n;
    }

    public static int multiply(int n1, int n2) {
        return n1 * n2;
    }

    public static void print(int res) {
        System.out.println("El resultado es: " + res);
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
*   En el método `main` se invocará al método que implementa el bucle del menú interactivo.\


    ```java
    package org.ies.tierno;

    import java.util.Scanner;

    public class Ej3 {
        public static Scanner scanner = new Scanner(System.in);

        public static int menu() {
            int option;
            do {
                option = askOption();

                if (option == 1) {
                    hello();
                } else if (option == 2) {
                    shout();
                } else {
                    exit();
                }

            } while (option != 3);
            return option;
        }

        public static String askName(Scanner scanner) {
            System.out.println("Escribe tu nombre");
            return scanner.nextLine();
        }

        public static void hello() {
            String name = askName(scanner);
            System.out.println("Hola , " + name);
        }

        public static void shout() {
            String name = askName(scanner);
            System.out.println("Cuidado, " + name + "!!!");
        }

        public static void exit() {
            System.out.println("adiós");
        }

        public static void main(String[] args) {
            menu();
        }

        public static int askOption() {
            System.out.println("1. Saluda");
            System.out.println("2. Grita ");
            System.out.println("3. Salir ");

            int option = scanner.nextInt();
            scanner.nextLine();
            return option;
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
*   En el `main` invoca el método del bucle del menú.\


    ```java
    package org.ies.tierno;

    import java.util.Scanner;

    public class Ej4 {
        private static Scanner scanner = new Scanner(System.in);

        public static void menu() {
            int option;
            do {
                System.out.println("Elige una opción:");
                System.out.println("1. Sumar");
                System.out.println("2. Restar");
                System.out.println("3. Multiplicar");
                System.out.println("4. Salir");
                option = scanner.nextInt();
                scanner.nextLine();

                if (option == 1) {
                    sum();
                } else if (option == 2) {
                    substract();
                } else if (option == 3) {
                    multiply();
                } else if (option == 4) {
                    System.out.println("Saliendo...");
                } else {
                    System.out.println("Opción inválida");
                }
            } while (option != 4);
        }

        public static void multiply() {
            int n1 = askNumber();
            int n2 = askNumber();

            int res = mult(n1, n2);

            System.out.println(res);
        }

        public static void substract() {
            int n1 = askNumber();
            int n2 = askNumber();

            int res = subs(n1, n2);

            System.out.println(res);
        }

        public static void sum() {
            int n1 = askNumber();
            int n2 = askNumber();

            int res = add(n1, n2);

            System.out.println(res);
        }

        public static int add(int n1, int n2) {
            return n1 + n2;
        }

        public static int subs(int n1, int n2) {
            return n1 - n2;
        }

        public static int mult(int n1, int n2) {
            return n1 * n2;
        }

        public static int askNumber() {
            System.out.println("Introduce un número:");
            int n = scanner.nextInt();
            scanner.nextLine();
            return n;
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
*   En el `main` se creará el menú interactivo usando lo anterior\


    ```java
    package org.ies.tierno;


    import java.util.Scanner;

    public class Ej5 {
        public static Scanner scanner = new Scanner(
                System.in
        );

        public static void main(String[] args) {
            int option;
            do {
                option = option();
                if (option == 1) {
                    int sum = summation();
                    System.out.println("=" + sum);
                } else if (option == 2) {
                    int factorial = factorial();
                    System.out.println("=" + factorial);
                } else if (option == 3) {
                    double average = average();
                    System.out.println("La media es " + average);
                } else if (option == 4) {
                    System.out.println("Saliendo.....");
                } else {
                    System.out.println("Opcion invalida");
                }
            } while (option != 4);
        }

        public static int summation() {
            System.out.println("Dime un numero");
            int num = scanner.nextInt();
            scanner.nextLine();
            int sum = 0;
            System.out.print(0);
            for (int i = 1; i <= num; i++) {
                System.out.print("+" + i);
                sum = sum + i;
            }
            return sum;
        }

        public static int factorial() {
            System.out.println("Dime un numero");
            int num = scanner.nextInt();
            scanner.nextLine();
            int factorial = 1;
            System.out.print(1);
            for (int i = 2; i <= num; i++) {
                System.out.print("*" + i);
                factorial = factorial * i;
            }
            return factorial;
        }

        public static double average() {
            double sum = 0;
            for (int i = 1; i <= 4; i++) {
                System.out.println("Dime el " + i + "º numero");
                int num = scanner.nextInt();
                scanner.nextLine();
                sum = sum + num;
            }
            double average = sum / 4;
            return average;
        }

        public static void menu() {
            System.out.println("Elige una opcion: ");
            System.out.println("1.Sumatorio");
            System.out.println("2.Factorial");
            System.out.println("3.Media ");
            System.out.println("4.Salir");
        }

        public static int option() {
            menu();
            int option = scanner.nextInt();
            scanner.nextLine();
            return option;
        }
    } 
    ```
