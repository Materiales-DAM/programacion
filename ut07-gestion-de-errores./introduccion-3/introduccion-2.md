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

# Propagación de excepciones

Una excepción es un evento que interrumpe el flujo normal de ejecución de un programa debido a algún error o condición inesperada. La propagación de excepciones se refiere al proceso mediante el cual una excepción se transmite a través de la pila de llamadas hasta que llegue a un método que capture la excepción con un try-catch o, en caso de que nadie la capture, finalice el programa.

Aquí tienes una explicación paso a paso de cómo se propagan las excepción:

```java
package org.ies.tierno.exceptions;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import java.util.InputMismatchException;
import java.util.Scanner;

public class TryCatchExample {
    private static final Logger log = LoggerFactory.getLogger(TryCatchExample.class);
    private final static Scanner scanner = new Scanner(System.in);
    
    public static void main(String[] args) {
        try {
            int numerator = askNumber("Introduce el numerador");
            
            int denominator = askNumber("Introduce el denominador");
            // invocamos a divide
            // Si se produce excepción el programa salta a los catch
            double res =  divide(numerator, denominator);
            // Mostramos el resultado
            log.info("El resultado es: " + res);
        } catch (InputMismatchException e) {
            // Si se produce InputMismatchException dentro del método askNumber lo capturamos aquí
            log.error("El número introducido es inválido", e);
        } catch (ArithmeticException e) {
            // Si se produce ArithmeticException dentro del método divide lo capturamos aquí
            log.error("No se puede dividir por cero", e);
        }
    }
    
    public static int askNumber(String message) {
        log.info(message);
        // Si el usuario introduce un valor no numérico provoca la excepción InputMismatchException
        // Como no hay try-catch se propaga al método que lo ha invocado
        int number = scanner.nextInt();
        scanner.nextLine();
        return number;
    }
    
    public static double divide(int numerator, int denominator) {
        // Produce una excepción cuando denominator es 0
        // Como no hay try - catch se propaga al método que lo ha invocado
        return (double) numerator / denominator;
    }
}
```
