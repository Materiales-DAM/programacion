# Soluciones

1\.

```java
import java.util.Scanner;

public class Ej1 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("Cuántas veces desea repetir un mensaje");
        int times = scanner.nextInt();
        scanner.nextLine();

        System.out.println("Introduzca el mensaje");
        String sentence = scanner.nextLine();

        for (int i = 0; i < times; i++) {
            System.out.println(sentence);
        }
    }
}

```

2\.



```java
import java.util.Scanner;

public class Ej2 {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("Introduce un número");
        int num1 = scanner.nextInt();
        scanner.nextLine();

        System.out.println("Introduce otro número");
        int num2 = scanner.nextInt();
        scanner.nextLine();

        if (num2 > num1) {
            for (int i = num1; i <= num2; i++) {
                System.out.println(i);
            }
        } else {
            for (int i = num2; i <= num1; i++) {
                System.out.println(i);
            }
        }
    }
}

```
