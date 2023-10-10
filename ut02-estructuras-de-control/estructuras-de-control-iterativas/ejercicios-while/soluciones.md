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

3\.

```java
import java.util.Scanner;

public class Ej3 {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("Introduce un número");
        double number = scanner.nextDouble();
        scanner.nextLine();

        System.out.println("¿Desea continuar? (S/N)");
        String res = scanner.nextLine();

        while(res.equals("S") || res.equals("s")) {
            System.out.println("Introduce un número");
            number = scanner.nextDouble();
            scanner.nextLine();

            System.out.println("¿Desea continuar? (S/N)");
            res = scanner.nextLine();
        }
    }
}

```

4\.

```java
import java.util.Scanner;

public class Ej4 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Introduce un número");
        int number = scanner.nextInt();
        scanner.nextLine();
        
        int counter = 1;
        while (number >= 0) {
            System.out.println("Introduce otro número");
            number = scanner.nextInt();
            scanner.nextLine();
            counter++;
        }

        System.out.println("Ha introducido " + counter);

    }
}

```

5\.

```java
import java.util.Random;
import java.util.Scanner;

public class Ej5 {
    public static void main(String[] args) {
        Random r = new Random();
        int n = r.nextInt(100); // G

        Scanner scanner = new Scanner(System.in);

        System.out.println("Trata de adivinar un  número del 0 al 99");

        int guess = scanner.nextInt();
        scanner.nextLine();

        while(guess != n) {
            if(guess > n) {
                System.out.println("Es menor");
            } else {
                System.out.println("Es mayor");
            }
            System.out.println("Trata de adivinar un  número del 0 al 99");

            guess = scanner.nextInt();
            scanner.nextLine();
        }

        System.out.println("Correcto, el número era " + guess);
    }
}

```

6\.

```java
import java.util.Scanner;

public class Ej6 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("Cuántos números deseas introducir");
        int n = scanner.nextInt();
        scanner.nextLine();

        while(n <= 0 ) {
            System.out.println("Por favor, introduca un valor mayor que cero");
            n = scanner.nextInt();
            scanner.nextLine();
        }

        int sum = 0;
        // for(int i=0;i<n;i++)
        int i = 0;
        while(i < n) {
            System.out.println("Introduce un número ");
            int number = scanner.nextInt();
            scanner.nextLine();
            sum = sum + number;
            i++;
        }

        double average = (double) sum / n;
        System.out.println("La media es " + average);
    }
}

```

7\.

```java
import java.util.Scanner;

public class Ej7 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Introduce un número");
        int number = scanner.nextInt();
        scanner.nextLine();

        int sum = number;
        while(number != 0) {
            System.out.println("Introduce un número");
            number = scanner.nextInt();
            scanner.nextLine();

            sum = sum + number;
        }

        System.out.println("La suma es " + sum);
    }
}

```

8\.

```java
import java.util.Scanner;

public class Ej8 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        int sumPositives = 0;
        int sumNegatives = 0;
        int zeros = 0;
        int positives = 0;
        int negatives = 0;

        int i = 0;
        while (i < 10) {
            System.out.println("Introduce un número");
            int number = scanner.nextInt();
            scanner.nextLine();

            if (number > 0) {
                positives++;
                sumPositives = sumPositives + number;
            } else if (number < 0) {
                negatives++;
                sumNegatives = sumNegatives + number;
            } else {
                zeros++;
            }

            i++;
        }

        double averagePositives = (double) sumPositives / positives;
        double averageNegatives = (double) sumNegatives / negatives;

        System.out.println("La media de positivos es " + averagePositives);
        System.out.println("La media de negativos es " + averageNegatives);
        System.out.println("El número de ceros es " + zeros);
    }
}

```
