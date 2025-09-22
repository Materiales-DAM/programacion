---
cover: ../../../.gitbook/assets/control-structures.gif
coverY: 0
---

# Soluciones Switch

1\. Escribe un programa que:

```java
package org.example.switchexercices;

import java.util.Scanner;

public class Ej1 {
    public static void main(String[] args) {
        System.out.println("¿Qué hora es?");
        Scanner scanner = new Scanner(System.in);
        int hora = scanner.nextInt();
        scanner.nextLine();

        switch (hora) {
            case 6, 7, 8, 9, 10, 11, 12:
                System.out.println("¡Buenos días!");
                break;
            case 13, 14, 15, 16, 17, 18, 19, 20:
                System.out.println("¡Buenas tardes!");
                break;
            case 0, 1, 2, 3, 4, 5, 21, 22, 23:
                System.out.println("¡Buenas noches!");
                break;
            default:
                System.out.println("Hora Inválida.");
                break;
        }
    }
} 
```

2\. Implementa la calculadora  (ejercicio 6 de If)  usando un switch en lugar de un if else

```java
package org.example.switchexercices;

import java.util.Scanner;

public class Calculator {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.println("Si quieres sumar pon + y si quieres restar pon -");
        String ope = sc.nextLine();
        switch (ope) {
            case "+" :
                System.out.println("Dime un número");
                double n1 = sc.nextDouble();
                sc.nextLine();
                System.out.println("Dame otro número");
                double n2 = sc.nextDouble();
                sc.nextLine();
                double sum = n1 + n2;
                System.out.println("Su suma es " + sum);
                break;
            case "-":
                System.out.println("Dame un número");
                int num1 = sc.nextInt();
                sc.nextLine();
                System.out.println("Dame otro maás");
                int num2 = sc.nextInt();
                sc.nextLine();
                int subs = num1 - num2;
                System.out.println("El resultado es " + subs);
                break;
            default:
                System.out.println("Operación inválida");
        }

    }
}
```

3\. Escribe un programa que:

```java
package org.example.switchexercices;

import java.util.Scanner;

public class Ej3 {
    public static void main(String[] args) {
        Scanner scanner=new Scanner(
                System.in
        );
        System.out.println("Dime una palabra de 8 caracteres");
        String word=scanner.nextLine();
        switch (word.length()){
            case 8:
                System.out.println("Es valido");
                break;
            default:
                System.out.println("No valido");
                break;
        }
    }
} 
```
