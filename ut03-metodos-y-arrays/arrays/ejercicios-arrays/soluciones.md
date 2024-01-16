# Soluciones

1\.



```java
public class Ej1 {
    public static void main(String[] args) {

        int[] numbers = {4, 8, 9, 1};

        for (int i = 0; i < numbers.length; i++) {
            int number = numbers[i];
            System.out.println(number);
        }
    }
}

```

2\.



```java
public class Ej2 {

    public static void main(String[] args) {

        double[] numbers = {3.4, 5.2, 3.7};

        System.out.println(numbers[numbers.length - 1]);
    }
}

```

3\.



```java
public class Ej3 {

    public static void main(String[] args) {
        int[] numbers = {4, 8, 9 , 1};

        int sum = 0;

        for (int i = 0; i < numbers.length; i++) {
            int number = numbers[i];
            sum = sum + number;
        }

        System.out.println(sum);
    }
}

```

4\.



```java
import java.util.Scanner;

public class Ej4 {
    private static Scanner scanner = new Scanner(System.in);

    public static void main(String[] args) {
        System.out.println("¿Cuántos nombres desea introducir?");
        int size = scanner.nextInt();
        scanner.nextLine();

        String[] names = new String[size];

        for (int i = 0; i < names.length; i++) {
            System.out.println("Introduce un nombre");
            String name = scanner.nextLine();
            names[i] = name;
        }

        for (int i = 0; i < names.length; i++) {
            System.out.println(names[i]);
        }
    }
}

```
