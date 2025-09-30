---
cover: ../../../.gitbook/assets/control-structures.gif
coverY: 0
---

# Soluciones while

1.  Escriba un programa que pida dos números enteros. El programa pedirá de nuevo el segundo número hasta que sea mayor que el primero. El programa terminará escribiendo los dos números.\


    ```java
    package org.example.whilexercices;

    import java.util.Scanner;

    public class Ej1 {
        public static void main(String[] args) {
            Scanner scanner = new Scanner(System.in);

            System.out.println("Introduce el primer numero");

            int num1 = scanner.nextInt();
            scanner.nextLine();

            System.out.println("Introduce el segundo numero");

            int num2 = scanner.nextInt();
            scanner.nextLine();

            while (num2 <= num1) {
                System.out.println("El segundo numero ha de ser mayor al primero");
                num2 = scanner.nextInt();
                scanner.nextLine();
            }
            System.out.println(num1 + " " + num2);
        }
    }

    ```
2.  Escriba un programa que pida dos números decimales. El programa pedirá de nuevo el segundo número hasta que sea menor que el primero. El programa terminará escribiendo los dos números.\


    ```java
    package org.example.whilexercices;

    import java.util.Scanner;

    public class Ej2 {
        public static void main(String[] args) {
            Scanner scanner = new Scanner(System.in);

            System.out.println("Introduce el primer numero");

            double num1 = scanner.nextDouble();
            scanner.nextLine();

            System.out.println("Introduce el segundo numero");

            double num2 = scanner.nextDouble();
            scanner.nextLine();

            while (num2 >= num1) {
                System.out.println("El segundo numero ha de ser menor que el primero");
                num2 = scanner.nextInt();
                scanner.nextLine();
            }
            System.out.println(num1 + " " + num2);
        }
    }

    ```
3. Escriba un programa que pida números mientras el usuario indique que quiere seguir introduciendo números. Para indicar que quiere seguir escribiendo números, el usuario deberá contestar S o s a la pregunta.
   * `Introduce numero: 2`
   * `¿Quieres seguir? S`
   *   `Introduce numero: 3`

       ```java
       package org.example.whilexercices;

       import java.util.Scanner;

       public class Ej3 {
           public static void main(String[] args){
               Scanner scanner = new Scanner(System.in);

               var askNumber = true;

               while(askNumber){
                   System.out.print("Introduzca un número: ");
                   var num = scanner.nextDouble();
                   scanner.nextLine();

                   System.out.print("¿Desea continuar? ");
                   var response = scanner.nextLine();

                   askNumber = response.equalsIgnoreCase("S");
               }
           }
       } 
       ```
4.  Pedir números hasta que se teclee uno negativo, y mostrar cuántos números positivos se han introducido.\


    ```java
    package org.example.whilexercices;

    import java.util.Scanner;

    public class Ej4 {
        public static void main(String[] args) {
            Scanner scanner = new Scanner(System.in);
            int numero = 0;
            int contador = 0;

            while (numero >= 0) {
                System.out.print("Introduce un número (negativo para salir): ");
                numero = scanner.nextInt();
                scanner.nextLine();

                if (numero >= 0) {
                    contador++;
                }
            }
            System.out.println("Has introducido " + contador + " números no negativos.");
        }
    }
    ```
5. Realizar un juego para adivinar un número. Para ello se asigna a una variable n un número entero aleatorio, y luego ir pidiendo números indicando “mayor” o “menor” según sea mayor o menor con respecto a N. El proceso termina cuando el usuario acierta y se imprime el texto “exacto!”. Para generar un número aleatorio se puede usar la utilidad java.util.Random

```java
Random r = new Random(); 
int secret = r.nextInt(100); // Genera un numero aleatorio del 0 al 10 
```

```java
package org.example.whilexercices;

import java.util.Random;
import java.util.Scanner;

public class Ej5 {
    public static void main(String[] args) {
        Random r = new Random();
        int secret = r.nextInt(100);

        Scanner scanner = new Scanner(System.in);
        System.out.println("Adivina un número del 0 al 99");
        int guess = -1;
        while (guess != secret) {
            System.out.println("Introduce un número");
            guess = scanner.nextInt();
            scanner.nextLine();

            if (guess > secret) {
                System.out.println("Es menor");
            } else if (guess < secret) {
                System.out.println("es mayor");
            } else {
                System.out.println("¡¡¡Acertaste!!!");
            }
        }
    }
}

```

6.  Escribe un programa que pregunte cuántos números se van a introducir (si mete un valor menor que 1, debe volver a pedirlo hasta que no sea mayor o igual que 1), pida esos números y calcule la media de los mismo. La media se calcula sumando todos los números y dividiendo la suma entre la cantidad de números\


    ```java
    package org.example.whilexercices;

    import java.util.Scanner;

    public class Ej6 {
        public static void main(String[] args) {
            var scanner = new Scanner(System.in);
            int amount = 0;
            while (amount < 1) {
                System.out.println("Introduce la cantidad de números (mayor que cero)");
                amount = scanner.nextInt();
                scanner.nextLine();
            }

            double sum = 0;
            int i = 0;
            while (i < amount) {
                System.out.println("Introduce un número");
                int num = scanner.nextInt();
                scanner.nextLine();
                sum = sum + num;
                i++;
            }

            double average = sum / amount;

            System.out.println("La media es " + average);
        }
    }
    ```
7.  Pedir números hasta que se teclee un 0, mostrar la suma de todos los números introducidos al finalizar.\


    ```java
    package org.example.whilexercices;

    import java.util.Scanner;

    public class Ej7 {
        public static void main(String[] args) {
            Scanner scanner = new Scanner(System.in);
            int suma = 0;
            int numero = -1;
            while (numero != 0) {
                System.out.print("Introduce un número (0 para terminar): ");
                numero = scanner.nextInt();
                scanner.nextLine();
                suma += numero;
            }
            System.out.println("Suma total: " + suma);
            scanner.close();
        }
    }

    ```
8.  Pedir 10 números. Mostrar la media de los números positivos, la media de los números negativos y la cantidad de ceros.\


    ```java
    ```
