---
cover: ../../../.gitbook/assets/control-structures.gif
coverY: 0
---

# Soluciones Switch

1\. Escribe un programa que:

```java
package org.ies.tierno;

import java.util.Scanner;

public class SwEj1 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("Introduzca un número: ");
        int number = scanner.nextInt();
        scanner.nextLine();

        switch (number){
            case 6, 7, 8, 9, 10, 11, 12:
                System.out.println("Buenos días");
            break;
            case 13, 14, 15, 16, 17, 18, 19, 20:
                System.out.println("Buenaw tardes");
            break;
            case 21, 22, 23, 0, 1, 2, 3, 4, 5:
                System.out.println("Buenas noches");
            break;
            default:
                System.out.println("Hora inválida");
        }
    }
} 
```

2\. Implementa la calculadora  (ejercicio 6 de If)  usando un switch en lugar de un if else

```java
package org.ies.tierno;

import java.util.Scanner;

public class Ejercicio2 {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        System.out.println("Elige una operación: + o -");
        String operacion = scanner.nextLine();
        
        switch (operacion) {
            case "+":
                System.out.println("Introduce un número: ");
                double a = scanner.nextDouble();
                scanner.nextLine();

                System.out.println("Introduce otro número: ");
                double b = scanner.nextDouble();
                scanner.nextLine();

                double suma = a + b;
                System.out.println("La suma es: " + suma);
                break;
            case "-":
                System.out.println("Introduce un número: ");
                int c = scanner.nextInt();
                scanner.nextLine();

                System.out.println("Introduce otro número: ");
                int d = scanner.nextInt();
                scanner.nextLine();

                int resta = c - d;
                System.out.println("La resta es: " + resta);
                break;
            default:
                System.out.println("Operación inválida");
        }
    }
} 
```

3\. Escribe un programa que:

```java
```
