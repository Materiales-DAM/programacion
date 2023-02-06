# Sentencias y comentarios

Simplificando, podríamos definir un programa con una **secuencia de sentencias** (órdenes) que se ejecutan una tras otra. Cuando ya no quedan sentencias por ejecutar el programa se acaba.

En Java el programa comienza ejecutando las sentencias que se encuentren en el **método main** de la clase que se esté ejecutando.

```java
public class PrintProgram {
    public static void main(String[] args) {
        // Esto es un comentario

        // Esta sentencia mostrará en pantalla el texto Hola mundo cuando se invoque
        System.out.println("Hola mundo");

        // Esta sentencia mostrará en pantalla el texto Hasta pronto cuando se invoque
        System.out.println("Hasta pronto");
    }
}

```

En el ejemplo anterior tenemos un programa llamado `PrintProgram`, dicho programa define la secuencia de sentencias dentro del método main.

En este caso hay dos sentencias, la primera muestra el texto `Hola mundo`y la segunda muestra el texto `Hasta pronto`. Cuando se ejecute este programa la salida mostrará lo siguiente

```
Hola mundo
Hasta pronto

Process finished with exit code 0
```

Como se puede observar, en Java las sentencias acaban con el símbolo `;`

Es posible añadir **comentarios** en el código que ayuden a entender para qué sirve cada sentencia. Para escribir un comentario la línea debe empezar por `//`, después se escribe el comentario. Normalmente, una línea de comentario hace referencia a la sentencia que se encuentra después del comentario.
