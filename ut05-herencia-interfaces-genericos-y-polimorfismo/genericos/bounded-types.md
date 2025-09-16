---
cover: ../../.gitbook/assets/generics.jpg
coverY: 0
---

# Bounded types

Es posible establecer restricciones sobre los parámetros de tipos para que, en lugar de aceptar cualquier tipo, se pueda definir cuales son válidos.

Por ejemplo, si quisiéramos tener un interfaz de Reader que sólo se pudiera implementar para animales.

```java
// Este interface solo se podrá extender usando una T que sea Animal o un subtipo de ANimal
public interface AnimalReader<T extends Animal> {
    T read();
}
```
