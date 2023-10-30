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

4\.

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

5\.



```java
import java.util.Scanner;

public class Ej5 {
    
    private static Scanner scanner = new Scanner(System.in);

    public static int askPosivite() {
        System.out.println("Introduce un número positivo");
        int number = scanner.nextInt();
        scanner.nextLine();

        while (number < 0) {
            System.out.println("El número debe ser positivo...");
            number = scanner.nextInt();
            scanner.nextLine();
        }

        return number;
    }

    public static int askNumber() {
        System.out.println("Introduce un número");
        int number = scanner.nextInt();
        scanner.nextLine();

        return number;
    }

    public static int summatory(int num) {
        int sum = 0;
        for (int i = 0; i <= num; i++) {
            sum = sum + i;
        }

        return sum;
    }

    public static void runSummatoryOption() {
        int number = askPosivite();

        int res = summatory(number);

        System.out.println("El sumatorio es " + res);
    }

    public static int factorial(int num) {
        int fact = 1;
        for (int i = 1; i <= num; i++) {
            fact = fact * i;
        }

        return fact;
    }

    public static void runFactorialOption() {
        int number = askPosivite();

        int res = factorial(number);

        System.out.println("El factorial es " + res);
    }

    public static double average(
            int number1,
            int number2,
            int number3,
            int number4
    ) {
        return (double) (number1 + number2 + number3 + number4) / 4;
    }

    public static void runAverageOption() {
        int number1 = askNumber();
        int number2 = askNumber();
        int number3 = askNumber();
        int number4 = askNumber();

        double res = average(number1, number2, number3, number4);

        System.out.println("La media es " + res);
    }

    public static int chooseOption() {
        printMenu();
        int opt = scanner.nextInt();
        scanner.nextLine();
        while (opt < 1 || opt > 4) {
            System.out.println("Opción inválida");
            printMenu();
            opt = scanner.nextInt();
            scanner.nextLine();
        }
        return opt;
    }

    private static void printMenu() {
        System.out.println("Elige una opción:");
        System.out.println("1. Sumatorio");
        System.out.println("2. Factorial");
        System.out.println("3. Media");
        System.out.println("4. Salir");
    }

    private static void runMenuLoop() {
        int opt;
        do {
            opt = chooseOption();

            if(opt == 1) {
                runSummatoryOption();
            } else if(opt == 2) {
                runFactorialOption();
            } else if(opt == 3) {
                runAverageOption();
            } else if(opt == 4) {
                System.out.println("Saliendo...");
            }
        } while (opt != 4);
    }

    public static void main(String[] args) {
        runMenuLoop();
    }
}

```
