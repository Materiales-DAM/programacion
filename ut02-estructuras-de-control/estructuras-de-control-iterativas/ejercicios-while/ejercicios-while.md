---
cover: ../../../.gitbook/assets/control-structures.gif
coverY: 0
---

# Soluciones while

1.  Escriba un programa que pida dos números enteros. El programa pedirá de nuevo el segundo número hasta que sea mayor que el primero. El programa terminará escribiendo los dos números.\


    ```java
    package whileexercises;

    import java.util.Scanner;

    public class While1 {
        public static void main(String[] args) {
            Scanner scanner = new Scanner(System.in);

            System.out.println("Introduce un número");
            int num1 = scanner.nextInt();
            scanner.nextLine();

            System.out.println("Introduce un número mayor que " + num1);
            int num2 = scanner.nextInt();
            scanner.nextLine();
            while (num2 <= num1) {
                System.out.println("El número introducido no es mayor que " + num1);
                num2 = scanner.nextInt();
                scanner.nextLine();
            }

            System.out.println("Num1: " + num1 + ". Num2: " + num2);
        }
    }
    ```
2.  Escriba un programa que pida dos números decimales. El programa pedirá de nuevo el segundo número hasta que sea menor que el primero. El programa terminará escribiendo los dos números.\


    ```java
    package whileexercises;

    import java.util.Scanner;

    public class While2 {
        public static void main(String[] args) {
            Scanner scanner = new Scanner(
                    System.in
            );

            System.out.println("Introduce un número decimal: ");
            double number1 = scanner.nextDouble();
            scanner.nextLine();

            System.out.println("Introduce el segundo número decimal: ");
            double number2 = scanner.nextDouble();
            scanner.nextLine();


            while (number1 <= number2){
                System.out.println("Introduce un número más pequeño: ");
                number2 = scanner.nextDouble();
                scanner.nextLine();
            }
            System.out.println(number1 + " Es más grande que "+ number2);

        }
    }
    ```
3. Escriba un programa que pida números mientras el usuario indique que quiere seguir introduciendo números. Para indicar que quiere seguir escribiendo números, el usuario deberá contestar S o s a la pregunta.
   * `Introduce numero: 2`
   * `¿Quieres seguir? S`
   *   `Introduce numero: 3`

       ```java
       package whileexercises;
       import java.util.Scanner;

       public class While3 {
           public static void main(String[] args) {
               Scanner scanner = new Scanner(
                       System.in
               );

               String sentence = "s";

               while (sentence.equalsIgnoreCase("s")) {
                   System.out.println("Introdzca otro numero ");
                   int num = scanner.nextInt();
                   scanner.nextLine();
                   System.out.println("¿ Quiere intorducir otro numero ? ");
                   sentence = scanner.nextLine();
               }
           }
       }
       ```
4.  Pedir números hasta que se teclee uno negativo, y mostrar cuántos números se han introducido.\


    ```java
    package whileexercises;

    import java.util.Scanner;

    public class While4 {
        public static void main(String[] args) {
            Scanner scanner = new Scanner(System.in);

            int num = 0;
            int cont = 0;

            while (num >= 0) {
                System.out.println("Introduce un número: ");
                num = scanner.nextInt();
                scanner.nextLine();
                if (num >= 0) {
                    cont++;
                }
            }
            System.out.println("Ha introducido " + cont + " números positivos");
        }
    }
    ```
5. Realizar un juego para adivinar un número. Para ello se asigna a una variable n un número entero aleatorio, y luego ir pidiendo números indicando “mayor” o “menor” según sea mayor o menor con respecto a N. El proceso termina cuando el usuario acierta y se imprime el texto “exacto!”. Para generar un número aleatorio se puede usar la utilidad java.util.Random

```java
Random r = new Random(); 
int secret = r.nextInt(100); // Genera un numero aleatorio del 0 al 10 
```

6. Escribe un programa que pregunte cuántos números se van a introducir (si mete un valor menor que 1, debe volver a pedirlo hasta que no sea menor que 1), pida esos números y calcule la media de los mismo. La media se calcula sumando todos los números y dividiendo la suma entre la cantidad de números
7. Pedir números hasta que se teclee un 0, mostrar la suma de todos los números introducidos al finalizar.
8. Pedir 10 números. Mostrar la media de los números positivos, la media de los números negativos y la cantidad de ceros.
