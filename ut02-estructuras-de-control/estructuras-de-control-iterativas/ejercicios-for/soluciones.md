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
