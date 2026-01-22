---
cover: ../../.gitbook/assets/tree.png
coverY: 0
---

# Ejercicios List

Los siguientes ejercicios se pueden crear como métodos una sola clase llamada ListExercises

1. Escribe un programa que cree un Array List y lo rellene con varios String. Luego recórrelo mostrando en pantalla cada elemento.
2. Escribe un método addAtBeggining(List\<String> list, String value) que dada una lista de String (list) y un String (value) y lo inserte en la primera posición.
   * {“Hola”, “Mundo”} + “Adiós” = {“Adiós” , “Hola”, “Mundo”}
3. Escribe un método first(List\<Integer> list) que dada una lista de Integer y devuelva el que está en la primera posición. Si la lista está vacía devuelve null. Prueba el método con una lista vacía y con otra con tres valores dentro.
4. Escribe un método last(List\<Integer> list) que dada una lista de Integer y devuelva el que está en la última posición. Si la lista está vacía devuelve null. Prueba el método con una lista vacía y con otra con tres valores dentro.
5. Un método sum(List\<Double> numbers ) que calcula la suma de los números en la lista.
6. Un método average(List\<Double> numbers ) que calcula la media de los números en la lista. Si la lista está vacía devuelve null.
7. Un método max(List\<Double> numbers ) que busca el máximo de los números en la lista. Si la lista está vacía devuelve null.
8. Un método min(List\<Double> numbers ) que busca el mínimo de los números en la lista. Si la lista está vacía devuelve null.
9. Crea un método que pida una lista de enteros, cada vez que el usuario introduce un número se le pregunta si desea introducir más (respuesta sí o no), cuando dice que no se devuelve la lista con los números que se hayan introducido hasta ese momento.
10. Un método sum10(List\<Integer> numbers) que dado una lista de enteros, devuelve otra lista de enteros del mismo tamaño en la que se le ha sumado 10 a cada número de la primera lista.
11. Un método union(List\<Double> numbers1 , List\<Double> numbers2) que dadas dos listas de números, crea una nueva lista en la que añade los elementos de numbers1 y después los de numbers 2.
12. Un método junction(List\<Double> numbers1 , List\<Double> numbers2) que dadas dos listas de números, crea una nueva lista en la que añade aquellos números que estén tanto en numbers1 como en numbers2
13. Un método removeAll(List\<Double> numbers , List\<Double> numbersToRemove) que dadas dos listas de números, elimina de numbers todos los números que estén en numbersToRemove<br>

    ```java
    @Data
    @AllArgsConstructor
    public class Student {
        private String name;
        private String surname;
        private String email;
        private int zipCode;
    }
    ```
14. Un método List\<String> mapToEmails(List\<Student> students) que dada una lista de estudiantes, devuelva una lista de los emails de los estudiantes en el mismo orden
15. Un método List\<Student> filterByZipCode(List\<Student> students, int zipCode) que dada una lista de estudiantes y un código postal, devuelva una lista con los estudiantes que vivan en ese código postal
16. Un método que recibe una lista de números enteros (numbers) y devuelve otra lista con los números pares que había en numbers

Crea tu propia implementación de una lista enlazada:

* Crea una clase Node que tenga como campos un valor de tipo Double y un enlace al siguiente nodo
* Crea una clase MyList con un campo llamado head que apunte al primer nodo
* Añade métodos para:
  * get(int index): Devuelve el valor en la posición del índice
  * add(Double value): añade el valor al final de la lista
  * addFirst(Double value): añade el valor al principio de la lista
  * remove(int index): elmina el valor en la posición index
* Convierte MyList en genérica (también debe serlo Node)
