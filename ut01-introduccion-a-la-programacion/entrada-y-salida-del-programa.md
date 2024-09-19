---
cover: ../.gitbook/assets/java.jpeg
coverY: 0
---

# Entrada y salida del programa

En la mayor parte de las ocasiones vamos a querer que nuestros programas interactuen con el usuario durante su ejecución.​

Cuando un programa quiere **enviar información al usuario** utiliza algún canal de **salida**. Por ejemplo, imprimir un texto en pantalla para que el usuario lo lea.​

Por otro lado, vamos a querer que el usuario tenga la capacidad de **introducir datos** para que sean procesados por el programa a través de una **entrada de datos**. Por ejemplo, el usuario introduce dos números enteros y el programa los suma.

## Salida estándar

La forma más sencilla de enviar una información al usuario en Java es a través de la salida estándar.​

```java
// Esta sentencia envía un mensaje a la salida estándar
System.out.println("Muestra este texto");
```

## ​Entrada estánda con java.util.Scanner

Cuando lo que queremos es que sea el usuario quien introduce datos que luego va a usar el programa tenemos una entrada de datos.​ Una forma de realizar entradas de datos es utilizando la utilidad `Scanner`.​ Para poder utilizarla hay que importar el paquete `java.util.Scanner​`

```java
import java.util.Scanner;

public class StandardInputOutputProgram {
    public static void main(String[] args) {
        // Creamos la utilidad scanner con la que después solicitamos datos al usuario
        Scanner scanner = new Scanner(System.in);
        // Mostramos por pantalla un mensaje para que el usuario sepa que debe
        // introducir un texto
        System.out.println("Introduce tu nombre de usuario...");
        // Leemos un String que nos pasa el usuario y lo guardamos en username
        String username = scanner.nextLine();
        // Mostramos un texto de bienvenida al usuario
        System.out.println("Bienvenido " + username);
    }
}

```

### Métodos de Scanner

<table><thead><tr><th width="188">Método</th><th>Descripción</th></tr></thead><tbody><tr><td><code>nextBoolean()</code></td><td>Lee un <code>boolean</code> que introduce el usuario</td></tr><tr><td><code>nextByte()</code></td><td>Lee un <code>byte</code> que introduce el usuario</td></tr><tr><td><code>nextDouble()</code></td><td>Lee un <code>double</code> que introduce el usuario</td></tr><tr><td><code>nextFloat()</code></td><td>Lee un <code>float</code> que introduce el usuario</td></tr><tr><td><code>nextInt()</code></td><td>Lee un <code>int</code> que introduce el usuario</td></tr><tr><td><code>nextLine()</code></td><td>Lee un <code>String</code> que introduce el usuario</td></tr><tr><td><code>nextLong()</code></td><td>Lee un <code>long</code> que introduce el usuario</td></tr><tr><td><code>nextShort()</code></td><td>Lee un <code>short</code> que introduce el usuario</td></tr></tbody></table>

**IMPORTANTE**: Después de utilizar cualquier método del Scanner que no sea `scanner.nextLine()`, se debe añadir una sentencia `scanner.nextLine()` para pasar a la siguiente línea de entrada.

```java
import java.util.Scanner;

public class StandardInputOutputProgram {
    public static void main(String[] args) {
        // Creamos la utilidad scanner con la que después solicitamos datos al usuario
        Scanner scanner = new Scanner(System.in);
        // Mostramos por pantalla un mensaje para que el usuario sepa que debe
        // introducir la edad
        System.out.println("Introduce tu edad...");
        // Leemos un número entero y lo guardamos en age
        int age = scanner.nextInt();
        // Esta sentencia debe ir siempre después de un nextInt() para pasar a la
        // siguiente línea de la entrada estándar
        scanner.nextLine();
        // Mostramos la edad introducida por el usuario
        System.out.println("Tienes " + age + " años");
    }
}
```
