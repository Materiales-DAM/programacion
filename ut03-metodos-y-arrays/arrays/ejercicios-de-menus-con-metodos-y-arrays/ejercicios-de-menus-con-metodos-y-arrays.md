---
cover: ../../../.gitbook/assets/arrays.png
coverY: 0
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
    package menu_methods_arrays;

    import java.util.Scanner;

    public class Menu1 {
        private static Scanner scanner = new Scanner(System.in);

        public static void main(String[] args) {
            menu();
        }

        public static int askPositive() {
            int num;
            do {
                System.out.println("Introduce un entero positivo");
                num = scanner.nextInt();
                scanner.nextLine();
            } while (num <= 0);
            return num;
        }

        public static int[] askArray() {
            int positive = askPositive();
            int[] numbers = new int[positive];
            for (int i = 0; i < numbers.length; i++) {
                System.out.println("Introduce el valor " + i + " del array");
                numbers[i] = scanner.nextInt();
                scanner.nextLine();
            }
            return numbers;
        }

        public static int maximum(int[] numbers) {
            int max = Integer.MIN_VALUE;

            for (int i = 0; i < numbers.length; i++) {
                int number = numbers[i];
                if (number > max) {
                    max = number;
                }
            }
            return max;
        }

        public static int minimum(int[] numbers) {
            int min = numbers[0];
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
                sum = sum + number;
            }
            return sum / numbers.length;
        }

        public static int chooseOption() {
            System.out.println("Elige una opcion");
            System.out.println("1.Buscar el maximo en el arrays");
            System.out.println("2. Buscar el minimo en el arrays");
            System.out.println("3 Calcular la media del array");
            System.out.println("4. Salir");

            int option = scanner.nextInt();
            scanner.nextLine();
            return option;
        }

        public static void menu() {
            int option;
            do {
                option = chooseOption();
                if (option == 1) {
                    int[] numbers = askArray();
                    int max = maximum(numbers);
                    System.out.println("El maximo es " + max);
                } else if (option == 2) {
                    int[] numbers = askArray();
                    int min = minimum(numbers);
                    System.out.println("El minimo es minimo " + min);
                } else if (option == 3) {
                    int[] numbers = askArray();
                    double media = avg(numbers);
                    System.out.println("La media es " + media);
                } else if (option == 4) {
                    System.out.println("Saliendo...");
                } else {
                    System.out.println("Valor erroneo");
                }
            } while (option != 4);
        }
    } 
    ```

2. Crea un programa de menú interactivo que permita al usuario realizar las siguientes operaciones:
   1. Calcular la suma de una lista de números
   2. Duplicar array: pide un array de números al usuario e imprime esos números multiplicados por dos&#x20;
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
    package menu_methods_arrays;

    import java.util.Scanner;

    public class Menu2 {
        private static Scanner scanner = new Scanner(System.in);

        public static void main(String[] args) {
            menu();
        }

        public static int askPositive() {
            int number;
            do {
                System.out.println("Introduce un número positivo");
                number = scanner.nextInt();
                scanner.nextLine();
            } while (number <= 0);
            return number;
        }

        public static int[] createArray() {
            int size = askPositive();
            int[] numbers = new int[size];

            for (int i = 0; i < size; i++) {
                System.out.println("Introduce un número");
                int number = scanner.nextInt();
                scanner.nextLine();
                numbers[i] = number;
            }
            return numbers;
        }

        public static int sumArray(int[] numbers) {
            int sum = 0;
            for (int number : numbers) {
                sum += number;
            }
            return sum;
        }

        public static int[] multArray(int[] numbers) {
            int[] result = new int[numbers.length];
            for (int i = 0; i < numbers.length; i++) {
                result[i] = numbers[i] * 2;
            }
            return result;
        }

        public static int chooseOption() {
            System.out.println("Elige una opcion");
            System.out.println("1.Calcular suma");
            System.out.println("2. Duplicar array");
            System.out.println("3. Salir");

            int option = scanner.nextInt();
            scanner.nextLine();
            return option;
        }

        public static void menu() {
            int option;
            do {
                option = chooseOption();
                if (option == 1) {
                    int[] numbers = createArray();
                    int suma = sumArray(numbers);
                    System.out.println("La suma es " + suma);
                } else if (option == 2) {
                    int[] numbers = createArray();
                    int[] multiplicacion = multArray(numbers);
                    for (int i = 0; i < multiplicacion.length; i++) {
                        System.out.println("Resultado[" + i + "]=" + multiplicacion[i]);
                    }
                } else if (option == 3) {
                    System.out.println("Saliendo...");
                } else {
                    System.out.println("Valor erroneo");
                }
            } while (option != 3);
        }
    } 
    ```
