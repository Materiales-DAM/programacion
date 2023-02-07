---
cover: .gitbook/assets/java.jpeg
coverY: 0
---

# Entrada y salida del programa

En la mayor parte de las ocasiones vamos a querer que nuestros programas interactuen con el usuario durante su ejecución.​

Cuando un programa quiere **enviar información al usuario** utiliza algún canal de **salida**. Por ejemplo, imprimir un texto en pantalla para que el usuario lo lea.​

Por otro lado, vamos a querer que el usuario tenga la capacidad de **introducir datos** para que sean procesados por el programa a través de una **entrada de datos**. Por ejemplo, el  usuario introduce dos números enteros y el programa los suma.

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

| Método          | Descripción                               |
| --------------- | ----------------------------------------- |
| `nextBoolean()` | Lee un `boolean` que introduce el usuario |
| `nextByte()`    | Lee un `byte` que introduce el usuario    |
| `nextDouble()`  | Lee un `double` que introduce el usuario  |
| `nextFloat()`   | Lee un `float` que introduce el usuario   |
| `nextInt()`     | Lee un `int` que introduce el usuario     |
| `nextLine()`    | Lee un `String` que introduce el usuario  |
| `nextLong()`    | Lee un `long` que introduce el usuario    |
| `nextShort()`   | Lee un `short` que introduce el usuario   |

