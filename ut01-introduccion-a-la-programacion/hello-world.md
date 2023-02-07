---
cover: ../.gitbook/assets/java.jpeg
coverY: 0
---

# Hello World

Vamos a comenzar compilando y ejecutando nuestro primer programa. Este programa, que llamaremos HelloWorld tiene como único cometido mostrar el mensaje `Hola mundo` cuando se ejecuta.

Pasos a seguir:

1. Instalar el JDK
2. Crear el fichero HelloWorld.java
3. Compilar HelloWorld.java
4. Ejecutar HelloWorld.class

### Instalar el JDK

Se puede descargar el instalador desde la página de [descargas](https://www.oracle.com/es/java/technologies/downloads/#java17) de Oracle

### Crear el fichero HelloWorld.java

Crea un fichero con el siguiente contenido

```java
public class HelloWorld {
    public static void main(String[] args){
          System.out.println("Hola mundo");
    }
}
```

### Compilar el programa

`javac HelloWorld.java`

### Ejecutar el programa

`java HelloWorld`

### Partes del programa

Este programa está compuesto por una única **clase** llamada `HelloWorld`. Dentro de la misma se ha definido un **método** `main` que contiene las sentencias que se van a ejecutar en este programa.

En este caso el programa tiene una única **sentencia** `System.out.println("Hola mundo");` que sirve para mostrar el texto `Hola mundo`.
