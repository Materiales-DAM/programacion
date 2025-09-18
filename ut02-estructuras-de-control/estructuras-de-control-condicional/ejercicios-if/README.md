---
cover: ../../../.gitbook/assets/control-structures.gif
coverY: 0
---

# Ejercicios If

1\. Escribe un programa Compare que:

* Pida dos números enteros
* Si el primero es mayor que el segundo imprime en pantalla “Es mayor”
* Si es menor imprime “es menor”
* Si son iguales imprime “son iguales”

2\. Escribe un programa IsEven que:

* Pide un número entero
* Imprime en pantalla “Es par” cuando el número es par (n % 2 == 0)
* Si n % 2 == 1 es impar
* Si es 0 imprime “No es ni par ni impar”

3\. Escribe un programa ShowSign que:

* Pide un número entero
* Imprime en pantalla “Es negativo” cuando el número es menor que cero
* Si es mayor de 0 “es positivo”
* Si es 0 imprime “No es positivo ni negativo”

4\. Escribe un programa StringSizeCheck que:

* Pide un String de 8 caracteres
* Imprime en pantalla “Demasiado pequeño” si el String tiene menos de 8 caracteres
* Imprime en pantalla “Demasiado grande” si el String tiene mas de 8 caracteres
* Si tiene 8 caracteres imprime “Es valido”
* HINT: para saber el número de caracteres de un String se utiliza el método `stringVariable.length()`

5\. Escribe un programa SumSubs que:

* Pide un número entero (a)
* Pide un número entero (b)
* Si a es mayor que b. Calcula la suma de a y b y muestra en pantalla el resultado
* Si a es igual a b. Calcula la resta de a - b y muestra el resultado en pantalla
* Si a es menor que b:
  * Pide al usuario otro numero c
  * Si c es mayor que la suma de a y b: imprime el mensaje “c es mayor que a + b”
  * Si c es menor que la suma de a y b: imprime el mensaje “c es menor que a + b”
  * c es igual que la suma de a y b: imprime el mensaje “c es igual que a + b”

6\. Escribe un programa Calculator que:

* Pide un String y lo guarda en una variable llamada operación
* Si el valor de operación es “+” (`operacion.equals("+")`) -> operacion == “+”
  * Pide un valor double (a)
  * Pide otro valor double (b)
  * Muestra el resultado de sumarlos
* Si el valor de la operación es “-”
  * Pide un valor int(a)
  * Pide otro valor int (b)
  * Muestra el resultado de restarlos
