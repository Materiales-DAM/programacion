---
cover: ../../../.gitbook/assets/arrays.png
coverY: 0
layout:
  width: default
  cover:
    visible: true
    size: full
    mask: none
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
  metadata:
    visible: true
  tags:
    visible: true
  actions:
    visible: true
  anchors:
    visible: true
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
*   Un método con el bucle del menú<br>

    ```java
    package org.ies.tierno;

    import java.util.Scanner;

    public class Menu1 {
        private static Scanner scanner = new Scanner(System.in);

        public static void main(String[] args) {
            menu();
        }

        public static int askSize() {
            int size;
            do {
                System.out.println("Introduce el tamaño del array");
                size = scanner.nextInt();
                scanner.nextLine();
                if (size < 1) {
                    System.out.println("El array debe ser de un tamaño mayor que 0");
                }
            } while (size < 1);
            return size;
        }

        public static int[] askNumbers() {
            int[] numbers = new int[askSize()];

            for (int i = 0; i < numbers.length; i++) {
                System.out.print("Introduce un número: ");
                numbers[i] = scanner.nextInt();
                scanner.nextLine();
            }
            return numbers;
        }

        public static int max(int[] numbers) {
            int max = Integer.MIN_VALUE;
            for (int number : numbers) {
                if (number > max) {
                    max = number;
                }
            }
            return max;
        }

        public static int min(int[] numbers) {
            int min = Integer.MAX_VALUE;
            for (int number : numbers) {
                if (number < min) {
                    min = number;
                }
            }
            return min;
        }

        public static double avg(int[] numbers) {
            double sum = 0;
            for (int number : numbers) {
                sum += number;
            }

            return sum / numbers.length;
        }

        public static int chooseOption() {
            System.out.println("Elige una opción:");
            System.out.println("1. Máximo");
            System.out.println("2. Mínimo");
            System.out.println("3. Media");
            System.out.println("4. Salir");
            int opt = scanner.nextInt();
            scanner.nextLine();
            return opt;
        }

        public static void runMax() {
            int[] numbers = askNumbers();
            int max = max(numbers);
            System.out.println("El máximo es: " + max);
        }

        public static void runMin() {
            int[] numbers = askNumbers();
            int min = min(numbers);
            System.out.println("El mínimo es: " + min);
        }

        public static void runAvg() {
            int[] numbers = askNumbers();
            double avg = avg(numbers);
            System.out.println("La media es: " + avg);
        }

        public static void menu() {
            int option;
            do {
                option = chooseOption();
                if(option == 1) {
                    runMax();
                } else if(option == 2) {
                    runMin();
                } else if(option == 3) {
                    runAvg();
                } else if(option == 4) {
                    System.out.println("Saliendo...");
                } else {
                    System.out.println("Opción inválida");
                }
            }while (option != 4);
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
*   Un método con el bucle del menú<br>

    ```java
    package org.ies.tierno;

    import java.util.Arrays;
    import java.util.Scanner;

    public class Menu2 {
        private static Scanner scanner = new Scanner(System.in);

        public static void main(String[] args) {
            int option;
            do {
                option = chooseOption();

                if (option == 1) {
                    runSum();
                } else if (option == 2) {
                    runMultArray();
                } else if (option == 3) {
                    System.out.println("Saliendo...");
                } else {
                    System.out.println("Opción inválida");
                }
            } while (option != 3);
        }

        public static void runSum() {
            int[] numbers = askNumbers();
            int sum = sum(numbers);
            System.out.println("La suma es " + sum);
        }

        public static void runMultArray() {
            int[] numbers = askNumbers();
            int[] res = multArray(numbers);
            // Esto muestra un código raro System.out.println(res);
            // Esto muestra los elementos dentro del array
            System.out.println(Arrays.toString(res));
        }

        public static int chooseOption() {
            System.out.println("Elige una opción:");
            System.out.println("1. Suma de array");
            System.out.println("2. Multiplicar array");
            System.out.println("3. Salir");
            int opt = scanner.nextInt();
            scanner.nextLine();
            return opt;
        }

        public static int[] multArray(int[] numbers) {
            int[] result = new int[numbers.length];
            for (int i = 0; i < numbers.length; i++) {
                int number = numbers[i];
                result[i] = number * 2;
            }
            return result;
        }

        public static int sum(int[] numbers) {
            int sum = 0;
            for (int number : numbers) {
                sum += number;
            }
            return sum;
        }

        public static int askSize() {
            int size;
            do {
                System.out.println("Introduce el tamaño del array");
                size = scanner.nextInt();
                scanner.nextLine();
                if (size < 1) {
                    System.out.println("El array debe ser de un tamaño mayor que 0");
                }
            } while (size < 1);
            return size;
        }

        public static int[] askNumbers() {
            int[] numbers = new int[askSize()];

            for (int i = 0; i < numbers.length; i++) {
                System.out.print("Introduce un número: ");
                numbers[i] = scanner.nextInt();
                scanner.nextLine();
            }
            return numbers;
        }
    }

    ```
