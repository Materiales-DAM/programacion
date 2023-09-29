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

3\.



```java
import java.util.Scanner;

public class Ej3 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("Introduce un entero positivo");
        int n = 5;

        // sumatorio(5) = 0 + 1 + 2 + 3 + 4 +5


        int suma = 0;

        for (int i = 0; i <= n; i++) {
            // It0 i=0 suma=0 -> suma=0 (0) + 1 + 2 + 3 + 4 + 5
            // It1 i=1 suma=0 -> suma=1 (1) + 2 + 3 + 4 + 5
            // It2 i=2 suma=1 -> suma=3 (3) + 3 + 4 + 5
            // It2 i=3 suma=3 -> suma=6 (6) + 4 + 5
            // It2 i=4 suma=6 -> suma=10 (10) + 5
            // It2 i=5 suma=10 -> suma=15
            suma = suma + i;
        }
        // suma = (((((0 + 0) + 1) + 2) + 3) + 4) + 5

        System.out.println("El resultado es " + suma);

    }
}

```
