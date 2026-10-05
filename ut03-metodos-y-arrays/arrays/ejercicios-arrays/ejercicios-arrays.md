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

# Soluciones arrays

1. Haz un programa que:
   1. Cree un array con los valores 4, 8, 9 y 1.
   2.  Recorre el array y muestra cada valor en pantalla<br>

       ```java
       package org.ies.tierno;

       public class Ej1 {
           public static void main(String[] args) {
               int[] numbers = {4, 8, 9, 1};

               for (int i = 0; i < numbers.length; i++) {
                   int number = numbers[i];
                   System.out.println(number);
               }
           }
       }

       ```
2. Haz un programa que:
   1. Cree un array con los valores 3.4, 5.2, 4.7
   2.  Después imprime en pantalla el último valor del array

       ```java
       package org.ies.tierno;

       public class Ej2 {
           public static void main(String[] args) {
               double[] numbers = {3.4, 5.2, 4.7};

               double lastNumber = numbers[numbers.length - 1];
               System.out.println(lastNumber);
           }
       }

       ```
3. Haz un programa que:
   1. Cree un array con los valores 4, 8, 9 y 1.
   2. Recorre el array calculando la suma de todos los números
   3.  Al final imprime la suma<br>

       ```java
       package org.ies.tierno;

       public class Ejercicio3 {
           public static void main(String[] args) {
               int[] numbers = {4, 8, 9, 1};

               int sum = 0;
               for (int number: numbers) {
                   sum = sum + number;
               }
               System.out.println(sum);
           }
       } 
       ```
4.  Haz un programa que:

    1. Pregunte al usuario cuántos nombres quiere meter
    2. Cree un array de Strings del tamaño que ha dicho el usuario
    3. Recorre el array, en cada iteración
       1. Pide un nombre al usuario con el scanner
       2. Guarda en la posición i del array el nombre que acaba de pasar el usuario
    4. Vuelve a recorrer el array mostrando en pantalla todos los nombres almacenados en el mismo<br>

    ```java
    package org.ies.tierno;

    import java.util.Scanner;

    public class Ej4Array {
        public static void main(String[] args) {
            Scanner sc = new Scanner(
    System.in
    );

            System.out.println("¿Cuántos nombres quieres introducir?: ");
            int num = sc.nextInt();
            sc.nextLine();
            String[] names = new String[num];
            for (int i = 0; i < names.length; i++) {
                System.out.println("Introduce el nombre: ");
                names[i] = sc.nextLine();
            }
            int sum=0;
            for(String name: names){
                System.out.println(name);;
            }
        }
    } 
    ```
