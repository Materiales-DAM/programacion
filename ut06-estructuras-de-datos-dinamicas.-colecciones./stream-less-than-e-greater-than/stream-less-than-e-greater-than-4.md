---
cover: ../../.gitbook/assets/lambda.jpeg
coverY: 0
layout:
  cover:
    visible: true
    size: hero
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

# Ejercicios Stream\<E>

Resuelve estos ejercicios usando Stream

1. Escribe un programa que cree un ArrayList y lo rellene con varios String. Luego conviértelo en un Stream y recórrelo mostrando en pantalla cada elemento.
2. Escribe un método first(List\<String> list) que dada una lista de String y devuelva el que está en la primera posición. Como la lista puede estar vacía, el método debe devolver Optional\<String>.
3. Escribe un método last(List\<Integer> list) que dada una lista de Integer y devuelva el que está en la última posición. Como la lista puede estar vacía, el método debe devolver Optional\<Integer>. Prueba el método con una lista vacía y con otra con tres valores dentro.
4. Un método sum10(List\<Integer> numbers) que dado una lista de enteros, devuelve otra lista de enteros del mismo tamaño en la que se le ha sumado 10 a cada número de la primera lista.
5. Un método List\<String> mapToEmails(List\<Student> students) que dada una lista de estudiantes, devuelva una lista de los emails de los estudiantes en el mismo orden
6. Un método List\<Student> filterByZipCode(List\<Student> students, int zipCode) que dada una lista de estudiantes y un código postal, devuelva una lista con los estudiantes que vivan en ese código postal
7. Un método que recibe una lista de números enteros (numbers) y devuelve otra lista con los números pares que había en numbers
8. Un método sum(List\<Double> numbers ) que calcula la suma de los números en la lista, si la lista está vacía devuelve 0.
9. Un método average(List\<Double> numbers ) que calcula la media de los números en la lista. Como la lista puede estar vacía, el método debe devolver Optional\<Double>.
10. Un método max(List\<Double> numbers ) que busca el máximo de los números en la lista. Como la lista puede estar vacía, el método debe devolver Optional\<Double>.
11. Un método min(List\<Double> numbers ) que busca el mínimo de los números en la lista. Como la lista puede estar vacía, el método debe devolver Optional\<Double>.
12. Un método junction(List\<Double> numbers1 , List\<Double> numbers2) que dadas dos listas de números, devuelve los números que están tanto numbers1 como en numbers2
13. Un método que dado una lista de pedidos, devuelve una lista con los precios de cada pedido
14. Un método que dado una lista de pedidos, devuelve el precio total de todos los pedidos
15. Un método que dado una lista de pedidos, devuelva una lista con todos los OrderItem
