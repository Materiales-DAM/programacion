# Soluciones



```java
import java.util.Scanner;

public class Ej5 {
    private static Scanner scanner = new Scanner(System.in);

    public static int askSize() {
        System.out.println("Introduce el tamaño del array");
        int number = scanner.nextInt();
        scanner.nextLine();
        while (number < 1) {
            System.out.println("El número debe ser mayor que cero...");
            number = scanner.nextInt();
            scanner.nextLine();
        }

        return number;
    }

    public static int[] askArray() {
        int size = askSize();
        int[] numbers = new int[size];
        for (int i = 0; i < numbers.length; i++) {
            System.out.println("Introduce un número");
            numbers[i] = scanner.nextInt();
            scanner.nextLine();
        }
        return numbers;
    }

    public static int findMax(int[] numbers) {
        int max = numbers[0];
        for (int number: numbers) {
            if (number > max) {
                max = number;
            }
        }
        return max;
    }

    public static int findMin(int[] numbers) {
        int min = numbers[0];
        for (int number: numbers) {
            if (number < min) {
                min = number;
            }
        }
        return min;
    }

    public static double average(int[] numbers) {
        int sum = 0;
        for (int number: numbers) {
            sum = sum + number;
        }

        return (double) sum / numbers.length;
    }

    public static int chooseOption() {
        System.out.println("Elige una opción:");
        System.out.println("1. Máximo");
        System.out.println("2. Mínimo");
        System.out.println("3. Media");
        System.out.println("4. Salir");
        int option = scanner.nextInt();
        scanner.nextLine();
        while (option < 0 || option > 4) {
            System.out.println("Opción inválida. Eliga una opción válida");
            option = scanner.nextInt();
            scanner.nextLine();
        }
        return option;
    }

    public static void runMax() {
        int[] numbers = askArray();
        int max = findMax(numbers);
        System.out.println("El máximo es " + max);
    }

    public static void runMin() {
        int[] numbers = askArray();
        int min = findMin(numbers);
        System.out.println("El mínimo es " + min);
    }

    public static void runAverage() {
        int[] numbers = askArray();
        double average = average(numbers);
        System.out.println("La media es " + average);
    }

    public static void runMenuLoop() {
        int option;
        do {
            option = chooseOption();
            if (option == 1) {
                runMax();
            } else if (option == 2) {
                runMin();
            } else if (option == 3) {
                runAverage();
            }
        } while (option != 4);
        System.out.println("Saliendo");
    }

    public static void main(String[] args) {
        runMenuLoop();
    }
}

```
