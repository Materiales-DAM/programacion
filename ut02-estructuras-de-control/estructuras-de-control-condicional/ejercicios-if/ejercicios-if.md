---
cover: ../../../.gitbook/assets/control-structures.gif
coverY: 0
---

# Soluciones If

1\. Escribe un programa que:

```java
package org.ies.tierno;

import java.util.Scanner;

public class Compare {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Introduce un número:");
        int n1 = scanner.nextInt();
        scanner.nextLine();

        System.out.println("Introduce otro número:");
        int n2 = scanner.nextInt();
        scanner.nextLine();

        if (n1 > n2) {
            System.out.println("Es mayor");
        } else if (n1 < n2) {
            System.out.println("Es menor");
        } else  {
            System.out.println("Son iguales");
        }
    }
}

```

2\. Escribe un programa que:

```java
package org.ies.tierno;

import java.util.Scanner;

public class IsEven {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Introduce un número:");
        int n = scanner.nextInt();
        scanner.nextLine();

        if (n == 0) {
            System.out.println("no es par ni impar");
        } else if (n % 2 == 0) {
            System.out.println("es par");
        } else {
            System.out.println("es impar");
        }
    }
}

```

3\. Escribe un programa que:

```java
package org.ies.tierno;

import java.util.Scanner;

public class ShowSign {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Introduce un número:");
        int n = scanner.nextInt();
        scanner.nextLine();

        if (n == 0) {
            System.out.println("No es positivo ni negativo");
        } else if (n > 0) {
            System.out.println("es positivo");
        } else {
            System.out.println("es negativo");
        }
    }
}

```

4\. Escribe un programa que:

```java
```

5\. Escribe un programa que:

```java
```

6\. Escribe un programa que:

```java
```
