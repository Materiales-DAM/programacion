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

# Excepciones

Las excepciones son errores que ocurren durante la ejecución del programa y pueden provocar que el programa se detenga inesperadamente.&#x20;

## StackTrace

El "stack trace" (traza de pila) de una excepción en Java es un registro detallado de las llamadas de método que se estaban ejecutando en el momento en que ocurrió la excepción. Esta traza de pila es una herramienta invaluable para el diagnóstico de errores, ya que proporciona información sobre qué métodos se estaban ejecutando y en qué punto del código se produjo la excepción.

Cuando se lanza una excepción y no se maneja en el mismo método, Java "desenrolla" la pila de llamadas para encontrar un bloque `try-catch` que pueda manejar la excepción. Durante este proceso, Java registra cada método que se estaba ejecutando en ese momento.

El stack trace de una excepción generalmente se muestra en la consola cuando ocurre un error durante la ejecución del programa. La traza de pila muestra los nombres de los métodos y las clases, junto con los números de línea del código donde se produjo la excepción. Esto ayuda a identificar exactamente qué parte del código causó el problema.

Aquí hay un ejemplo simplificado de una traza de pila:

```log
Exception in thread "main" java.lang.NullPointerException
    at com.example.Main.metodoB(Main.java:15)
    at com.example.Main.metodoA(Main.java:10)
    at com.example.Main.main(Main.java:5)
```

En este ejemplo, la excepción `NullPointerException` ocurrió en el método `metodoB()` de la clase `Main` en la línea 15 del archivo `Main.java`. El método `metodoB()` fue llamado desde el método `metodoA()` en la línea 10, y a su vez, el método `metodoA()` fue llamado desde el método `main()` en la línea 5.

Al analizar la traza de pila, puedes identificar la secuencia de llamadas de método que condujeron al error, lo que te ayuda a comprender mejor el flujo de ejecución y a diagnosticar y corregir el problema en tu código.

## Excepciones causadas por bugs

Las siguientes excepciones siempre están causadas por un error en el código, por tanto la manera de solucionarlas es localizar el problema de codificación y arreglarlo.

<table data-full-width="true"><thead><tr><th width="305">Excepción</th><th>Descripción</th></tr></thead><tbody><tr><td>NullPointerException</td><td>Se produce cuando se trata de invocar a un método o campo de una variable cuyo valor es null. Este error es señal de la existencia de un bug.</td></tr><tr><td>ArrayIndexOutOfBoundsException</td><td>Ocurre cuando se trata de acceder a una posición de un array que no existe. Por ejemplo si se accede a la posición 3 de un array de tamaño 2.</td></tr><tr><td>ArithmeticException</td><td>Ocurre cuando se ejecuta una operación aritmética inválida. Por ejempló 0 / 0</td></tr><tr><td>ClassCastException</td><td>Ocurre cuando se trata de hacer casting de tipos incompatibles</td></tr><tr><td>NumberFormatException</td><td><p>Ocurre cuando se trata de convertir un String en un número y el String contiene caracteres que no permiten realizar la operación. Por ejemplo:</p><p>int num = Integer.parseInt("cien");</p></td></tr></tbody></table>

## Excepciones causadas por causas externas

Estas excepciones están causadas por cuestiones ajenas a la codificación, por lo que no es posible evitar que ocurran modificando el código del programa.&#x20;

<table data-full-width="true"><thead><tr><th width="305">Excepción</th><th>Descripción</th></tr></thead><tbody><tr><td>InputMismatchException</td><td>Esta excepción está vinculada al Scanner, ocurre cuando se trata de leer un número pero el usuario mete letras.</td></tr><tr><td>IOException</td><td>Se produce cuando hay algún fallo en una operacion del lectura / escritura (no queda espacio en disco, no se encuentra un archivo...)</td></tr></tbody></table>
