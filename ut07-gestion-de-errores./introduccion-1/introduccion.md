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

# error: cannot find symbol

Existen dos causas para este error:

## Variable no encontrada

&#x20;Se está intentando usar una variable que no existe, está mal escrita o no está en el scope\


{% code lineNumbers="true" %}
```java
package org.ies.tierno.compilation;

public class CanNotFindSymbolVariable {
    public static void main(String[] args) {
        String name = "hola";
        // No encuentra la variable nombre
        System.out.println(nombre);
    }
}
```
{% endcode %}

La salida del compilador es

```log
/home/mikel/errors/src/main/java/org/ies/tierno/compilation/CanNotFindSymbolVariable.java:7:28
java: cannot find symbol
  symbol:   variable nombre
  location: class org.ies.tierno.compilation.CanNotFindSymbolVariable
```

## Clase no encontrada

Se está intentando usar una variable que no existe, está mal escrita o no está en el scope

{% code lineNumbers="true" %}
```java
package org.ies.tierno.compilation;

public class CanNotFindSymbolClass {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println(scanner.nextLine());
    }
}
```
{% endcode %}

La salida del compilador es

```log
/home/mikel/errors/src/main/java/org/ies/tierno/compilation/CanNotFindSymbolClass.java:5:9
java: cannot find symbol
  symbol:   class Scanner
  location: class org.ies.tierno.compilation.CanNotFindSymbolClass
```
