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

4\.



```java
import java.util.Scanner;

public class Ejer4 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Introduce el año de inicio");
        int year1 = scanner.nextInt();
        scanner.nextLine();

        int year2 = scanner.nextInt();
        scanner.nextLine();

        for (int i = year1; i <= year2; i++) {
            // Aquí va a haber tantas iteraciones como year2 - year1
            // year1 toma el mismo valor en todas las iteraciones
            // year2 toma siempre el mismo valor en todas las iteraciones
            if (i % 4 == 0 && i % 100 != 0) {
                System.out.println(i);
            }
        }
    }
}

```

5\.



```java
import java.util.Scanner;

public class Ej5 {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("¿Cuántos números desea introducir?");
        int numbers = scanner.nextInt();
        scanner.nextLine();

        int negatives = 0;

        // numbers= 5
        for (int i = 0; i < numbers; i++) {
            // i=0, negatives =0, number=4 -> negatives=0
            // i=1, negatives=0, number=-3 -> negatives=1
            // i=2, negatives=1, number=2 -> negatives=1
            // i=3, negatives=1, number=-2 -> negatives=2
            // i=4, negatives=2, number=-5 -> negatives=3
            System.out.println("Introduzca un número:");
            int number = scanner.nextInt();
            scanner.nextLine();

            if (number < 0) {
                // negatives = negatives + 1;
                negatives++;
            }
        }
        // negatives=3
        System.out.println("La cantidad de negativos es " + negatives);
    }
}

```

6\.



```java
import java.util.Scanner;

public class Ej6 {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Cuántos números va a introducir");

        int numbers = scanner.nextInt();
        scanner.nextLine();

        int max = Integer.MIN_VALUE;
        // numbers= 3
        for (int i = 0; i < numbers; i++) {
            // i=0, number=3, max=0 --> max=3
            // i=1, number=2, max=3 --> max=3
            // i=2, number=5, max=3 --> max=5
            System.out.println("Introduce un número");
            int number = scanner.nextInt();
            scanner.nextLine();

            if(number > max) {
                max = number;
            }

        }

        System.out.println("El máximo es " + max);
    }
}

```

7\.



```java
import java.util.Scanner;

public class Ej7 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("Cuántos números desea introducir");
        int numbers = scanner.nextInt();
        scanner.nextLine();

        int sum = 0;
        // numbers = 3
        for (int i = 0; i < numbers; i++) {
            // i=0, sum=0, number=3 ---> sum =3
            // i=1, sum=3, number=2 ---> sum = 5
            // i=2, sum=5, number=4 ---> sum = 9
            System.out.println("Introduce un número");
            int number = scanner.nextInt();
            scanner.nextLine();

            sum = sum + number;
        }

        double average = (double) sum / numbers;

        System.out.println("La media es " + average);

    }
}

```

8\.



```java
import java.util.Scanner;

public class Ej8 {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Introduce un entero mayor que 1");
        int number = scanner.nextInt();
        scanner.nextLine();

        if(number <= 1) {
            System.out.println("Introduzca un número mayor que uno...");
        } else {
            // number = 7
            //  number % 2 != 0
            //  number % 3 != 0
            //  number % 4 != 0
            //  number % 5 != 0
            //  number % 6 != 0

            boolean isPrime = true;

            for (int i = 2; i < number; i++) {
                if(number % i == 0) {
                    isPrime = false;
                }
            }

            if(isPrime) {
                System.out.println("Es primo");
            } else {
                System.out.println("No es primo");
            }
        }
    }
}

```
