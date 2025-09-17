---
cover: ../.gitbook/assets/java.jpeg
coverY: 0
---

# Expresiones y operadores

Los valores almacenados en las variables pueden ser combinados a través del uso de diferentes tipos de operadores.

## Operadores aritméticos

Son operadores que combinan valores numéricos y dan como resultado otros valores numéricos.

<table><thead><tr><th width="121">Operador</th><th width="139">Nombre</th><th width="219">Descripción</th><th width="112">Ejemplo</th><th>Try it</th></tr></thead><tbody><tr><td>+</td><td>Suma</td><td>Suma dos valores</td><td>x + y</td><td><a href="https://www.w3schools.com/java/tryjava.asp?filename=demo_oper_add">Try it »</a></td></tr><tr><td>-</td><td>Resta</td><td>Resta dos valores</td><td>x - y</td><td><a href="https://www.w3schools.com/java/tryjava.asp?filename=demo_oper_sub">Try it »</a></td></tr><tr><td>*</td><td>Multiplicación</td><td>Multiplica dos valores</td><td>x * y</td><td><a href="https://www.w3schools.com/java/tryjava.asp?filename=demo_oper_mult">Try it »</a></td></tr><tr><td>/</td><td>División</td><td>Divide un valor por otro</td><td>x / y</td><td><a href="https://www.w3schools.com/java/tryjava.asp?filename=demo_oper_div">Try it »</a></td></tr><tr><td>%</td><td>Módulo</td><td>Devuelve el resto de la división de dos números</td><td>x % y</td><td><a href="https://www.w3schools.com/java/tryjava.asp?filename=demo_oper_mod">Try it »</a></td></tr><tr><td>++</td><td>Incremento</td><td>Incrementa el valor de la variable en 1</td><td>x++</td><td><a href="https://www.w3schools.com/java/tryjava.asp?filename=demo_oper_inc">Try it »</a></td></tr><tr><td>--</td><td>Decremento</td><td>Decrementa el valor de la variable en 1</td><td>x--</td><td></td></tr></tbody></table>

Cuando se combinan varias variables y operadores obtenemos una expresión. Las expresiones son evaluadas en el momento que se ejecuta la sentencia y se calcula el resultado de las mismas.

```java
// Se declaran dos variables enteras
int number1 = 1;
int number2 = 3;

// Se declara result y se le asigna el resultado de la expresión que ambos números
int result = number1 + number2;

System.out.println(result);
```

## Operadores de comparación o relacionales

Son operadores que sirven para expresar comparaciones, el resultado las expresiones es un valor boolean (true o false).

<table><thead><tr><th width="114">Operador</th><th width="180">Nombre</th><th width="104">Ejemplo</th><th>Try it</th></tr></thead><tbody><tr><td>==</td><td>Igual a</td><td>x == y</td><td><a href="https://www.w3schools.com/java/tryjava.asp?filename=demo_oper_compare1">Try it »</a></td></tr><tr><td>!=</td><td>Distinto de</td><td>x != y</td><td><a href="https://www.w3schools.com/java/tryjava.asp?filename=demo_oper_compare2">Try it »</a></td></tr><tr><td>></td><td>Mayor que</td><td>x > y</td><td><a href="https://www.w3schools.com/java/tryjava.asp?filename=demo_oper_compare3">Try it »</a></td></tr><tr><td>&#x3C;</td><td>Menor que</td><td>x &#x3C; y</td><td><a href="https://www.w3schools.com/java/tryjava.asp?filename=demo_oper_compare4">Try it »</a></td></tr><tr><td>>=</td><td>Mayor o igual que</td><td>x >= y</td><td><a href="https://www.w3schools.com/java/tryjava.asp?filename=demo_oper_compare5">Try it »</a></td></tr><tr><td>&#x3C;=</td><td>Menor o igual que</td><td>x &#x3C;= y</td><td></td></tr></tbody></table>

```java
// Se declaran dos variables enteras
int number1 = 1;
int number2 = 3;

// Se declara result y se le asigna el resultado de comprobar si ambos números son iguales
boolean result = number1 == number2;

System.out.println(result);
```

### Operadores booleanos

Este tipo de operadores nos permiten combinar una o varias expresiones booleanas para crear condiciones más complejas.

| Operador | Símbolo |
| -------- | ------- |
| AND      | &&      |
| OR       | \|\|    |
| Negación | !       |

#### Conditional AND

Una expresión booleana compuesta utilizando el operador AND (&&) cumple la siguiente tabla lógica:

| expression1 | expression2 | expression1 && expression2 |
| ----------- | ----------- | -------------------------- |
| True        | False       | False                      |
| False       | True        | False                      |
| False       | False       | False                      |
| True        | True        | True                       |

####

```java
// Esta condición solo se cumple cuando: a es mayor que b Y b es mayor que 0
boolean aGreaterThan0AndB = a > b && b > 0;
```

#### Conditional OR

Una expresión booleana compuesta utilizando el operador OR (||) cumple la siguiente tabla lógica:

| expression1 | expression2 | expression1 \|\| expression2 |
| ----------- | ----------- | ---------------------------- |
| True        | True        | True                         |
| True        | False       | True                         |
| False       | True        | True                         |
| False       | False       | False                        |

```java
// Esta condición solo se cumple cuando: a es mayor que b O b es mayor que 0
boolean aGreaterThan0OrGreaterThanB = a > b || b > 0;
```

## [Mas información sobre operadores](https://www.w3schools.com/java/java_operators.asp)
