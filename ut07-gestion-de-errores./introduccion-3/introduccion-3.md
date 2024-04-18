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

# Jerarquía de excepciones

Las distintas excepciones existentes conforman la siguiente jerarquía de clases

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption><p>Jerarquía de excepciones y errores</p></figcaption></figure>

Como se puede ver,  `Exception` es la clase padre de todas las excepciones existentes. Podemos clasificar las excepciones en dos tipos:

## Unchecked Exceptions

Son aquellas excepciones que heredan directa o indirectamente de RuntimeException. Este tipo de excepciones pueden ocurrir durante la ejecución de un programa y generalmente son causadas por errores en el código del programador o por situaciones impredecibles.&#x20;

Es decisión del programador capturar (o no) este tipo de excepciones, el compilador no nos va a obligar a capturarlas.

Ejemplos comunes de excepciones de tiempo de ejecución son **`NullPointerException`**, **`ArrayIndexOutOfBoundsException`**, **`ArithmeticException`**, etc.

## Checked Exceptions

Este tipo de excepciones son las que no heredan de `RuntimeException`. El compilador obliga a manejar este tipo de excepciones de manera explícita de una de estas dos formas:

* **Capturándola** mediante un bloque `try-catch`&#x20;
* **Propagando** la excepción de manera explícita  (`throws`).&#x20;

Ejemplos comunes de Checked Exceptions son **`IOException`**, **`SQLException`**, etc...&#x20;

### Ejemplo con captura

Por ejemplo, este programa lee la primera línea del fichero que pida el usuario

```java
package org.example;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import java.io.BufferedReader;
import java.io.FileNotFoundException;
import java.io.FileReader;
import java.io.IOException;
import java.util.InputMismatchException;
import java.util.Scanner;

public class ReadFileExample {
    private static final Logger log = LoggerFactory.getLogger(ReadFileExample.class);
    
    public static void main(String[] args){
        Scanner scanner = new Scanner(System.in);
        log.info("Introduzca el path al fichero que desea leer");
        String file = scanner.nextLine();
        String firstLine = readFirstLine(file);
        System.out.println(firstLine);
    }
    
    public static String readFirstLine(String file) {
        try {
            BufferedReader reader = new BufferedReader(new FileReader(file));
            return reader.readLine();
        } catch (FileNotFoundException e) {
            log.error("No se ha encontrado el archivo " + file);
            return null;
        } catch (IOException e) {
            log.error("No se ha podido leer la línea", e);
            return null;
        }
    }
}

```

### Ejemplo con propagación

Por ejemplo, este programa lee la primera línea del fichero que pida el usuario

```java
package org.example;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import java.io.BufferedReader;
import java.io.FileNotFoundException;
import java.io.FileReader;
import java.io.IOException;
import java.util.InputMismatchException;
import java.util.Scanner;

public class ReadFileExample {
    private static final Logger log = LoggerFactory.getLogger(ReadFileExample.class);
    
    public static void main(String[] args){
        Scanner scanner = new Scanner(System.in);
        log.info("Introduzca el path al fichero que desea leer");
        String file = scanner.nextLine();
        
        try {
            String firstLine = readFirstLine(file);
            System.out.println(firstLine);
        } catch (FileNotFoundException e) {
            log.error("No se ha encontrado el archivo " + file);
        } catch (IOException e) {
            log.error("No se ha podido leer la línea", e);
        }
    }
    
    public static String readFirstLine(String file) throws FileNotFoundException, IOException {
        BufferedReader reader = new BufferedReader(new FileReader(file));
        return reader.readLine();
    }
}
```
