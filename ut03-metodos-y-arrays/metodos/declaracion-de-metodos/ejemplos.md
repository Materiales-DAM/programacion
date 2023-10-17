# Ejemplos

DoWhile -> Ej1

```java
import java.util.Scanner;

public class Ej1 {

    static Scanner scanner = new Scanner(System.in);

    public static void main(String[] args) {
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

    public static void shout() {
        String name = askName();
        System.out.println("Cuidado, " + name);
    }

    public static void hello() {
        String name = askName();
        System.out.println("Hola, " + name);
    }

    public static String askName() {
        System.out.println("Introduce tu nombre");
        String name = scanner.nextLine();
        return name;
    }

    public static int chooseOption() {
        printMenu();
        int option = scanner.nextInt();
        scanner.nextLine();
        return option;
    }

    public static void printMenu() {
        System.out.println("1. Saluda");
        System.out.println("2. Grita");
        System.out.println("3. Salir");
    }
}

```
