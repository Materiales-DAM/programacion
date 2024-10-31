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

# Soluciones arrays

1. Haz un programa que:
   1. Cree un array con los valores 4, 8, 9 y 1.
   2.  Recorre el array y muestra cada valor en pantalla\


       ```java
       package arrays;

       public class Arrays1 {
           public static void main(String[] args) {
               int[] numbers = {4, 8, 9, 1};

               for(int i = 0; i < numbers.length; i++) {
                   int number = numbers[i];
                   System.out.println("El valor en la posición " + i + " es " + number);
               }
           }
       }
       ```
2. Haz un programa que:
   1. Cree un array con los valores 3.4, 5.2, 4.7
   2.  Después imprime en pantalla el último valor del array

       ```java
       package arrays;

       public class Arrays2 {
           public static void main(String[] args) {
               double[] numbers = {3.4, 5.2, 4.7};
               System.out.println("En la posición 2 está el número " + numbers[numbers.length - 1]);
           }
       }
       ```
3. Haz un programa que:
   1. Cree un array con los valores 4, 8, 9 y 1.
   2. Recorre el array calculando la suma de todos los números
   3.  Al final imprime la suma\


       ```java
       package arrays;

       public class Arrays3 {
           public static void main(String [] args){
               
               int[] numbers = {4, 8, 9, 1};
               int add = 0;

               for (int number: numbers){
                   add += number;
               }

               System.out.println("La suma de estos números es: " + add);
           }
       } 
       ```
4. Haz un programa que:
   1. Pregunte al usuario cuántos nombres quiere meter
   2. Cree un array de Strings del tamaño que ha dicho el usuario
   3. Recorre el array, en cada iteración
      1. Pide un nombre al usuario con el scanner
      2. Guarda en la posición i del array el nombre que acaba de pasar el usuario
   4.  Vuelve a recorrer el array mostrando en pantalla todos los nombres almacenados en el mismo\


       ```java
       package arrays;

       import java.util.Scanner;

       public class Arrays4 {
           public static void main(String[] args) {
               Scanner scanner = new Scanner(System.in);

               System.out.println("¿Cuantos nombres va a meter?");
               int n = scanner.nextInt();
               scanner.nextLine();

               String[] names = new String[n];

               for (int i = 0; i < names.length; i++) {
                   System.out.println("Introduce un nombre");
                   String name = scanner.nextLine();
                   names[i] = name;
               }

               for (String name : names) {
                   System.out.println(name);
               }
           }
       }
       ```
