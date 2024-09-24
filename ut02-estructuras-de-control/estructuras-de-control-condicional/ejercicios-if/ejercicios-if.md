---
cover: ../../../.gitbook/assets/control-structures.gif
coverY: 0
---

# Soluciones If

1\. Escribe un programa que:

```java
import java.util.Scanner;

public class If1 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("Introduce un número:");
        int n1 = scanner.nextInt();
        scanner.nextLine();

        System.out.println("Introduce otro número");
        int n2 = scanner.nextInt();
        scanner.nextLine();

        if (n1 > n2) {
            System.out.println("Es mayor");
        } else if (n1 < n2) {
            System.out.println("Es menor");
        } else {
            System.out.println("Es igual");
        }
    }
}
```

2\. Escribe un programa que:

```java
import java.util.Scanner;

public class If2 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("Introduce un número");
        int n = scanner.nextInt();
        scanner.nextLine();

        if (n == 0) {
            System.out.println("No es par ni impar");
        } else if (n % 2 == 0) {
            System.out.println("Es par");
        } else {
            System.out.println("Es impar");
        }
    }
}
```

3\. Escribe un programa que:

```java
import java.util.Scanner;

public class If3 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(
                System.in
        );

        System.out.println("Escribe un numero");
        int n = scanner.nextInt();
        scanner.nextLine();

        if (n < 0) {
            System.out.println("El numero es negativo");
        } else if (n > 0) {
            System.out.println("El numero es positivo");
        } else {
            System.out.println("El numero no es positivo ni negativo");
        }
    }
} 
```

4\. Escribe un programa que:

```java
import java.util.Scanner;

public class If4 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("Introduce una frase de 8 caracteres");
        String sentence = scanner.nextLine();

        if (sentence.length() > 8) {
            System.out.println("Demasiado largo");
        } else if (sentence.length() < 8) {
            System.out.println("Demasiado corto");
        } else {
            System.out.println("Correcto");
        }
    }
}
```

5\. Escribe un programa que:

```java
import java.util.Scanner;

public class If5 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(
                System.in
        );
        System.out.println("Introduce un número entero");
        int num1 = scanner.nextInt();
        scanner.nextLine();
        System.out.println("Introduce un nuevo número");
        int num2 = scanner.nextInt();
        scanner.nextLine();


        if (num1 > num2) {
            int sum = num1 + num2;
            System.out.println("El resultado es " + sum);
        } else if (num1 == num2) {
            int substract = num1 - num2;
            System.out.println("El resultado es " + substract);
        } else {
            int sum = num1 + num2;

            System.out.println("Introduce otro número");
            int num3 = scanner.nextInt();
            scanner.nextLine();
            if (num3 > sum) {
                System.out.println(num3 + " es mayor que " + num1 + " + " + num2);
            } else if (num3 < sum) {
                System.out.println(num3 + " es menor que " + num1 + " + " + num2);
            } else {
                System.out.println(num3 + " es igual que " + num1 + " + " + num2);
            }
        }
    }
}
```

6\. Escribe un programa que:

```java
import java.util.Scanner;

public class If6 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(
                System.in
        );

        System.out.println("¿Qué operación desea realizar? ");
        String operacion = scanner.nextLine();

        if (operacion.equals("+")) {
            System.out.println("Ingrese un número con decimales: ");
            double a = scanner.nextDouble();
            scanner.nextLine();

            System.out.println("Ingrese otro número con decimales: ");
            double b = scanner.nextDouble();
            scanner.nextLine();

            System.out.println("El resultado es: " + (a + b));
        } else if (operacion.equals("-")) {
            System.out.println("Ingrese un número decimal: ");
            int a = scanner.nextInt();
            scanner.nextLine();

            System.out.println("Ingrese otro número decimal: ");
            int b = scanner.nextInt();
            scanner.nextLine();

            System.out.println("El resultado es: " + (a - b));
        } else {
            System.out.println("Operación no permitida.");
        }
    }
} 
```
