# Ejercicios while

1. Escriba un programa que pida dos números enteros. El programa pedirá de nuevo el segundo número hasta que sea mayor que el primero. El programa terminará escribiendo los dos números.&#x20;
2. Escriba un programa que pida dos números decimales. El programa pedirá de nuevo el segundo número hasta que sea menor que el primero. El programa terminará escribiendo los dos números.&#x20;
3. Escriba un programa que pida números mientras el usuario indique que quiere seguir introduciendo números. Para indicar que quiere seguir escribiendo números, el usuario deberá contestar S o s a la pregunta.&#x20;
   * `Introduce numero: 2`&#x20;
   * `¿Quieres seguir? S`&#x20;
   * `Introduce numero: 3`&#x20;
4. Pedir números hasta que se teclee uno negativo, y mostrar cuántos números se han introducido.&#x20;
5. Realizar un juego para adivinar un número. Para ello se asigna a una variable n un número entero aleatorio, y luego ir pidiendo números indicando “mayor” o “menor” según sea mayor o menor con respecto a N. El proceso termina cuando el usuario acierta y se imprime el texto “exacto!”. Para generar un número aleatorio se puede usar la utilidad java.util.Random&#x20;

```java
Random r = new Random(); 
int n = r.nextInt(100); // Genera un numero aleatorio del 0 al 10 
```

6. Escribe un programa que pregunte cuántos números se van a introducir (si mete un valor menor que 1, debe volver a pedirlo hasta que no sea menor que 1), pida esos números y calcule la media de los mismo. La media se calcula sumando todos los números y dividiendo la suma entre la cantidad de números&#x20;
7. Pedir números hasta que se teclee un 0, mostrar la suma de todos los números introducidos al finalizar.&#x20;
8. Pedir 10 números. Mostrar la media de los números positivos, la media de los números negativos y la cantidad de ceros.&#x20;
