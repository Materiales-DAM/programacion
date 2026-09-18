---
cover: ../../../.gitbook/assets/control-structures.gif
coverY: 0
---

# Soluciones If

1\. Escribe un programa que:

```java
package org.ies.tierno;

import java.util.Scanner;

public class Compare {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Introduce un número:");
        int n1 = scanner.nextInt();
        scanner.nextLine();

        System.out.println("Introduce otro número:");
        int n2 = scanner.nextInt();
        scanner.nextLine();

        if (n1 > n2) {
            System.out.println("Es mayor");
        } else if (n1 < n2) {
            System.out.println("Es menor");
        } else  {
            System.out.println("Son iguales");
        }
    }
}

```

2\. Escribe un programa que:

```java
package org.ies.tierno;

import java.util.Scanner;

public class IsEven {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Introduce un número:");
        int n = scanner.nextInt();
        scanner.nextLine();

        if (n == 0) {
            System.out.println("no es par ni impar");
        } else if (n % 2 == 0) {
            System.out.println("es par");
        } else {
            System.out.println("es impar");
        }
    }
}

```

3\. Escribe un programa que:

```java
package org.ies.tierno;

import java.util.Scanner;

public class ShowSign {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Introduce un número:");
        int n = scanner.nextInt();
        scanner.nextLine();

        if (n == 0) {
            System.out.println("No es positivo ni negativo");
        } else if (n > 0) {
            System.out.println("es positivo");
        } else {
            System.out.println("es negativo");
        }
    }
}

```

4\. Escribe un programa que:

```java
package org.ies.tierno;

import java.util.Scanner;

public class StringSizeCheck {
    public static void main(String[] args) {
        System.out.println("dime una palabra de ocho letras");
        Scanner scanner = new Scanner(System.in);
        scanner.nextLine();
        String word = scanner.nextLine();
        int length = word.length();

        if (length == 8) {
            System.out.println("esta bien");
        } else if (length > 8) {
            System.out.println("es muy grande");
        } else {
            System.out.println("es muy pequeña");
        }
    }
} 
```

5\. Escribe un programa que:

```java
package org.ies.tierno;

import java.util.Scanner;

public class Ejercicio5 {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        System.out.println("Introduce un número: ");
        int a = scanner.nextInt();
        scanner.nextLine();

        System.out.println("Introduce otro número: ");
        int b = scanner.nextInt();
        scanner.nextLine();

        if (a > b) {
            int suma = a + b;
            System.out.println("El resultado es: " + suma);

        } else if (a < b) {
            int resta = a - b;
            System.out.println("El resultado es: " + resta);

        } else {
            System.out.println("Introduce otro número: ");
            int c = scanner.nextInt();
            scanner.nextLine();
            int suma = a + b;

            if (c > suma) {
                System.out.println("c es mayor que a + b");

            } else if (c < suma) {
                System.out.println("c es menor que a + b");

            } else {
                System.out.println("c es igual que a + b");
            }
        }
    }
} 
```

6\. Escribe un programa que:

```java
package org.ies.tierno;

import java.util.Scanner;

public class Calculator {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        System.out.println("Elige una operacion: + o -");
        String operacion = scanner.nextLine();
        if (operacion.equals("+")) {
            System.out.println("Dime un valor doble a");
            double number = scanner.nextDouble();
            scanner.nextLine();

            System.out.println("Dime otro valor doble b");
            double number1 = scanner.nextDouble();
            scanner.nextLine();

            double res = (number + number1);
            System.out.println(res);
        } else if (operacion.equals("-")) {
            System.out.println("Dime un valor entero a");
            int number3 = scanner.nextInt();
            scanner.nextLine();

            System.out.println("Dime otro valor entero b");
            int number4 = scanner.nextInt();
            scanner.nextLine();

            int res1 = number3 - number4;
            System.out.println(res1);
        } else {
            System.out.println("operacion invalida");
        }
    }
} 
```
