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

