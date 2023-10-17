# Soluciones

1\.

```java
import java.util.Scanner;

public class Ej1 {

    static Scanner scanner = new Scanner(System.in);

    public static void main(String[] args) {
        int option;
        do {
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
                System.out.println("Cuidado, " + name);
            } else if (option == 3) {
                System.out.println("Saliendo...");
            } else {
                System.out.println("Opción inválida");
            }
        } while (option != 3);


    }
}

```

2\.

```java
import java.util.Scanner;

public class Ej2 {

    static Scanner scanner = new Scanner(System.in);

    public static void main(String[] args) {
        int option;

        do {
            System.out.println("Elige una opción: ");
            System.out.println("1. Sumar");
            System.out.println("2. Restar");
            System.out.println("3. Multiplicar");
            System.out.println("4. Salir");

            option = scanner.nextInt();
            scanner.nextLine();

            if (option == 1) {
                System.out.println("Introduce un número");
                int num1 = scanner.nextInt();
                scanner.nextLine();

                System.out.println("Introduce un número");
                int num2 = scanner.nextInt();
                scanner.nextLine();

                int sum = num1 + num2;

                System.out.println(sum);
            } else if (option == 2) {
                System.out.println("Introduce un número");
                int num1 = scanner.nextInt();
                scanner.nextLine();

                System.out.println("Introduce un número");
                int num2 = scanner.nextInt();
                scanner.nextLine();

                int substract = num1 - num2;

                System.out.println(substract);
            } else if (option == 3) {
                System.out.println("Introduce un número");
                int num1 = scanner.nextInt();
                scanner.nextLine();

                System.out.println("Introduce un número");
                int num2 = scanner.nextInt();
                scanner.nextLine();

                int mult = num1 * num2;

                System.out.println(mult);
            } else if (option == 4) {
                System.out.println("Saliendo...");
            } else {
                System.out.println("Opción inválida");
            }

        } while (option != 4);

    }
}

```
