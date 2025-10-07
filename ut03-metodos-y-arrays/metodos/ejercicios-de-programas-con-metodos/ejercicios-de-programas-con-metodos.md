---
cover: ../../../.gitbook/assets/method.jpg
coverY: 0
---

# Soluciones de programas con métodos

1. Crea un programa que defina los siguientes métodos:
   1. Un método que calcule la suma de sus dos parámetros enteros y devuelva el resultado
   2.  Un método que reciba un entero por parámetro e imprima el texto “El resultado es: ” y el parámetro recibido. Este método no devolverá nada\


       En el main pide dos números enteros, e invoca el primer método pasando esos valores, después se invocará el segundo método con el resultado de la invocación del primero

       ```java
       package org.ies.tierno;

       import java.util.Scanner;

       public class Ej1 {
           public static Scanner scanner = new Scanner(System.in);

           public static void main(String[] args) {
               int n1 = askNumber();
               int n2 = askNumber();
               int res = addition(n1, n2);
               print(res);
           }

           public static int askNumber() {
               System.out.println("Introduce un número entero");
               int n = scanner.nextInt();
               scanner.nextLine();
               return n;
           }

           public static int addition(int n1, int n2) {
               int res = n1 + n2;
               return res;
           }

           public static void print(int res) {
               System.out.println("El resultado es: " + res);
           }
       } 
       ```
2. Crea un programa que defina los siguientes métodos:
   1. Un método que calcule la multiplicación de sus dos parámetros enteros y devuelva el resultado
   2. Un método que reciba un entero por parámetro e imprima el texto “El resultado es: ” y el parámetro recibido. Este método no devolverá nada

En el main pide dos números enteros, e invoca el primer método pasando esos valores, después se invocará el segundo método con el resultado de la invocación del primero\


```java
package org.ies.tierno;

import java.util.Scanner;

public class Ej2 {
    public static Scanner scanner = new Scanner(System.in);

    public static void main(String[] args) {
        int n1 = askNumber();
        int n2 = askNumber();
        int res = multiply(n1, n2);
        print(res);
    }

    public static int askNumber() {
        System.out.println("Introduce un número entero");
        int n = scanner.nextInt();
        scanner.nextLine();
        return n;
    }

    public static int multiply(int n1, int n2) {
        return n1 * n2;
    }

    public static void print(int res) {
        System.out.println("El resultado es: " + res);
    }
} 
```

3. Crea un programa que muestre un menú con las siguientes opciones:

* Saluda: Pide al usuario su nombre y muestra en pantalla el texto `Hola, <nombre introducido>`. Por ejemplo, si introduce el nombre Bob aparecerá el texto `Hola, Bob`
* Grita: Pide al usuario su nombre y muestra en pantalla el texto `Cuidado <nombre introducido>!`. Por ejemplo, si introduce el nombre Bob aparecerá el texto`Cuidado, Bob!`
* Salir

Para implementar este programa crea los siguiente métodos:

* Un método que sirva para imprimir en pantalla el menú y lee la opción elegida por el usuario, al final devuelve la opción elegida
* Un método `askName()` que pide al usuario su nombre y lo devuelve
* Un método que contiene todo el código de la opción "Saluda": Pide al usuario su nombre y muestra en pantalla el texto `Hola, <nombre introducido>`. Por ejemplo, si introduce el nombre Bob aparecerá el texto `Hola, Bob`
* Un método que contiene todo el código de la opción Grita: Pide al usuario su nombre y muestra en pantalla el texto `Cuidado <nombre introducido>!`. Por ejemplo, si introduce el nombre Bob aparecerá el texto`Cuidado, Bob!`
* Un método que implementa el bucle del menú interactivo e invoca a los métodos anteriores para realizar las distintas tareas
*   En el método `main` se invocará al método que implementa el bucle del menú interactivo.\


    ```java
    ```

4. Crea un programa de menú interactivo que permita al usuario realizar las siguientes operaciones:

* Sumar dos números: los pide, los suma y muestra el resultado en pantalla.
* Restar dos números: los pide, los resta y muestra el resultado en pantalla.
* Multiplicar dos números: los pide, los multiplica y muestra el resultado en pantalla.
* Salir

Implementa el programa creando métodos para:.

* Mostrar menú y elegir opción
* Un método que ejecute la opción sumar
* Un método que ejecute la opción restar
* Un método que ejecute la opción multiplicar
* Un método que implemente el bucle del menú
*   En el `main` invoca el método del bucle del menú.\


    ```java
    ```

5\. Escribe un programa con estos métodos:

* Un método que dado un entero, devuelva el sumatorio de cero a ese número. Por ejemplo, si se pasa el 6, el resultado será 0 +1 +2 +3 +4 +5+ 6.
* Un método que dado un número entero, devuelve el factorial de ese número. Por ejemplo, si se pasa el 6, el resultado será 1 \* 2 \* 3 \* 4 \* 5 \* 6
* Un método que dados cuatro números enteros, calcula la media y la devuelve.
* Un método que muestre las siguientes opciones,:
  * Sumatorio
  * Factorial
  * Media
  * Salir
* Un método que imprima el menú y pida una opción al usuario, luego la devuelve
*   En el `main` se creará el menú interactivo usando lo anterior\


    ```java
    ```
