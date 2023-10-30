# Soluciones

1\.



```java
import java.util.Scanner;

public class Ej1 {

    private static Scanner scanner = new Scanner(System.in);

    public static void printResult(int result) {
        System.out.println("El resultado es " + result);
    }

    public static int sum(int number1, int number2) {
        return number1 + number2;
    }
    
    public static int askNumber() {
        System.out.println("Introduce un número");
        int number = scanner.nextInt();
        scanner.nextLine();
        
        return number;
    }

    public static void main(String[] args) {
        int n1 = askNumber();
        int n2 = askNumber();

        int res = sum(n1, n2);

        printResult(res);
    }


}

```

2\.



```java
import java.util.Scanner;

public class Ej2 {

    private static Scanner scanner = new Scanner(System.in);

    public static int mult(int num1, int num2) {
        return num1 * num2;
    }

    public static void printResult(int res) {
        System.out.println("El resultado es " + res);
    }

    public static int askNumber() {
        System.out.println("Introduce un número");
        int number = scanner.nextInt();
        scanner.nextLine();

        return number;
    }

    public static void main(String[] args) {
        int number1 = askNumber();
        int number2 = askNumber();

        int res = mult(number1, number2);

        printResult(res);

    }
}

```

3\.



```java
import java.util.Scanner;

public class Ej3 {

    private static Scanner scanner = new Scanner(System.in);

    public static String askName() {
        System.out.println("Introduce tu nombre");
        return scanner.nextLine();
    }

    public static void sayHello() {
        String name = askName();

        System.out.println("Hola, " + name);
    }

    public static void shout() {
        String name = askName();

        System.out.println("Cuidado " + name);
    }

    public static int chooseOption() {
        System.out.println("Elige una opción:");
        System.out.println("1. Saluda");
        System.out.println("2. Grita");
        System.out.println("3 Salir");
        int option = scanner.nextInt();
        scanner.nextLine();
        return option;
    }

    public static void runMenuLoop() {
        int option;
        do {
            option = chooseOption();
            switch (option) {
                case 1:
                    sayHello();
                    break;
                case 2:
                    shout();
                    break;
                case 3:
                    System.out.println("Saliendo...");
                    break;
                default:
                    System.out.println("Opción inválida");
            }
        } while(option != 3);
    }

    public static void main(String[] args) {
        runMenuLoop();
    }
}

```

3\.

```java
import java.util.Scanner;

public class Ej4 {
    // chooseOption
    // askNumber
    // printResult
    // runSum
    // runSubstract
    // runMult
    // runMenuLoop

    private static Scanner scanner = new Scanner(System.in);

    public static int chooseOption() {
        printMenu();

        int opt = scanner.nextInt();
        scanner.nextLine();
        while(opt > 4 || opt < 1) {
            System.out.println("Opción inválida...");
            printMenu();
            opt = scanner.nextInt();
            scanner.nextLine();
        }

        return opt;
    }

    private static void printMenu() {
        System.out.println("Elige una opción");
        System.out.println("1. Sumar");
        System.out.println("2. Restar");
        System.out.println("3. Multiplicar");
        System.out.println("4. Salir");
    }

    public static int askNumber() {
        System.out.println("Introduzca un número");
        int num = scanner.nextInt();
        scanner.nextLine();
        return num;
    }

    public static void printResult(int res) {
        System.out.println("El resultado es " + res);
    }

    public static void runSum() {
        int number1 = askNumber();
        int number2 = askNumber();

        int res = number1 + number2;

        printResult(res);
    }

    public static void runSubs() {
        int number1 = askNumber();
        int number2 = askNumber();

        int res = number1 - number2;

        printResult(res);
    }

    public static void runMult() {
        int number1 = askNumber();
        int number2 = askNumber();

        int res = number1 * number2;

        printResult(res);
    }
    
    public static void runMenuLoop() {
        int opt;
        do {
            opt = chooseOption();
            if(opt == 1) {
                runSum();
            } else if(opt == 2) {
                runSubs();
            } else if (opt == 3) {
                runMult();
            } else if (opt == 4) {
                System.out.println("Saliendo...");
            } 
        } while (opt != 4);
    }

    public static void main(String[] args) {
        runMenuLoop();
    }
}
```
