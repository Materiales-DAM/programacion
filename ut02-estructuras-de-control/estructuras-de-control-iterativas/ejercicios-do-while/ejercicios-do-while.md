---
cover: ../../../.gitbook/assets/control-structures.gif
coverY: 0
---

# Soluciones do-while

1.  Crea un programa que muestre un menú con las siguientes opciones:

    * Saluda: Pide al usuario su nombre y muestra en pantalla el texto `Hola, <nombre introducido>`. Por ejmplo si introduce el nombre Bob aparecerá el texto `Hola, Bob`
    * Grita: Pide al usuario su nombre y muestra en pantalla el texto `Cuidado <nombre introducido>!`. Por ejmplo si introduce el nombre Bob aparecerá el texto`Cuidado, Bob!`
    *   Salir<br>

        ```java
        package org.example.dowhile;

        import java.util.Scanner;

        public class Ej1 {
            public static void main(String[] args) {
                Scanner scanner = new Scanner(System.in);
                int option;
                do {
                    System.out.println("Elige una opción: ");
                    System.out.println("1. Saluda");
                    System.out.println("2. Grita");
                    System.out.println("3. Salir");
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
                    } else if (option == 3) {
                        System.out.println("Saliendo del menú");
                    } else {
                        System.out.println("Opción inválida");
                    }
                } while (option != 3);
            }
        }

        ```

    El programa debe empezar pidiendo al usuario que seleccione la operación que desea realizar, una vez seleccionada la operación solicitará los datos necesarios para realizarla, al final mostrará el resultado en pantalla y volverá a pedir la siguiente operación.
2.  Crea un programa que permita al usuario realizar las siguientes operaciones:

    * Sumar dos números enteros: los pide, los suma y muestra el resultado en pantalla.
    * Restar dos números con decimales: los pide, los resta y muestra el resultado en pantalla.
    * Multiplicar dos números enteros: los pide, los multiplica y muestra el resultado en pantalla.
    * Salir

    El programa debe empezar pidiendo al usuario que seleccione la operación que desea realizar, una vez seleccionada la operación solicitará los datos necesarios para realizarla, al final mostrará el resultado en pantalla y volverá a pedir la siguiente operación.<br>

    ```java
    package org.example.dowhile;

    import java.util.Scanner;

    public class Ej2 {
        public static void main(String[] args) {
            Scanner sc = new Scanner(System.in);
            int option;
            do {
                System.out.println("Calculator");
                System.out.println("1. Suma");
                System.out.println("2. Resta");
                System.out.println("3. Multiplica");
                System.out.println("4. Salir");
                option = sc.nextInt();
                sc.nextLine();
                if (option == 1) {
                    System.out.println("Introduce un numero");
                    int n1 = sc.nextInt();
                    sc.nextLine();
                    System.out.println("Introduce otro");
                    int n2 = sc.nextInt();
                    sc.nextLine();
                    int n3 = n1 + n2;
                    System.out.println("La suma es " + n3);
                } else if (option == 2) {
                    System.out.println("Introduce un numero");
                    int n1 = sc.nextInt();
                    sc.nextLine();
                    System.out.println("Introduce otro");
                    int n2 = sc.nextInt();
                    sc.nextLine();
                    int n3 = n1 - n2;
                    System.out.println("La resta es " + n3);
                } else if (option == 3) {
                    System.out.println("Introduce un numero");
                    int n1 = sc.nextInt();
                    sc.nextLine();
                    System.out.println("Introduce otro");
                    int n2 = sc.nextInt();
                    sc.nextLine();
                    int n3 = n1 * n2;
                    System.out.println("La multiplicacion es " + n3);
                }
            } while (option != 4);
        }
    }
    ```
