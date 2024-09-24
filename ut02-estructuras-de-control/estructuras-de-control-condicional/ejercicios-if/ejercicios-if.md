---
cover: ../../../.gitbook/assets/control-structures.gif
coverY: 0
---

# Soluciones If

1\. Escribe un programa que:

```java
import java.util.Scanner;

public class If1 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("Introduce un número:");
        int n1 = scanner.nextInt();
        scanner.nextLine();

        System.out.println("Introduce otro número");
        int n2 = scanner.nextInt();
        scanner.nextLine();

        if (n1 > n2) {
            System.out.println("Es mayor");
        } else if (n1 < n2) {
            System.out.println("Es menor");
        } else {
            System.out.println("Es igual");
        }
    }
}
```

2\. Escribe un programa que:

```java
import java.util.Scanner;

public class If2 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("Introduce un número");
        int n = scanner.nextInt();
        scanner.nextLine();

        if (n == 0) {
            System.out.println("No es par ni impar");
        } else if (n % 2 == 0) {
            System.out.println("Es par");
        } else {
            System.out.println("Es impar");
        }
    }
}
```

3\. Escribe un programa que:

* Pide un número entero
* Imprime en pantalla “Es negativo” cuando el número es menor que cero
* Si es mayor de 0 “es positivo”
* Si es 0 imprime “No es positivo ni negativo”

4\. Escribe un programa que:

* Pide un String de 8 caracteres
* Imprime en pantalla “Demasiado pequeño” si el String tiene menos de 8 caracteres
* Imprime en pantalla “Demasiado grande” si el String tiene mas de 8 caracteres
* Si tiene 8 caracteres imprime “Es valido”
* HINT: para saber el número de caracteres de un String se utiliza el método `stringVariable.length()`

5\. Escribe un programa que:

* Pide un número entero (a)
* Pide un número entero (b)
* Si a es mayor que b. Calcula la suma de a y b y muestra en pantalla el resultado
* Si a es igual a b. Calcula la resta de a - b y muestra el resultado en pantalla
* Si a es menor que b:
  * Pide al usuario otro numero c
  * Si c es mayor que la suma de a y b: imprime el mensaje “c es mayor que a + b”
  * Si c es menor que la suma de a y b: imprime el mensaje “c es menor que a + b”
  * c es igual que la suma de a y b: imprime el mensaje “c es igual que a + b”

6\. Escribe un programa que:

* Pide un String y lo guarda en una variable llamada operación
* Si el valor de operación es “+” (`operacion.equals(`
* `"+")`) -> operacion == “+”
* Pide un valor double (a)
* Pide otro valor double (b)
* Muestra el resultado de sumarlos
* Si el valor de la operación es “-”
* Pide un valor int(a)
* Pide otro valor int (b)
* Muestra el resultado de restarlos
