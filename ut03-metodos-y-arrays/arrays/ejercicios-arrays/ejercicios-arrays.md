---
cover: ../../../.gitbook/assets/arrays.png
coverY: 0
---

# Soluciones arrays

1. Haz un programa que:
   1. Cree un array con los valores 4, 8, 9 y 1.
   2.  Recorre el array y muestra cada valor en pantalla<br>

       ```java
       package org.ies.tierno.arrays;

       public class Ej1 {
           public static void main(String[] args) {
               int[] numbers = {4, 8, 9, 1};

               for (int i = 0; i < numbers.length; i++) {
                   int number = numbers[i];
                   System.out.println(number);
               }

               for (int number : numbers) {
                   System.out.println(number);
               }
           }
       } 
       ```
2. Haz un programa que:
   1. Cree un array con los valores 3.4, 5.2, 4.7
   2.  Después imprime en pantalla el último valor del array

       ```java
       package org.ies.tierno.arrays;

       public class Ej2 {
           public static void main(String[] args) {
               double[] nums = new double[4];
               nums[0] = 3.4;
               nums[1] = 5.2;
               nums[2] = 4.7;
               
               int lastI = nums.length - 1;
               System.out.println(nums[lastI]);
           }
       }

       ```
3. Haz un programa que:
   1. Cree un array con los valores 4, 8, 9 y 1.
   2. Recorre el array calculando la suma de todos los números
   3.  Al final imprime la suma<br>

       ```java
       package org.ies.tierno.arrays;

       public class Ej3 {
           public static void main(String[] args) {
               int[] numbers = {4, 8, 9, 1};
               int sum = 0;
               for (int number : numbers) {
                   // sum = sum + number;
                   sum += number;
               }
               System.out.println(sum);
           }
       } 

       ```
4. Haz un programa que:
   1. Pregunte al usuario cuántos nombres quiere meter
   2. Cree un array de Strings del tamaño que ha dicho el usuario
   3. Recorre el array, en cada iteración
      1. Pide un nombre al usuario con el scanner
      2. Guarda en la posición i del array el nombre que acaba de pasar el usuario
   4.  Vuelve a recorrer el array mostrando en pantalla todos los nombres almacenados en el mismo<br>

       ```java
       package org.ies.tierno.arrays;

       import java.util.Scanner;

       public class Ej4 {
           public static void main(String[] args) {
               Scanner scanner = new Scanner(System.in);
               int length;
               do {
                   System.out.println("¿Cuántos nombres vas a introducir?");
                   length = scanner.nextInt();
                   scanner.nextLine();
                   if (length < 1) {
                       System.out.println("Debe ser mayor que cero");
                   }
               } while (length < 1);


               String[] names = new String[length];
               for (int i = 0; i < names.length; i++) {
                   System.out.println("Introduce un nombre: ");
                   String name = scanner.nextLine();
                   names[i] = name;
               }

               System.out.println("Nombres:");
               for (String name: names) {
                   System.out.println(name);
               }
           }
       }

       ```
