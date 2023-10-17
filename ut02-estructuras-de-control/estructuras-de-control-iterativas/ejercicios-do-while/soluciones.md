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
