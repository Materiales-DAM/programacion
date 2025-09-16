---
cover: ../../.gitbook/assets/quality-assurance-code-bug.jpg
coverY: 110.50526315789473
---

# illlegal start of expression

Puede ser causado por

## Un método declarado dentro de otro método



{% code lineNumbers="true" %}
```java
package org.ies.tierno;

import java.util.InputMismatchException;
import java.util.Scanner;


public class IllegalStartExpression {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);

        System.out.println("INtroduce un mensaje");
        String hello = scanner.nextLine();
        if (hello.length() < 6) {
            System.out.println("Mensaje demasiado corto");
        } else {
            System.out.println(hello.charAt(5));
        }

        try {
            System.out.println("Introduce tu edad");
            int age = scanner.nextInt();
            scanner.nextLine();
            System.out.println("Edad: " + age);
        } catch (InputMismatchException e) {
            System.out.println("Edad inválida");
        }
    
    public int suma(int a, int b) {
        return a + b;
    }
}
}
```
{% endcode %}

La salida del compilador es

```log
/home/mikel/errors/src/main/java/org/ies/tierno/IllegalStartExpression.java:29:5
java: illegal start of expression
```

## Falta una llave de cierre

Se está intentando usar una variable que no existe, está mal escrita o no está en el scope

{% code lineNumbers="true" %}
```java
package org.ies.tierno;

import java.util.InputMismatchException;
import java.util.Scanner;


public class IllegalStartExpression {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);

        System.out.println("INtroduce un mensaje");
        String hello = scanner.nextLine();
        if (hello.length() < 6) {
            System.out.println("Mensaje demasiado corto");
        } else {
            System.out.println(hello.charAt(5));
        }

        try {
            System.out.println("Introduce tu edad");
            int age = scanner.nextInt();
            scanner.nextLine();
            System.out.println("Edad: " + age);
        } catch (InputMismatchException e) {
            System.out.println("Edad inválida");
        }

    public int suma(int a, int b) {
        return a + b;
    }

}
```
{% endcode %}

La salida del compilador es

```log
/home/mikel/errors/src/main/java/org/ies/tierno/IllegalStartExpression.java:29:5
java: illegal start of expression
```
