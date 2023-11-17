# Tarea Potencias

Crea un programa con los siguientes métodos:\
Un método que, dados dos enteros, calcula la potencia de esos números y la devuelve. Por ejemplo si recibe 2 y 3 debe devolver 2³ o sea 2 \* 2 \* 2

1. Un método que recibe un array de números y otro número, el método debe devolver otro array que contendrá el resultado de calcular la potencia de cada uno de los números del array de entrada con el otro parámetro. Por ejemplo: si recibe el array {2, 3, 4} y el número 2 debería devolver { 2², 3², 4²} = {4, 9, 16}
2. Un método que pida  un array de números y los devuelve
3. Un método que pide un número mayor que 1
4. Un método que imprimer un array en pantalla
5. El método principal implementará un menú interactivo. Opciones
6.
   1. Elevar array a potencia: pide un array, pide un número positivo, eleva el array a la potencia y lo imprime en pantalla
   2. Elevar número a potencia: pide un número entero (a), pide otro número entero positivo (n),  calcula an y muestra el resultado en pantalla
   3. Salir

```java
package practica2;

import java.util.Scanner;

public class Potencias {

    private static Scanner scanner = new Scanner(System.in);

    public static int potencia(int base, int exponente) {
        int res = 1;
        for (int i = 0; i < exponente; i++) {
            res = res * base;
        }
        return res;
    }

    public static int[] potenciaArray(int[] numbers, int exponente) {
        int[] result = new int[numbers.length];

        for (int i = 0; i < numbers.length; i++) {
            result[i] = potencia(numbers[i], exponente);
        }
        return result;
    }

    public static void printArray(int[] numbers) {
        System.out.println("Array(");

        for (int number : numbers) {
            System.out.println("    " + number);
        }
        System.out.println(")");
    }

    public static int pidePositivo(String message) {
        System.out.println(message);
        int number = scanner.nextInt();
        scanner.nextLine();

        while (number < 1) {
            System.out.println("Error, debe ser mayor que cero");
            number = scanner.nextInt();
            scanner.nextLine();
        }
        return number;
    }

    public static int[] pideArray() {
        int size = pidePositivo("Introduce el tamaño");
        int[] numbers = new int[size];

        for (int i = 0; i < numbers.length; i++) {
            System.out.println("Introduce un número");
            numbers[i] = scanner.nextInt();
            scanner.nextLine();
        }

        return numbers;
    }

    private static void runPotenciaArray() {
        int[] numbers = pideArray();
        int exponente = pidePositivo("Introduce el exponente");

        int[] resultado = potenciaArray(numbers, exponente);

        printArray(resultado);
    }

    private static void runPotencia() {
        System.out.println("Introduce la base");
        int base = scanner.nextInt();
        scanner.nextLine();

        int exponente = pidePositivo("Introduce el exponente");

        int resultado = potencia(base, exponente);
        System.out.println("El resultado es " + resultado);
    }

    public static void main(String[] args) {
        int option;

        do {
            System.out.println("Elija una opción:");
            System.out.println("1. Potencia de dos números");
            System.out.println("2. Potencia de un array");
            System.out.println("3. Salir");

            option = scanner.nextInt();
            scanner.nextLine();

            if (option == 1) {
                runPotencia();
            } else if (option == 2) {
                runPotenciaArray();
            } else if (option != 3) {
                System.out.println("Opción inválida");
            }

        } while (option != 3);
        System.out.println("Saliendo");
    }
}

```
