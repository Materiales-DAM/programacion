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
       import java.util.Scanner;

       public class Methods1 {

           public static void main(String[] args) {
               Scanner scanner = new Scanner(System.in);
               System.out.println("Introduce un número");
               int n1 = scanner.nextInt();
               scanner.nextLine();

               System.out.println("Introduce otro número");
               int n2 = scanner.nextInt();
               scanner.nextLine();

               int res = sum(n1, n2);
               print(res);
               
               // print(sum(n1, n2));
           }

           public static int sum(int n1, int n2) {
               return n1 + n2;
           }

           public static void print(int result) {
               System.out.println("El resutlado es " + result);
           }
       }
       ```
2. Crea un programa que defina los siguientes métodos:
   1. Un método que calcule la multiplicación de sus dos parámetros enteros y devuelva el resultado
   2. Un método que reciba un entero por parámetro e imprima el texto “El resultado es: ” y el parámetro recibido. Este método no devolverá nada

En el main pide dos números enteros, e invoca el primer método pasando esos valores, después se invocará el segundo método con el resultado de la invocación del primero\


```java
import java.util.Scanner;

public class Methods2 {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Introduce un número");
        int n1 = scanner.nextInt();
        scanner.nextLine();

        System.out.println("Introduce otro número");
        int n2 = scanner.nextInt();
        scanner.nextLine();

        int res = mult(n1, n2);
        print(res);

        // print(mult(n1, n2));
    }

    public static int mult(int n1, int n2) {
        return n1 * n2;
    }

    public static void print(int result) {
        System.out.println("El resutlado es " + result);
    }

}
```

3. Crea un programa que muestre un menú con las siguientes opciones:

* Saluda: Pide al usuario su nombre y muestra en pantalla el texto `Hola, <nombre introducido>`. Por ejmplo si introduce el nombre Bob aparecerá el texto `Hola, Bob`
* Grita: Pide al usuario su nombre y muestra en pantalla el texto `Cuidado <nombre introducido>!`. Por ejmplo si introduce el nombre Bob aparecerá el texto`Cuidado, Bob!`
* Salir

Para implementar este programa crea los siguiente métodos:

* Un método que sirva para imprimir en pantalla el menú y lee la opción elegida por el usuario, al final devuelve la opción elegida
* Un método que contiene todo el código de la opción "Saluda": Pide al usuario su nombre y muestra en pantalla el texto `Hola, <nombre introducido>`. Por ejmplo si introduce el nombre Bob aparecerá el texto `Hola, Bob`
* Un método que contiene todo el código de la opción Grita: Pide al usuario su nombre y muestra en pantalla el texto `Cuidado <nombre introducido>!`. Por ejmplo si introduce el nombre Bob aparecerá el texto`Cuidado, Bob!`
* Un método que implementa el bucle del menú interactivo e invoca a los métodos anteriores para realizar las distintas tareas
*   En el método main se invocará al método que implementa el bucle del menú interactivo.\


    ```java
    import java.util.Scanner;

    public class Methods3 {
        public static void main(String[] args) {
            menuLoop();
        }

        public static int chooseOption(Scanner scanner) {
            System.out.println("Elige una opción");
            System.out.println("1. Saluda");
            System.out.println("2. Grita");
            System.out.println("3. Salir");

            int option = scanner.nextInt();
            scanner.nextLine();

            return option;
        }

        public static void greeting(Scanner scanner) {
            System.out.println("Introduce tu nombre");
            String name = scanner.nextLine();

            System.out.println("Hola, " + name);
        }

        public static void shout(Scanner scanner) {
            System.out.println("Introduce tu nombre");
            String name = scanner.nextLine();

            System.out.println("Cuidado, " + name + "!");
        }

        public static void menuLoop() {
            int option;
            Scanner scanner = new Scanner(System.in);
            do {
                option = chooseOption(scanner);

    //            switch (option) {
    //                case 1:
    //                    greeting(scanner);
    //                    break;
    //                case 2:
    //                    shout(scanner);
    //                    break;
    //                case 3:
    //                    System.out.println("Saliendo...");
    //                    break;
    //                default:
    //                    System.out.println("Opción inválida");
    //            }
                if(option == 1) {
                    greeting(scanner);
                } else if (option == 2) {
                    shout(scanner);
                } else if (option == 3) {
                    System.out.println("Saliendo...");
                } else {
                    System.out.println("Opción inválida");
                }

            } while(option != 3);
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
*   En el main invoca el método del bucle del menú.\


    ```java
    import java.util.Scanner;

    public class Methods4 {
        public static void main(String[] args) {
            Scanner scanner = new Scanner(
                    System.in
            );
            loop(scanner);
        }

        public static void loop(Scanner scanner) {
            System.out.println("¡Bienvenido!");
            int option;
            do {
                option = chooseOption(scanner);
                if (option == 1) {
                    sum(scanner);
                } else if (option == 2) {
                    subtract(scanner);
                } else if (option == 3) {
                    multiply(scanner);
                } else if (option == 4) {
                    System.out.println("¡Hasta luego!");
                } else {
                    System.out.println("opción no válida");
                }
            } while (option != 4);
        }

        public static int chooseOption(Scanner scanner) {
            System.out.println("Elija una operación: ");
            System.out.println("1. Sumar");
            System.out.println("2. Restar");
            System.out.println("3. Multiplicar");
            System.out.println("4. Salir");
            int option = scanner.nextInt();
            scanner.nextLine();
            return option;
        }

        public static void sum(Scanner scanner) {
            Double num1 = askNumber(scanner);
            Double num2 = askNumber(scanner);

            System.out.println("El resultado de la suma es: " + (num1 + num2));
        }

        public static void subtract(Scanner scanner) {
            double num1 = askNumber(scanner);
            double num2 = askNumber(scanner);

            System.out.println("El resultado de la resta es: " + (num1 - num2));
        }

        public static void multiply(Scanner scanner) {
            double num1 = askNumber(scanner);
            double num2 = askNumber(scanner);

            System.out.println("El resultado de la multiplicación es: " + (num1 * num2));
        }

        public static double askNumber(Scanner scanner) {
            System.out.println("Ingrese un número: ");
            double num = scanner.nextDouble();
            scanner.nextLine();

            return num;
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
* En el main se creará el menú interactivo usando lo anterior
