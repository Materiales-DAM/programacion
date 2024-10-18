---
cover: ../../../.gitbook/assets/method.jpg
coverY: 0
---

# Soluciones cabeceras

Escribe las cabeceras de los siguientes métodos:

1.  Un método que calcule la suma de sus dos parámetros enteros y devuelva el resultado

    ```java
    public static int sum(int num1, int num2)
    ```
2. Un método que reciba un entero por parámetro e imprima el texto “El resultado es: ” y el parámetro recibido. Este método no devolverá nada\
   `public static void printResult(int result)`
3. Un método que calcule la multiplicación de sus dos parámetros enteros y devuelva el resultado\
   public static int multiply(int num1, int num2)
4.  Un método que calcule el máximo de cuatro enteros (se pasa por parámetro) y devuelva el máximo

    ```java
    public static int max(int n1, int n2, int n3, int n4) {
        int max = n1;
        if(n2 > max) {
            max = n2;
        }

        if(n3 > max) {
            max = n3;
        }

        if(n4 > max) {
            max = n4;
        }

        return max;
    }
    ```
5. Un método que reciba un entero por parámetro e imprima el texto “El máximo es: ” y el parámetro recibido. Este método no devolverá nada\
