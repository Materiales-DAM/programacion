# Soluciones matrices

1. Escribe un programa que:
   1. Un método que dado una matriz bidimensional de enteros, devuelva la suma de todos los números que contiene
   2. En el main crea una matriz con los siguientes números y calcula la suma:
      1. 2, 3, 4
      2. 2, 3
      3.  5,2,2<br>

          ```java
          package org.ies.tierno.matrices;

          public class Ej1 {

              public static void main(String[] args) {
                  int[][] numbers = {
                          {1, 2, 3},
                          {2, 3},
                          {5, 2, 2}
                  };
                  
                  int sum = 0;
                  for (int[] row: numbers) {
                      for (int number: row) {
                          sum += number;
                      }
                  }
                  System.out.println(sum);
              }
          }
          ```
2. Escribe un programa que pida al usuario un número entero positivo (n), después crea una matriz de dimensiones nxn y la rellena con números consecutivos. Por ejemplo, una matriz de 3x3 sería:\
   0 1 2\
   3 4 5\
   6 7 8<br>
3. Implementa un método que dada una matriz de enteros, devuelva otra matriz con las mismas dimensiones en la que los valores estén multiplicados por 2<br>
