---
cover: ../../.gitbook/assets/control-structures.gif
coverY: 0
---

# Operadores condicionales

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
if(a > b && b > 0){
    
} 
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
if(a > b || b > 0){
    
} 
```
