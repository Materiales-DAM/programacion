---
cover: ../../../.gitbook/assets/control-structures.gif
coverY: 0
---

# Soluciones for

1\. Crea un programa que en el main:

```java
package org.example;

import java.util.Scanner;

public class ejercicio3 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Introduce un String de 8 caracteres: ");
        String texto = scanner.nextLine();
        switch (texto.length()){
            case 8: 
                System.out.println("Es válido"); 
                break;
            default:
                System.out.println("No es válido");  
        }
    
    }
} 
```

2\. Escribir un programa que pida dos números enteros e imprima todos los números que hay entre el más pequeño y el más grande:

```java
package org.ies.tierno;

import java.util.Scanner;

public class For2 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("Introduce un número:");
        int n1 = scanner.nextInt();
        scanner.nextLine();

        System.out.println("Introduce otro número:");
        int n2 = scanner.nextInt();
        scanner.nextLine();
        // Si el valor de n1 es mayor que el de n2, los voy a intercambiar de variable
        if (n1 > n2) {
            // Intercambio los valores entre n1 y n2
            // Necesito la variable aux para guardar el valor original de n1
            int aux = n1;
            // Ahora n1 toma el valor de n2
            n1 = n2;
            // Ahora n2 toma el valor original de n1
            n2 = aux;
        }

        for (int i = n1; i <= n2; i++) {
            System.out.println(i);
        }
    }
}

```

3\. Escribir un programa que pida un entero positivo y calcule el sumatorio de cero a ese número

```java
package org.ies.tierno;
import java.util.Scanner;

public class For3 {
    public static void main(String[]args){
        Scanner scanner = new Scanner(System.in);

        System.out.println("Ingresa un numero: ");
        int number = scanner.nextInt();
        scanner.nextLine();
        int suma = 0;

        for (int i = 0; i <= number;i++){
            // suma += i;
            suma = suma + i;
        }
        System.out.println(suma);
    }
} 
```

4\. Escribir un programa que pida un entero positivo y calcule el factorial de uno a ese número

```java
package org.ies.tierno;

import java.util.Scanner;

public class EjFor4 {
    public static void main(String[] args) {Scanner scanner = new Scanner(System.in);
        System.out.println("Introduce un número entero");
        int num = scanner.nextInt();
        scanner.nextLine();

        if (num <= 0){
            System.out.println("Introduce un número válido");
        } else {
            // factorial empieza por 1 porque si no siempre da 0
            int factorial = 1;

            // i empieza por 1 porque si no siempre da 0
            for (int i = 1; i <= num; i+º) {
                // factorial = factorial * i;
                factorial *= i;

            }
            System.out.println(factorial);
        }
    }
} 
```

5\. Escribir un programa que permita al usuario ingresar dos años y luego imprima todos los años en ese rango, que sean bisiestos.

```java
package buclefor;

import java.util.Scanner;

public class ejercicio2 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Ingresa el primer año: ");
        int year1 = sc.nextInt();
        sc.nextLine();

        System.out.print("Ingresa el segundo año: ");
        int year2 = sc.nextInt();
        sc.nextLine();

        System.out.println("Años bisiestos:");

        if (year1 > year2) {
            int aux = year1;
            year1 = year2;
            year2 = aux; 
        }

        for (int year = year1; year <= year2; year++) {
            if (year % 4 == 0 && year % 100 != 0) {
                System.out.println(year);
            }
        }

    }
} 
```

6\. Escribe un programa que pregunte cuántos números se van a introducir, pida esos números y escriba cuántos negativos se han introducido.

```java
```

7\. Escribe un programa que pregunte cuántos números se van a introducir, pida esos números e imprima el máximo de entre los números introducidos

```java
```

8\. Escribe un programa que pregunte cuántos números se van a introducir, pida esos números y calcule la media de los mismo. La media se calcula sumando todos los números y dividiendo la suma entre la cantidad de números

```java
```

9\. Escribe un programa que solicite un número entero mayor que 1 y compruebe si este es primo o no. Un número primo solo es divisible por sí mismo y por el 1

```
5: 5 % 2 == 0, 5 % 3 == 0, 5 % 3 == 0, 5 % 4 == 0 TODO FALSE: es primo 
6: 6 % 2 == 0 TRUE -> NO ES PRIMO
```

```java
```
