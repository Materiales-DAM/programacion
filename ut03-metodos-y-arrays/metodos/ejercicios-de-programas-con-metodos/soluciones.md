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
