---
cover: ../.gitbook/assets/tree.png
coverY: 94.60266666666666
---

# Factory methods

Los _factory methods_ de colecciones en Java son **métodos estáticos** (como `List.of`, `Set.of` o `Map.of`) introducidos a partir de Java 9 que permiten crear instancias de colecciones de forma concisa y segura **sin usar constructores**. Devuelven implementaciones internas de las interfaces de colección, normalmente **inmutables**, **no admiten valores `null`** y ocultan la clase concreta utilizada, lo que mejora la legibilidad del código y reduce errores. Al centralizar la creación en la propia interfaz, facilitan un estilo declarativo y evitan la exposición innecesaria de detalles de implementación.

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
