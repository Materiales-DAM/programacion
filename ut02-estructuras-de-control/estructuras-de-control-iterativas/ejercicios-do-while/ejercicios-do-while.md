---
cover: ../../../.gitbook/assets/control-structures.gif
coverY: 0
---

# Soluciones do-while

1.  Crea un programa que muestre un menú con las siguientes opciones:

    * Saluda: Pide al usuario su nombre y muestra en pantalla el texto `Hola, <nombre introducido>`. Por ejmplo si introduce el nombre Bob aparecerá el texto `Hola, Bob`
    * Grita: Pide al usuario su nombre y muestra en pantalla el texto `Cuidado <nombre introducido>!`. Por ejmplo si introduce el nombre Bob aparecerá el texto`Cuidado, Bob!`
    *   Salir\


        ```java
        package dowhile;

        import java.util.Scanner;

        public class DoWhile1 {
            public static void main(String[] args) {
                Scanner scanner = new Scanner(System.in);

                int option;
                do {
                    System.out.println("1. Saluda ");
                    System.out.println("2. Grita ");
                    System.out.println("3. Salir ");
                    option = scanner.nextInt();
                    scanner.nextLine();

                    if (option == 1) {

                        System.out.println("Introduce tu nombre");
                        String name = scanner.nextLine();

                        System.out.println("Hola, " + name);
                    } else if (option == 2) {

                        System.out.println("Introduce tu nombre");
                        String name = scanner.nextLine();

                        System.out.println("Cuidado, " + name + "!");
                    }
                } while (option != 3);
            }
        }
        ```

    El programa debe empezar pidiendo al usuario que seleccione la operación que desea realizar, una vez seleccionada la operación solicitará los datos necesarios para realizarla, al final mostrará el resultado en pantalla y volverá a pedir la siguiente operación.
2.  Crea un programa que permita al usuario realizar las siguientes operaciones:

    * Sumar dos números: los pide, los suma y muestra el resultado en pantalla.
    * Restar dos números: los pide, los resta y muestra el resultado en pantalla.
    * Multiplicar dos números: los pide, los multiplica y muestra el resultado en pantalla.
    * Salir

    El programa debe empezar pidiendo al usuario que seleccione la operación que desea realizar, una vez seleccionada la operación solicitará los datos necesarios para realizarla, al final mostrará el resultado en pantalla y volverá a pedir la siguiente operación.\


    ```java
    package dowhile;

    import java.util.Scanner;

    public class DoWhile2 {
        public static void main(String[] args) {
            Scanner scanner = new Scanner(System.in);

            int option;
            do {
                System.out.println("Elija la opción que desee ");
                System.out.println("1. Suma de los dos números");
                System.out.println("2. Resta de los dos números");
                System.out.println("3. Multiplicación de los dos números");
                System.out.println("4. Salir");

                option = scanner.nextInt();
                scanner.nextLine();

                if (option == 1) {
                    System.out.println("Ingrese un número: ");
                    int number1 = scanner.nextInt();
                    scanner.nextLine();

                    System.out.println("Ingrese otro número: ");
                    int number2 = scanner.nextInt();
                    scanner.nextLine();

                    int res = number1 + number2;
                    System.out.println("La suma es: " + res);
                } else if (option == 2) {
                    System.out.println("Ingrese un número: ");
                    int number1 = scanner.nextInt();
                    scanner.nextLine();

                    System.out.println("Ingrese otro número: ");
                    int number2 = scanner.nextInt();
                    scanner.nextLine();

                    int res = number1 - number2;
                    System.out.println("La resta es: " + res);
                } else if (option == 3) {
                    System.out.println("Ingrese un número: ");
                    int number1 = scanner.nextInt();
                    scanner.nextLine();

                    System.out.println("Ingrese otro número: ");
                    int number2 = scanner.nextInt();
                    scanner.nextLine();

                    int res = number1 * number2;
                    System.out.println("La multiplicación es: " + res);
                } else if (option == 4) {
                    System.out.println("Saliendo...");
                } else {
                    System.out.println("Operación inválida");
                }
            } while (option != 4);
        }
    }
    ```
