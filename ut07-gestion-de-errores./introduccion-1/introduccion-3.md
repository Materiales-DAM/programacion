---
cover: ../../.gitbook/assets/quality-assurance-code-bug.jpg
coverY: 110.50526315789473
---

# unreachable statement

El error "unreachable statement" en Java indica que hay una instrucción en tu código que nunca se ejecutará, ya que está precedida por una instrucción que termina la ejecución del método o bloque de código antes de llegar a esa línea.

Aquí tienes algunos ejemplos para ilustrar este error:

#### Instrucción después de un return

```java
class UnreachableStatementReturn {
    public static void main(String[] args) {
        System.out.println("Hola");
        return; // Esta línea termina la ejecución del método main
        System.out.println("Mundo"); // Error: unreachable statement
    }
}
```

En este ejemplo, la línea `System.out.println("Mundo");` nunca se ejecutará porque está después de un `return`, que termina la ejecución del método `main`.

#### Instrucción después de un break

```java
public class UnreachableStatementBreak {
    public static void main(String[] args) {
        for (int i = 0; i < 10; i++) {
            System.out.println("Hola");
            break;
            System.out.println("Mundo");
        }
    }
}
```

Aquí, la línea `System.out.println("Mundo");` nunca se ejecutará porque está después de un `break`, que termina la ejecución del bucle.

#### Instrucción después de un continue

```java
public class UnreachableStatementContinue {
    public static void main(String[] args) {
        for (int i = 0; i < 10; i++) {
            System.out.println("Hola");
            continue;
            System.out.println("Mundo");
        }
    }
}
```

Aquí, la línea `System.out.println("Mundo");` nunca se ejecutará porque está después de un `continue`, que pasa a la siguiente iteración.

#### Instrucción después de un bucle infinito

```java
public class UnreachableStatementInfiniteLoop {
    public static void main(String[] args) {
        while (true) {
            System.out.println("Hola");
        }
        System.out.println("Mundo");
    }
}
```

Aquí, la línea `System.out.println("Mundo");` nunca se ejecutará porque está después de un bucle infinito.
