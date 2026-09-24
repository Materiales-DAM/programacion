---
cover: ../../../.gitbook/assets/control-structures.gif
coverY: 0
---

# Soluciones while

1.  Escriba un programa que pida dos números enteros. El programa pedirá de nuevo el segundo número hasta que sea mayor que el primero. El programa terminará escribiendo los dos números.<br>

    ```java
    package org.ies.tierno;

    import java.util.Scanner;

    public class Ej1 {
        public static void main(String[] args) {
            Scanner scanner = new Scanner(System.in);

            System.out.println("Introduce un número:");
            int n1 = scanner.nextInt();
            scanner.nextLine();
            
            System.out.println("Introduce otro número:");
            int n2 = scanner.nextInt();
            scanner.nextLine();

            while (n2 <= n1) {
                System.out.println("El segundo número debe ser mayor que " + n1);
                System.out.println("Vuelva a introducir el segundo número: ");
                n2 = scanner.nextInt();
                scanner.nextLine();
            }

            System.out.println("Los números son " + n1 + " y " + n2);
        }
    }
    ```
2.  Escriba un programa que pida dos números decimales. El programa pedirá de nuevo el segundo número hasta que sea menor que el primero. El programa terminará escribiendo los dos números.<br>

    ```java
    ```
3. Escriba un programa que pida números mientras el usuario indique que quiere seguir introduciendo números. Para indicar que quiere seguir escribiendo números, el usuario deberá contestar S o s a la pregunta.
   * `Introduce numero: 2`
   * `¿Quieres seguir? S`
   *   `Introduce numero: 3`

       ```java
       ```
4.  Pedir números hasta que se teclee uno negativo, y mostrar cuántos números positivos se han introducido.<br>

    ```java
    ```
5. Realizar un juego para adivinar un número. Para ello se asigna a una variable n un número entero aleatorio, y luego ir pidiendo números indicando “mayor” o “menor” según sea mayor o menor con respecto a N. El proceso termina cuando el usuario acierta y se imprime el texto “exacto!”. Para generar un número aleatorio se puede usar la utilidad java.util.Random

```java
Random r = new Random(); 
int secret = r.nextInt(100); // Genera un numero aleatorio del 0 al 10 
```

```java
```

6.  Escribe un programa que pregunte cuántos números se van a introducir (si mete un valor menor que 1, debe volver a pedirlo hasta que no sea mayor o igual que 1), pida esos números y calcule la media de los mismo. La media se calcula sumando todos los números y dividiendo la suma entre la cantidad de números<br>

    ```java
    ```
7.  Pedir números hasta que se teclee un 0, mostrar la suma de todos los números introducidos al finalizar.<br>

    ```java
    ```
8.  Pedir 10 números. Mostrar la media de los números positivos, la media de los números negativos y la cantidad de ceros.<br>

    ```java
    ```
