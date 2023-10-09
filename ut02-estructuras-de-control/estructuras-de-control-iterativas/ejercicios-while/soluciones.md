# Soluciones

1\.

```java
import java.util.Scanner;

public class Ej1 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Introduce un número");
        int number1 = scanner.nextInt();
        scanner.nextLine();
        System.out.println("Introduce otro número");
        int number2 = scanner.nextInt();
        scanner.nextLine();

        // number1 = 5
        // number2 = 3
        while(number2 <= number1) {
            // number1= 5, number2= 3 ---> number2= 1
            // number1= 5, number2= 1 ---> number2=4
            // number1= 5, number2= 4 ---> number2=7
            System.out.println("El segundo número debe ser mayor que el primero...");
            number2 = scanner.nextInt();
            scanner.nextLine();
        }
        // number1=5, number2=7
        System.out.println("Correcto: " + number1 +" > " + +number2);
    }
}

```

2\.



```java
import java.util.Scanner;

public class Ej2 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Introduzca un número con decimales");

        double num1 = scanner.nextDouble();
        scanner.nextLine();

        System.out.println("Introduzca otro número con decimales");

        double num2 = scanner.nextDouble();
        scanner.nextLine();

        while (num2 > num1) {
            System.out.println("El segundo número debe ser menor que " + num1);
            num2 = scanner.nextDouble();
            scanner.nextLine();
        }

        System.out.println("Los números son: " + num1 + " y " + num2);
    }
}

```
