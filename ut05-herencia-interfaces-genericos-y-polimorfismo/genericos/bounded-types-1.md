---
cover: ../../.gitbook/assets/generics.jpg
coverY: 0
---

# Métodos genéricos

Un **método genérico** es un método que “recibe” un **tipo `T`** y lo usa para devolver/aceptar ese mismo tipo .

La sintaxis es:

```java
public static <T> T someMethod(...) { ... }
```

Existen varios casos en los que sería útil, por ejemplo para un constructor de arrays

```java
public static <T> T[] array(T v1, T v2) { 
    T[] array = {v1, v2};
    return array;
}
```

Luego podríamos usar este método de la siguiente manera

```java
// Crea un array [2,3]
Integer[] numbers = array<>(2, 4);

// Crea un array ["Bob", "Peppa"]
String[] names = array<>("Bob", "Peppa");


```
