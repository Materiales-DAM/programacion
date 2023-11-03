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

4\.



```java
import java.util.Scanner;

public class Ej4 {

    public static Scanner scanner = new Scanner(System.in);

    public static int askPositive() {
        System.out.println("Introduce el tamaño del array");
        int size = scanner.nextInt();
        scanner.nextLine();
        while(size < 1) {
            System.out.println("El tamaño deber ser mayor que cero. Introduce el tamaño del array...");
            size = scanner.nextInt();
            scanner.nextLine();
        }
        return size;
    }

    public static int[] askArray() {
        int size = askPositive();
        int[] numbers = new int[size];
        for (int i = 0; i < numbers.length; i++) {
            System.out.println("Introduce un número");
            numbers[i] = scanner.nextInt();
            scanner.nextLine();
        }
        return numbers;
    }


    public static int[] invertArray(int[] numbers) {
        int[] res = new int[numbers.length];
        // Supongamos que numbers es {1, 3, 5, 7}
        for (int i = 0; i < numbers.length; i++) {
            // i=0; j= 4 - 1 - 0 = 3; numbers[0]= 1; res= { _, _, _, 1 }
            // i=1; j= 4 - 1 - 1 = 2; numbers[1]= 3; res= { _, _, 3, 1 }
            // i=2; j= 4 - 1 - 2 = 1; numbers[2]= 5; res= { _, 5, 3, 1 }
            // i=3; j= 4 - 1 - 3 = 0; numbers[3]= 7; res= { 7, 5, 3, 1 }
            int j = numbers.length - 1 - i;
            res[j] = numbers[i];
        }
        return res;
    }

    public static int[] unionArrays(int[] a1, int[] a2) {
        int[] res = new int[a1.length + a2.length];

        // a1={2, 3}, a2={5, 7}, res = {_, _, _, _}

        for (int i = 0; i < a1.length; i++) {
            // i=0, j=0, res={2, _, _, _}
            // i=1, j=1, res={2, 3, _, _}
            int j = i;
            res[j] = a1[i];
        }

        for (int i = 0; i < a2.length; i++) {
            // i=0, j=2, res={2, 3, 5, _}
            // i=1, j=3, res={2, 3, 5, 7}
            int j = i + a1.length;
            res[j] = a2[i];
        }
        // res={2, 3, 5, 7}

        return res;
    }

    public static void printArray(int[] numbers) {
        System.out.println("Array {");
        for (int i = 0; i < numbers.length; i++) {
            System.out.println("    " +  numbers[i]);
        }
        System.out.println("}");
    }

    public static void main(String[] args) {
        var numbers1 = askArray();

        var invertedNumbers1 = invertArray(numbers1);

        printArray(invertedNumbers1);

        var numbers2 = askArray();

        var invertedNumbers2 = invertArray(numbers2);

        printArray(invertedNumbers2);

        var unionArray = unionArrays(invertedNumbers1, invertedNumbers2);

        printArray(unionArray);
    }
}

```
