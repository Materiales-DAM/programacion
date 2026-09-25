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
    package org.ies.tierno;

    import java.util.Scanner;

    public class Buclewhile2 {
        public static void main(String[] args) {
            Scanner scanner = new Scanner(System.in);
            System.out.println("Escribe el primer numero");
            double num1 = scanner.nextDouble();
            scanner.nextLine();

            System.out.println("Escribe el segundo numero");
            double num2 = scanner.nextDouble();
            scanner.nextLine();

            while (num2 > num1){
                System.out.println("Introduce otro numero menor que le primero");
                num2 = scanner.nextDouble();
                scanner.nextLine();
            }
            System.out.println("Los numeros son " + num1 + " y " + num2);
        }
    } 
    ```
3. Escriba un programa que pida números mientras el usuario indique que quiere seguir introduciendo números. Para indicar que quiere seguir escribiendo números, el usuario deberá contestar S o s a la pregunta.
   * `Introduce numero: 2`
   * `¿Quieres seguir? S`
   *   `Introduce numero: 3`

       ```java
       package org.ies.tierno;

       import java.util.Scanner;

       public class While3 {
           public static void main(String[] args) {
               Scanner scanner = new Scanner(System.in);
               String word ="S";
               while (word.equalsIgnoreCase("S")) {
                   System.out.println("Introduce un número");
                   int num = scanner.nextInt();
                   scanner.nextLine();
                   System.out.println("Has introducido "+ num);
                   System.out.println("Quieres seguir? ");
                   word = scanner.nextLine();
               }
           }
       } 
       ```
4.  Pedir números hasta que se teclee uno negativo, y mostrar cuántos números positivos se han introducido.<br>

    ```java
    package org.ies.tierno;

    import java.util.Scanner;

    public class Main {
        public static void main(String[] args) {
            Scanner scanner = new Scanner(System.in);

            System.out.println("Introduzca un número: ");
            int num = scanner.nextInt();
            scanner.nextLine();

            int count = 0;

            while(num>0){
                System.out.println("Introduzca otro número: ");
                num = scanner.nextInt();
                scanner.nextLine();

                count++;
            }
            System.out.println("Se han introducido "+ count +" números positivos");
        }
    } 
    ```
5. Realizar un juego para adivinar un número. Para ello se asigna a una variable n un número entero aleatorio, y luego ir pidiendo números indicando “mayor” o “menor” según sea mayor o menor con respecto a N. El proceso termina cuando el usuario acierta y se imprime el texto “exacto!”. Para generar un número aleatorio se puede usar la utilidad java.util.Random

```java
Random r = new Random(); 
int secret = r.nextInt(100); // Genera un numero aleatorio del 0 al 100 
```

```java
package org.ies.tierno;

import java.util.Scanner;
import java.util.Random;

public class Ejercicio5 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Random r = new Random();
        int secret = r.nextInt(10);
        System.out.println("Adivina el número del 1 al 10");
        int number = -1;

        while (number != secret) {
            System.out.println("Introduce un número: ");
            number = scanner.nextInt();
            scanner.nextLine();
            if (number > secret) {
                System.out.println("Tu número es mayor");
            } else if (number < secret) {
                System.out.println("Tu número es menor");
            }
        }
        System.out.println("exacto!");
    }
} 
```

6.  Escribe un programa que pregunte cuántos números se van a introducir (si mete un valor menor que 1, debe volver a pedirlo hasta que no sea mayor o igual que 1), pida esos números y calcule la media de los mismo. La media se calcula sumando todos los números y dividiendo la suma entre la cantidad de números<br>

    ```java
    package While;

    import java.util.Scanner;

    public class EJ6 {
        public static void main(String[] args) {
            System.out.println("¿Cuantos números se van a introducir?");
            Scanner scanner = new Scanner(System.in);
            int num1 = scanner.nextInt();
            scanner.nextLine();

            while (num1<1) {
                System.out.println("Dame otro número");
                num1 = scanner.nextInt();
                scanner.nextLine();
            }
            
            int sum= 0;
            System.out.println("Dime los números");
            int i = 0;
            while (i < num1) {
                int num = scanner.nextInt();
                scanner.nextLine();
                sum += num;
                i++;
            }

            double avg = (double) sum / num1;

            System.out.println("La media es: " + avg);
        }
    } 
    ```
7.  Pedir números hasta que se teclee un 0, mostrar la suma de todos los números introducidos al finalizar.<br>

    ```java
    ```
8.  Pedir 10 números. Mostrar la media de los números positivos, la media de los números negativos y la cantidad de ceros.<br>

    ```java
    ```
