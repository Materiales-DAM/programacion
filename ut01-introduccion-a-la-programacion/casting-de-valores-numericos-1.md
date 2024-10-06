---
cover: ../.gitbook/assets/java.jpeg
coverY: 0
---

# Casting de valores numéricos

En ocasiones, vamos a querer convertir un valor de un tipo a otro. Para ello existe el mecanismo del casting que nos permite cambiar de un tipo a otro siguiendo unas reglas determinadas.

```java
// Declaramos una variable one que toma el valor 1
int one = 1;
// Declaramos una variable onePointZero de tipo double, le asignamos el valor anterior
// Como la variable one era un entero el casting convierte el valor 1 a 1.0
double onePointZero = (double) one;
// Se imprime 1.0
System.out.println(onePointZero);
```

Cada tipo de datos define un conjunto de valores que se pueden tomar.

* int: números enteros entre -2,147,483,648 y 2,147,483,647
* long: números enteros entre -9,223,372,036,854,775,808 y 9,223,372,036,854,775,807
* float: números con decimales con hasta 6 o 7 dígitos
* double: números con decimales con hasta 15 dígitos

Algunos de estos tipos son subconjuntos de otros, es decir que todos los valores de un tipo existen en otro tipo.

<figure><img src="../.gitbook/assets/image (3) (1) (1) (1) (1).png" alt=""><figcaption><p>Conjuntos de tipos</p></figcaption></figure>

Cuando hacemos un casting de tipos es posible que vayamos de un tipo más grande a uno más pequeño o viceversa:

* Widening casting: son los casting en los que vamos de un conjunto más pequeño a uno más grande. En este tipo de casting no puede haber ningún problema ya que todos los valores del tipo de origen existen en el tipo de destino.

`byte -> short -> char -> int -> long -> float -> double`

* Narrow casting: son los casting en los que vamos de un conjunto más grande a uno más pequeño. Estos casting son potencialmente problemáticos ya que no todos los valores del tipo de origen son representables en el tipo de destino

`double -> float -> long -> int -> char -> short -> byte`
