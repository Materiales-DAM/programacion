---
cover: ../../.gitbook/assets/quality-assurance-code-bug.jpg
coverY: 110.50526315789473
layout:
  cover:
    visible: true
    size: full
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Captura de excepciones

Es posible definir el comportamiento de un programa ante una excepción mediante la estructura de control **try-catch**.  A esta técnica, se le denomina captura de excepciones.

## Sintaxis

```java
try {
    // Aquí va el código que podría lanzar una excepción
    ...
} catch (Exception1 e) {
    // Aquí definimos qué hacer en caso de que haya ocurrido la excepción Exception1
} catch (Exception2 e) {
    // Aquí definimos qué hacer en caso de que haya ocurrido la excepción Exception2
}
```

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption><p>Flujo try - catch</p></figcaption></figure>

Por ejemplo, veamos un programa que pide dos números double y calcula su división

{% code lineNumbers="true" %}
```java
package org.ies.tierno.exceptions;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import java.util.InputMismatchException;
import java.util.Scanner;

public class TryCatchExample {
    private static final Logger log = LoggerFactory.getLogger(TryCatchExample.class);
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        try {
            log.info("Introduce el numerador");
            int numerator = scanner.nextInt();
            scanner.nextLine();
            log.info("Introduce el denominador");
            int denominator = scanner.nextInt();
            scanner.nextLine();
            // Calculamos la división
            double res =  numerator / denominator;
            // Mostramos el resultado
            log.info("El resultado es: " + res);
        } catch (InputMismatchException e) {
            // Esto se va a ejecutar si ocurre la excepción InputMismatchException
            // Usamos el logger para mostrar la stacktrace de la excepción
            log.error("El valor introducido es inválido", e);
        } catch (ArithmeticException e) {
            // Esto se va a ejecutar si ocurre la excepción ArithmeticException
            // Usamos el logger para mostrar la stacktrace de la excepción
            log.error("No se puede dividir por cero", e);
        }
    }
}
```
{% endcode %}

Este programa podría lanzar una excepción en:

* &#x20;Línea 16: si el usuario escribe algo que no es un número esta línea lanzará la excepción `InputMismatchException`.
* Línea 19: si el usuario escribe algo que no es un número esta línea lanzará la excepción `InputMismatchException`.
* Línea 22: si denominator es 0, se producirá la excepción `ArithmeticException`.
