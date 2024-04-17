---
cover: ../../../.gitbook/assets/quality-assurance-code-bug.jpg
coverY: 110.50526315789473
layout:
  cover:
    visible: true
    size: full
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
---

# method \<X> in class \<Y> cannot be applied to given types

El mensaje de error "method \<X> in class \<Y> cannot be applied to given types" en Java indica que estás intentando llamar a un método en una clase con argumentos que no coinciden con ninguno de los métodos definidos en esa clase.

Supongamos que tienes una clase llamada `Calculadora` con un método `sumar` que toma dos números como argumentos:

```java
package org.ies.tierno.compilation;

class Calculadora {
    public int sumar(int a, int b) {
        return a + b;
    }
}
```

Ahora, en otro lugar de tu código, intentas llamar al método `sumar` con un solo argumento:

{% code lineNumbers="true" %}
```java
package org.ies.tierno.compilation;

class CannotBeAppliedExample {
    public static void main(String[] args) {
        Calculadora calc = new Calculadora();
        int resultado = calc.sumar(5); // Error: argumentos incorrectos
        System.out.println(resultado);
    }
}

```
{% endcode %}

El error resultante es

```log
/home/mikel/errors/src/main/java/org/ies/tierno/compilation/CannotBeAppliedExample.java:6:29
java: method sumar in class org.ies.tierno.compilation.Calculadora cannot be applied to given types;
  required: int,int
  found: int
  reason: actual and formal argument lists differ in length
```
