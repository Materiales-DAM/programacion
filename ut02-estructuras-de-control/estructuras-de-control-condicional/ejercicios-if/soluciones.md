# Soluciones

5\.

```java
import java.util.Scanner;

public class Ejercicio5 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("Introduce un número entero");
        int a = scanner.nextInt();
        scanner.nextLine();

        System.out.println("Introduce otro número entero");
        int b = scanner.nextInt();
        scanner.nextLine();

        if (a > b) {
            int sum = a + b;
            System.out.println("La suma es " + sum);
        } else if (a == b) {
            int substract = a - b;
            System.out.println("La resta es " + substract);
        } else {
            System.out.println("Introduce otro número entero");
            int c = scanner.nextInt();
            scanner.nextLine();

            int sum = a + b;
            if (c > sum) {
                System.out.println("c es mayor que a + b");
            } else if (c < sum) {
                System.out.println("c es menor que a + b");
            } else {
                System.out.println("c es igual que a + b");
            }
        }
    }
}

```
