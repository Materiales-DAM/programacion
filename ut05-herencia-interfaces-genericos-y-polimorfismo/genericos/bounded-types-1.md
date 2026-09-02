---
cover: ../../.gitbook/assets/generics.jpg
coverY: 0
layout:
  width: default
  cover:
    visible: true
    size: hero
    mask: none
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
  metadata:
    visible: true
  tags:
    visible: true
  actions:
    visible: true
---

# Métodos genéricos

Un **método genérico** es un método que “recibe” un **tipo `T`** y lo usa para devolver/aceptar ese mismo tipo .

La sintaxis es:

```java
public static <T> T someMethod(...) { ... }
```

Existen varios casos en los que sería útil, por ejemplo para un constructor de listas

```java
public static <T> List<T> lista(T v1, T v2) { 
    return List.of(v1, v2);
}
```

Luego podríamos usar este método de la siguiente manera

```java
// Crea una lista [2,3]
List<Integer> numbers = lista(2, 4);

// Crea una lista ["Bob", "Peppa"]
List<String> names = lista("Bob", "Peppa");
```
