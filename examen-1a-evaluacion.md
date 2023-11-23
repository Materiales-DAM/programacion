# Examen 1ª evaluación

{% file src=".gitbook/assets/1ª evaluación.pdf" %}

Ej1

```java
import java.util.Scanner;

public class Ej1 {
    static Scanner scanner = new Scanner(System.in);

    public static int askSize() {
        System.out.println("Introduce el tamaño del array");
        int size = scanner.nextInt();
        scanner.nextLine();
        while (size < 1) {
            System.out.println("El tamaño debe ser mayor que cero");
            size = scanner.nextInt();
            scanner.nextLine();
        }

        return size;
    }


    public static double[] askArray() {
        System.out.println("Introduce los datos del array");
        double[] numbers = new double[askSize()];
        for (int i = 0; i < numbers.length; i++) {
            System.out.println("Introduce un número");
            numbers[i] = scanner.nextDouble();
            scanner.nextLine();
        }

        return numbers;
    }

    public static double sumArrays(double[] numbers1, double[] numbers2) {
        double sum = 0;
        for (double number: numbers1) {
            sum = sum + number;
        }

        for (int i = 0; i < numbers2.length; i++) {
            sum = sum + numbers2[i];
        }

        return sum;
    }

    public static void printResult(double res) {
        System.out.println("El resultado es " + res);
    }


    public static void main(String[] args) {
        double[] numbers1 = askArray();
        double[] numbers2 = askArray();

        double res = sumArrays(numbers1, numbers2);

        printResult(res);
    }
}

```

Ej2

```java
import java.util.Scanner;

public class Ej2 {
    private static Scanner scanner = new Scanner(System.in);

    public static int askSize() {
        System.out.println("Introduce el tamaño del array");
        int size = scanner.nextInt();
        scanner.nextLine();
        while (size < 1) {
            System.out.println("El tamaño debe ser mayor que cero");
            size = scanner.nextInt();
            scanner.nextLine();
        }

        return size;
    }


    public static double[] askArray() {
        System.out.println("Introduce los datos del array");
        double[] numbers = new double[askSize()];
        for (int i = 0; i < numbers.length; i++) {
            System.out.println("Introduce un número");
            numbers[i] = scanner.nextDouble();
            scanner.nextLine();
        }

        return numbers;
    }

    public static double average(double[] numbers) {
        double sum = 0;
        for (double number : numbers) {
            sum = sum + number;
        }
        return sum / numbers.length;
    }

    public static int countNegatives(double[] numbers) {
        int negatives = 0;
        for (double number : numbers) {
            if (number < 0) {
                negatives++;
            }
        }
        return negatives;
    }

    public static void runAverage() {
        double[] numbers = askArray();
        double avg = average(numbers);
        System.out.println("La media es " + avg);
    }

    public static void runCountNegatives() {
        double[] numbers = askArray();
        int negatives = countNegatives(numbers);
        System.out.println("El número de negativos es " + negatives);
    }

    public static int chooseOption() {
        System.out.println("Elige una opción:");
        System.out.println("1. Cuenta negativos");
        System.out.println("2. Media");
        System.out.println("3. Salir");

        int opt = scanner.nextInt();
        scanner.nextLine();
        while (opt < 1 || opt > 3) {
            System.out.println("Opción inválida... elija una opción válida");
            opt = scanner.nextInt();
            scanner.nextLine();
        }
        return opt;
    }

    public static void main(String[] args) {
        int opt;
        do {
            opt = chooseOption();
            if (opt == 1) {
                runCountNegatives();
            } else if (opt == 2) {
                runAverage();
            }
        } while (opt != 3);
        System.out.println("Saliendo");
    }
}

```
