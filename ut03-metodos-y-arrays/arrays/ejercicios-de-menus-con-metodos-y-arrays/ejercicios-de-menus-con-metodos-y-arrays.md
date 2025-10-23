---
cover: ../../../.gitbook/assets/arrays.png
coverY: 0
---

# Soluciones de menús con métodos y arrays

1. Crea un programa de menú interactivo que permita al usuario realizar las siguientes operaciones:
   1. Buscar el máximo de entre una lista de números
   2. Buscar el mínimo de entre una lista de números
   3. Calcular la media de una lista de números
   4. Salir

Métodos necesarios:

* Un método para pedir un entero positivo
* Un método para pedir un array de números
* Un método que, dado un array de números, devuelve el máximo
* Un método que, dado un array de números, devuelve el mínimo
* Un método que, dado un array de números, devuelve la media
* Un método para pedir la opción que quiere hacer el usuario
* Un método por cada opción del menú
*   Un método con el bucle del menú\


    ```java
    package org.ies.tierno.menuarrays;

    import java.util.Scanner;

    public class Ej1 {
        public static Scanner scanner = new Scanner(System.in);

        public static void main(String[] args) {
            menu();
        }

        public static void menu() {
            int option;
            do {
                option = chooseOption();
                if (option == 1) {
                    runOpt1();
                } else if (option == 2) {
                    runOpt2();
                } else if (option == 3) {
                    runOpt3();
                }
            } while (option != 4);
        }

        private static int chooseOption() {
            int option;
            System.out.println("Elige una opción: ");
            System.out.println("1. Maximo");
            System.out.println("2. Mínimo");
            System.out.println("3. Media");
            System.out.println("4. Salir");
            option = scanner.nextInt();
            scanner.nextLine();
            return option;
        }

        public static void runOpt1() {
            int[] numbers = askNumbersArrays();
            int max = max(numbers);
            System.out.println("El max es: " + max);
        }

        public static void runOpt2() {
            int[] numbers = askNumbersArrays();
            int min = min(numbers);
            System.out.println("El min es: " + min);
        }

        public static void runOpt3() {
            int[] numbers = askNumbersArrays();
            double media = media(numbers);
            System.out.println("La media es: " + media);
        }

        public static int askSize() {
            System.out.println("Introduzca el tamaño del array: ");
            int size = scanner.nextInt();
            scanner.nextLine();
            while (size < 0) {
                System.out.println("El array debe ser positivo.");
                size = scanner.nextInt();
                scanner.nextLine();
            }
            return size;
        }

        public static int[] askNumbersArrays() {
            int size = askSize();
            int[] numbers = new int[size];
            for (int i = 0; i < numbers.length; i++) {
                System.out.println("Introduce el " + (i + 1) + "número");
                numbers[i] = scanner.nextInt();
                scanner.nextLine();

            }
            return numbers;
        }

        public static int max(int[] numbers) {
            int max = numbers[0];
            for (int i = 0; i < numbers.length; i++) {
                if (numbers[i] > max) {
                    max = numbers[i];
                }
            }
            return max;
        }

        public static int min(int[] numbers) {
            int min = numbers[0];
            for (int i = 0; i < numbers.length; i++) {
                if (numbers[i] < min) {
                    min = numbers[i];
                }
            }
            return min;
        }

        public static double media(int[] numbers) {
            double suma = 0;
            for (int number : numbers) {
                suma += number;
            }
            return suma / numbers.length;
        }
    }

    ```

2. Crea un programa de menú interactivo que permita al usuario realizar las siguientes operaciones:
   1. Calcular la suma de una lista de números
   2. Duplicar array: Duplicar array: pide un array de números al usuario, crea otro array con los números multiplicados por dos e imprime el array resultante
   3. Salir

Métodos necesarios:

* Un método para pedir un entero positivo
* Un método para pedir un array de números
* Un método que, dado un array de números, devuelve la suma
* Un método que, dado un array de números, devuelve otro array de números con los valores multiplicados por 2. Por ejemplo, para el array \[3 , 5] devolvería \[6, 10]
* Un método para pedir la opción que quiere hacer el usuario
* Un método por cada opción del menú
*   Un método con el bucle del menú\


    ```java
    ```
