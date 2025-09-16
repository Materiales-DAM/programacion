---
cover: ../.gitbook/assets/tree.png
coverY: 94.60266666666666
---

# Smart constructors

Existen los llamados constructores inteligentes (smart constructors), que nos permiten crear **colecciones inmutables** con sus datos de una manera más sencilla.

## Listas

```java
// Crea un lista inmutable con los números 2, 4, 1, 2
var numbers = List.of(2, 4, 1, 2);
```

## Sets

```java
// Crea un set inmutable con los números 2, 4, 1, 2
var numbers = Set.of(2, 4, 1, 2);
```

## Mapas

```java
// Crea un Map<String, Integer> inmutable con los pares:
// es -> 34
// fr -> 33
// uk -> 44
// us -> 1
var numbers = Map.of(
    "es", 34,
    "fr", 33,
    "uk", 44,
    "us", 1
);
```
