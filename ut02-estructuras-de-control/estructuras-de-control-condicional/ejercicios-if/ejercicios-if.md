---
cover: ../../../.gitbook/assets/control-structures.gif
coverY: 0
---

# Soluciones If

1\. Escribe un programa que:

```java
package org.example.ifexercises;

import java.util.Scanner;

public class Compare {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(
                System.in
        );

        System.out.println("Dime un número");
        double number = scanner.nextDouble();
        scanner.nextLine();

        System.out.println("Dime otro número");
        double number2 = scanner.nextDouble();
        scanner.nextLine();
        if (number > number2) {
            System.out.println("Es mayor");
        } else if (number < number2) {
            System.out.println("Es menor");
        } else {
            System.out.println("Es igual");
        }
    }
}

```

2\. Escribe un programa que:

```java
package org.example.ifexercises;

import java.util.Scanner;

public class IsEven {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("Introduce un número entero");
        int num1 = scanner.nextInt();
        scanner.nextLine();

        if (num1 == 0) {
            System.out.println("No es ni PAR ni IMPAR");
        } else if (num1 % 2 == 0) {
            System.out.println("Es PAR");
        } else {
            System.out.println("Es IMPAR");
        }
    }
} 

```

3\. Escribe un programa que:

```java
package org.example.ifexercises;

import java.util.Scanner;

public class ShowSign {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Dime un numero entero: ");
        int num1 = scanner.nextInt();
        scanner.nextLine();

        if (num1 == 0) {
            System.out.println(num1 + " no es ni positivo ni negativo");
        } else if (num1 > 0) {
            System.out.println(num1 + " es un numero positivo");
        } else {
            System.out.println(num1 + " es un numero negativo");
        }
    }
} 
```

4\. Escribe un programa que:

```java
package org.example.ifexercises;

import java.util.Scanner;

public class StringSizeCheck {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("Introduzca una contraseña de 8 digitos");
        String password = scanner.nextLine();

        if (password.length() < 8) {
            System.out.println("Demasiado pequeño");
        } else if (password.length() > 8) {
            System.out.println("Demasiado grande");
        } else {
            System.out.println("Es valida");
        }
    }
} 

```

5\. Escribe un programa que:

```java
package org.example.ifexercises;

import java.util.Scanner;

public class SumSubs {
    public static void main(String[] args){
        Scanner scanner = new Scanner(System.in);

        System.out.print("Introduzca un primer número: ");
        var a = scanner.nextInt();
        scanner.nextLine();

        System.out.print("Introduzca un segundo número; ");
        var b = scanner.nextInt();
        scanner.nextLine();

        if (b < a){
            var sum = a+b;
            System.out.print(sum);
        } else if (a<b) {
            var res = a - b;
            System.out.print(res);
        } else {
            var sum = a+b;

            System.out.print("Introduzca un tercer número: ");
            var c = scanner.nextInt();
            scanner.nextLine();

            if (c < sum){
                System.out.print("c es menor que a + b");
            } else if (c > sum) {
                System.out.print("c es mayor que a + b");

            } else {
                System.out.print("c es igual a a+b");
            }
        }

    }
}

```

6\. Escribe un programa que:

```java
```
