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

# Soluciones de métodos y arrays

1. Crea un programa que defina los siguientes métodos:
   1. Un método que, dado un array de enteros, busque el máximo y lo devuelva.
   2. Un método que reciba un entero por parámetro e imprima el texto “El máximo es: ” y el parámetro recibido. Este método no devolverá nada

En el main se invocara el primer método pasando un array con los valores 1, 3, 5 y 0, después se invocará el segundo método con el resultado de la invocación del primero

```java
package methods_arrays;

public class Arrays1 {
    public static void main(String[] args) {
        int[] numbers = {1, 3, 5, 0};
        int max = max(numbers);
        printMax(max);
    }

    public static int max(int[] numbers) {
        int max = numbers[0];
        for (int number : numbers) {
            if (number > max) {
                max = number;
            }
        }

        return max;
    }

    public static void printMax(int number) {
        System.out.println("El máximo es " + number);
    }
}
```

2. Crea un programa que defina los siguientes métodos:
   1. Un método que calcule la suma de los valores de un array de enteros (se pasa por parámetro) y devuelva la suma
   2. Un método que reciba un entero por parámetro e imprima el texto “La suma es: ” y el parámetro recibido. Este método no devolverá nada

En el main se invocara el primer método pasando un array con los valores 1, 3, 5 y 0, después se invocará el segundo método con el resultado de la invocación del primero

```java
package methods_arrays;

public class Arrays2 {
    public static void main(String[] args) {
        int[] numbers = {1, 3, 5, 0};
        int sum = sum(numbers);
        printSum(sum);
    }

    public static int sum(int[] numbers) {
        int sum = 0;
        for (int number : numbers) {
            sum += number;
        }
        return sum;
    }

    public static void printSum(int number) {
        System.out.println("La suma es " + number);
    }
}
```

3. Crea un programa que defina los siguientes métodos:
   1. Un método que pida un al usuario un número entero positivo. Si el usuario introduce un negativo el programa volverá a pedir el número hasta que sea positivo.
   2. Un método que pida un array de números:
      1. Primero pide un entero positivo (tamaño) usando el método anterior
      2. Crea un array vacío del tamaño que ha pedido el usuario
      3. Rellena el array con un bucle for, en cada iteración se pide al usuario que introduzca un número y se guarda en la posición correspondiente
   3. Un método que, dado un array de enteros, calcule la media de todos los números que contiene y la devuelva
   4. Un método que reciba un double por parámetro e imprima el texto “La media es: ” y el parámetro recibido. Este método no devolverá nada

En el main se pide un array, se calcula la media y se imprime el resultado

```java
package methods_arrays;

import java.util.Scanner;

public class Arrays3 {
    private static Scanner scanner = new Scanner(System.in);

    public static void main(String[] args) {
        int[] numbers = createArray();
        double average = calculateAverage(numbers);
        printAverage(average);
    }


    public static int askPositve() {
        System.out.println("Introduce un número positivo");
        int number;

        do {
            System.out.println("Introduce un número positivo");
            number = scanner.nextInt();
            scanner.nextLine();
        } while (number <= 0);
        return number;
    }

    public static int[] createArray() {
        int size = askPositve();
        int[] array = new int[size];

        for (int i = 0; i < size; i++) {
            System.out.println("Introduce un número");
            int number = scanner.nextInt();
            scanner.nextLine();
            array[i] = number;
        }
        return array;
    }

    public static double calculateAverage(int[] numbers) {
        double add = 0;
        for (int number : numbers) {
            add += number;
        }

        return add / numbers.length;
    }

    public static void printAverage(double average) {
        System.out.println("La media es: " + average);
    }
}
```

4. Crea un programa con los siguientes métodos:
   1. Un método que pida un array de números y los devuelve
   2. Un método que reciba un array de números y devuelva el array en orden inverso
   3. Un método que recibe dos arrays de números y devuelve la unión de los mismos
   4. Un método que reciba un array de números y los imprima en pantalla
   5. El método main realizará las siguientes invocaciones:
      1. Pide un array
      2. Invierte el array
      3. Imprime el array invertido
      4. Pide otro array
      5. Invierte este nuevo array
      6. Imprime el otro array invertido
      7. Une los dos arrays invertidos
      8.  Imprime el resultado de la unión\


          ```java
          package methods_arrays;

          import java.util.Scanner;

          public class Arrays4 {
              private static Scanner scanner = new Scanner(System.in);

              public static void main(String[] args) {
                  int[] numbers1 = askArray();
                  int[] invertedNumbers1 = reverseArray(numbers1);
                  print(invertedNumbers1);
                  int[] numbers2 = askArray();
                  int[] invertedNumbers2 = reverseArray(numbers2);
                  print(invertedNumbers2);
                  int[] union = union(invertedNumbers1, invertedNumbers2);
                  print(union);

              }

              public static int numberArray() {
                  System.out.println("Introduzca el tamaño del array que desea ");
                  int number = scanner.nextInt();
                  scanner.nextLine();

                  while (number <= 0) {
                      System.out.println("Introduzca un numero mayor que cero");
                      number = scanner.nextInt();
                      scanner.nextLine();
                  }
                  return number;
              }

              public static int[] askArray() {
                  int positive = numberArray();
                  int[] numbers = new int[positive];
                  for (int i = 0; i < numbers.length; i++) {
                      System.out.println("Introduzca los numeros que quiere dentro del array ");
                      numbers[i] = scanner.nextInt();
                      scanner.nextLine();
                  }
                  return numbers;
              }

              public static int[] reverseArray(int[] numbers) {
                  int[] reverted = new int[numbers.length];
                  for (int i = 0; i < numbers.length; i++) {
                      int newI = numbers.length - i - 1;
                      reverted[newI] = numbers[i];
                  }
                  return reverted;
              }

              public static int[] union(int[] numbers1, int[] numbers2) {
                  int[] union = new int[numbers1.length + numbers2.length];
                  for (int i = 0; i < numbers1.length; i++) {
                      union[i] = numbers1[i];
                  }
                  for (int i = 0; i < numbers2.length; i++) {
                      int newI = numbers1.length + i;
                      union[newI] = numbers2[i];
                  }
                  return union;
              }

              public static void print(int[] numbers) {
                  for (int number : numbers) {
                      System.out.println(number);
                  }
              }
          }
          ```
