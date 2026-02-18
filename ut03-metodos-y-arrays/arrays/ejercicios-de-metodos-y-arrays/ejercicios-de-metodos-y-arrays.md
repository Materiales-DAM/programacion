---
cover: ../../../.gitbook/assets/arrays.png
coverY: 0
---

# Soluciones de métodos y arrays

1. Crea un programa que defina los siguientes métodos:
   1. Un método que, dado un array de enteros, busque el máximo y lo devuelva.
   2. Un método que reciba un entero por parámetro e imprima el texto “El máximo es: ” y el parámetro recibido. Este método no devolverá nada

En el main se invocara el primer método pasando un array con los valores 1, 3, 5 y 0, después se invocará el segundo método con el resultado de la invocación del primero

```java
package org.ies.tierno.mehtodsarrays;

public class Ej1 {
    public static int max(int[] numbers) {
        int max = numbers[0];
        for (int number : numbers) {
            if (number > max) {
                max = number;
            }
        }
        return max;
    }

    public static void printMax(int max) {
        System.out.println("El máximo es " + max);
    }

    public static void main(String[] args) {
        int[] numbers = {1, 3, 5, 0};
        int max = max(numbers);
        printMax(max);
    }
}

```

2. Crea un programa que defina los siguientes métodos:
   1. Un método que calcule la suma de los valores de un array de enteros (se pasa por parámetro) y devuelva la suma
   2. Un método que reciba un entero por parámetro e imprima el texto “La suma es: ” y el parámetro recibido. Este método no devolverá nada

En el main se invocara el primer método pasando un array con los valores 1, 3, 5 y 0, después se invocará el segundo método con el resultado de la invocación del primero

```java
package org.ies.tierno.mehtodsarrays;

public class Ej2 {
    public static void main(String[] args) {
        int[] numbers = {1, 2, 3, 4};
        int sum = sum(numbers);
        print(sum);
    }

    public static int sum(int[] numbers) {
        int sum = 0;
        for (int number : numbers) {
            sum += number;
        }
        return sum;
    }

    public static void print(int sum) {
        System.out.println("La suma es: " + sum);
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
package org.ies.tierno.mehtodsarrays;

import java.util.Scanner;

public class Ej3 {
    public static Scanner scanner = new Scanner(System.in);

    public static void main(String[] args) {
        int[] numbers = askNumbers();
        double average = average(numbers);
        messageAverage(average);
    }

    public static int askSize() {
        System.out.println("Por favor introduce el tamaño del array");
        int size = scanner.nextInt();
        scanner.nextLine();
        while (size < 0) {
            System.out.println("El numero ha de ser POSTIVO");
            size = scanner.nextInt();
            scanner.nextLine();
        }
        return size;
    }

    public static int[] askNumbers() {
        int size = askSize();
        int[] numbers = new int[size];
        for (int i = 0; i < numbers.length; i++) {
            System.out.println("Introduce el " + (i + 1) + "º numero");
            numbers[i] = scanner.nextInt();
            scanner.nextLine();
        }
        return numbers;
    }

    public static double average(int[] numbers) {
        double sum = 0;
        for (int number : numbers) {
            sum = sum + number;
        }
        return sum / numbers.length;
    }

    public static void messageAverage(double average) {
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
      8.  Imprime el resultado de la unión<br>

          ```java
          package org.ies.tierno.mehtodsarrays;

          import java.util.Scanner;

          public class Ej4 {
              private final static Scanner scanner = new Scanner(System.in);

              public static void main(String[] args) {
                  int[] numbers1 = askNumbers();
                  int[] numbers1Reverse = reverse(numbers1);
                  print(numbers1Reverse);

                  int[] numbers2 = askNumbers();
                  int[] numbers2Reverse = reverse(numbers2);
                  print(numbers2Reverse);

                  int[] union = union(numbers1Reverse, numbers2Reverse);
                  print(union);
              }

              private static int askSize() {
                  int size;
                  do {
                      System.out.println("Introduce el tamaño del array");
                      size = scanner.nextInt();
                      scanner.nextLine();
                      if (size < 1) {
                          System.out.println("El tamaño debe ser mayor que cero");
                      }
                  } while (size < 1);
                  return size;
              }

              private static int[] askNumbers() {
                  int size = askSize();
                  int[] numbers = new int[size];
                  for (int i = 0; i < numbers.length; i++) {
                      System.out.println("Introduce un número:");
                      numbers[i] = scanner.nextInt();
                      scanner.nextLine();
                  }
                  return numbers;
              }

              private static int[] reverse(int[] numbers) {
                  int[] reversed = new int[numbers.length];
                  for (int i = 0; i < numbers.length; i++) {
                      // j = len - 1 -i
                      int j = numbers.length - 1 - i;
                      reversed[j] = numbers[i];
                  }
                  return reversed;
              }

              public static int[] union(int[] numbers1, int[] numbers2) {
                  int[] union = new int[numbers1.length + numbers2.length];
                  for (int i = 0; i < numbers1.length; i++) {
                      union[i] = numbers1[i];
                  }
                  for (int i = 0; i < numbers2.length; i++) {
                      union[i + numbers1.length] = numbers2[i];
                  }
                  return union;
              }

              private static void print(int[] numbers) {
                  for (var number: numbers) {
                      System.out.print(number + " ");
                  }
                  System.out.println();
              }
          }

          ```
