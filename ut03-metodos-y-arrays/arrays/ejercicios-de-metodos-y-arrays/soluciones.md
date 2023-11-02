# Soluciones

1\.



```java
public class Ej1 {

    public static int max(int[] numbers) {
        int max = numbers[0];
        for (int i = 0; i < numbers.length; i++) {
            if(numbers[i] > max) {
                max = numbers[i];
            }
        }

        return max;
    }

    public static void printMax(int value) {
        System.out.println("El máximo es " + value);
    }

    public static void main(String[] args) {
        int[] numbers = {1, 3, 5, 0};
        int max = max(numbers);
        printMax(max);
    }
}

```

2\.



```java
public class Ej2 {

    public static int sum(int[] numbers) {
        int sum = 0;
        for (int i = 0; i < numbers.length; i++) {
            sum = sum + numbers[i];
        }
        return sum;
    }
    
    public static void printResult(int res) {
        System.out.println("La suma es " + res);
    }

    public static void main(String[] args) {
        int[] numbers = {1, 3, 5, 0};
        
        int res = sum(numbers);
        
        printResult(res);
    }
}

```

3\.



```java
import java.util.Scanner;

public class Ej3 {

    private static Scanner scanner = new Scanner(System.in);

    public static int askPositiveNumber() {
        System.out.println("Introduce un número mayor que cero");

        int number = scanner.nextInt();
        scanner.nextLine();

        while (number <= 0) {
            System.out.println("El número no mayor que cero. Introduce un número mayor que cero...");
            number = scanner.nextInt();
            scanner.nextLine();
        }

        return number;
    }

    public static int[] askArray() {
        int size = askPositiveNumber();
        int[] numbers = new int[size];
        for (int i = 0; i < numbers.length; i++) {
            System.out.println("Introduce un número");
            int number = scanner.nextInt();
            scanner.nextLine();
            numbers[i] = number;
        }

        return numbers;
    }

    public static double average(int[] numbers) {
        int sum = 0;
        for (int i = 0; i < numbers.length; i++) {
            sum = sum + numbers[i];
        }
        return (double) sum / numbers.length;
    }

    public static void printResult(double res) {
        System.out.println("La media es " + res);
    }

    public static void main(String[] args) {
        int[] numbers = askArray();

        double average = average(numbers);

        printResult(average);
    }
}

```
