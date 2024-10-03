---
cover: ../../../.gitbook/assets/control-structures.gif
coverY: 0
---

# Soluciones Switch

1\. Escribe un programa que:

```java
package switchexercises;

import java.util.Scanner;

public class Switch1 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        int hour = scanner.nextInt();
        scanner.nextLine();

        switch (hour) {
            case 6, 7, 8, 9, 10, 11, 12:
                System.out.println("Buenos días");
                break;
            case 13, 14, 15, 16, 17, 18, 19, 20:
                System.out.println("Buenas tardes");
                break;
            case 0, 1, 2, 3, 4, 5, 21, 22, 23:
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
package switchexercises;

import java.util.Scanner;

public class Switch2 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Introduce la operación (+, -)");
        String operation = scanner.nextLine();
        switch (operation) {
            case "+":
                System.out.println("Introduce un número");
                double num1 = scanner.nextDouble();
                scanner.nextLine();
                System.out.println("Introduce otro número");
                double num2 = scanner.nextDouble();
                scanner.nextLine();

                double res = num1 + num2;

                System.out.println("El resultado es " + res);
                break;
            case "-":
                System.out.println("Introduce un número");
                int num3 = scanner.nextInt();
                scanner.nextLine();
                System.out.println("Introduce otro número");
                int num4 = scanner.nextInt();
                scanner.nextLine();

                double res2 = num3 - num4;

                System.out.println("El resultado es " + res2);
                break;
            default:
                System.out.println("Operación inválida " + operation);
        }
    }
}
```

3\. Escribe un programa que:

```java
package switchexercises;

import java.util.Scanner;

public class Switch3 {

    public static void main(String[] args) {
        // Crea un escaner
        Scanner scanner = new Scanner(System.in);
        //Pido una palabra de 8 carácteres
        System.out.println("Introduce una palabra de 8 carácteres");
        //Declaro una variable llamada sentence de tipo String.
        String sentence = scanner.nextLine();
        //verifica la longitud de la palabra introducida
        switch (sentence.length()) {
            // En el caso de que la paalbra tenga 8 carácteres dirá que es válido.>
            case 8:
                System.out.println("Es válido");
                break;

            default:
                // Y en el caso de que no, dirá que no es válido.
                System.out.println("No es válido");
        }
    }
} 
```
