---
cover: ../../.gitbook/assets/control-structures.gif
coverY: 0
---

# Ejercicios avanzados de ampliación

1. Realiza un programa que solicite un número entero positivo (n) y calcule el MCM de todos los número de 1 a n:
   1. 5 -> 60
   2. 6 -> 60
   3. 7 -> 420
   4.  8 -> 840\


       ```java
       package org.ies.tierno;

       import java.util.Scanner;

       public class Mcm {
           public static void main(String[] args) {
               var scanner = new Scanner(System.in);
               int n;
               do {
                   System.out.println("Introduce un número mayor que 1");
                   n = scanner.nextInt();
                   scanner.nextLine();
               } while (n < 2);

               double mcm;
               if (n == 2) {
                   mcm = 2;
               } else if (n == 3) {
                   mcm = 6;
               } else {
                   mcm = 6 * n;
               }

               boolean found;
               do {
                   found = true;
                   for (int i = 1; i <= n; i++) {
                       if (mcm % i != 0) {
                           found = false;
                           break;
                       }
                   }
                   if (!found) {
                       mcm++;
                   }
               } while (!found);

               System.out.println(mcm);
           }
       }
       ```
2. Realiza un programa que solicite un número entero positivo (n) y compruebe si es palíndromo (es el mismo número si inviertes los números). Para comprobarlo debes invertir el número en un while utilizando las operaciones % y \*:
   1. 1001 -> es palíndromo
   2. 100010 -> no es palíndromo
   3. 110011 -> es palíndromo
3. Realiza un programa que solicite un número entero positivo (n), imprimer la representación de este número como suma de pontencias de 2 en orden descendente (2<sup>N</sup>...2<sup>3</sup>, 2<sup>2</sup>,2<sup>1</sup>,2<sup>0</sup>):
   1. 9 -> 8 + 1
   2. 25 -> 16 +8 + 1
