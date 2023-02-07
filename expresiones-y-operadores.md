---
cover: .gitbook/assets/java.jpeg
coverY: 0
---

# Expresiones y operadores

Los valores almacenados en las variables pueden ser combiando a través del uso de diferentes tipos de operadores.

## Operadores aritméticos

Son operadores que combinan valores numéricos y dan como resultado otros valores numéricos.

| Operador | Nombre         | Descripción                                     | Ejemplo | Try it                                                                           |
| -------- | -------------- | ----------------------------------------------- | ------- | -------------------------------------------------------------------------------- |
| +        | Suma           | Suma dos valores                                | x + y   | [Try it »](https://www.w3schools.com/java/tryjava.asp?filename=demo\_oper\_add)  |
| -        | Resta          | Resta dos valores                               | x - y   | [Try it »](https://www.w3schools.com/java/tryjava.asp?filename=demo\_oper\_sub)  |
| \*       | Multiplicación | Multiplica dos valores                          | x \* y  | [Try it »](https://www.w3schools.com/java/tryjava.asp?filename=demo\_oper\_mult) |
| /        | Division       | Divide un valor por otro                        | x / y   | [Try it »](https://www.w3schools.com/java/tryjava.asp?filename=demo\_oper\_div)  |
| %        | Módulo         | Devuelve el resto de la división de dos números | x % y   | [Try it »](https://www.w3schools.com/java/tryjava.asp?filename=demo\_oper\_mod)  |
| ++       | Incremento     | Incrementa el valor de la variable en 1         | x++     | [Try it »](https://www.w3schools.com/java/tryjava.asp?filename=demo\_oper\_inc)  |
| --       | Decremento     | crementa el valor de la variable en 1           | x--     |                                                                                  |

Cuando se combinan varias variables y operadores obtenemos una expresión. Las expresiones son evaluadas en el momento que se ejecuta la sentencia y se calcula el resultado de las mismas.

```java
// Se declaran dos variables enteras
int number1 = 1;
int number2 = 3;

// Se declara result y se le asigna el resultado de la expresión que ambos números
int result = number1 + number2;

System.out.println(result);
```

## Operadores condicionales

Son operadores que sirven para expresar condiciones, el resultado las expresiones condicionales es un valor boolean (true o false).

| Operador | Nombre            | Ejemlo | Try it                                                                               |
| -------- | ----------------- | ------ | ------------------------------------------------------------------------------------ |
| ==       | Igual a           | x == y | [Try it »](https://www.w3schools.com/java/tryjava.asp?filename=demo\_oper\_compare1) |
| !=       | Distinto de       | x != y | [Try it »](https://www.w3schools.com/java/tryjava.asp?filename=demo\_oper\_compare2) |
| >        | Mayor que         | x > y  | [Try it »](https://www.w3schools.com/java/tryjava.asp?filename=demo\_oper\_compare3) |
| <        | Menor que         | x < y  | [Try it »](https://www.w3schools.com/java/tryjava.asp?filename=demo\_oper\_compare4) |
| >=       | Mayor o igual que | x >= y | [Try it »](https://www.w3schools.com/java/tryjava.asp?filename=demo\_oper\_compare5) |
| <=       | Menor o igual que | x <= y |                                                                                      |

```java
// Se declaran dos variables enteras
int number1 = 1;
int number2 = 3;

// Se declara result y se le asigna el resultado de comprobar si ambos números son iguales
boolean result = number1 == number2;

System.out.println(result);
```
