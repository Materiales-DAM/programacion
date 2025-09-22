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
```

3\. Escribe un programa que:

```java
```
