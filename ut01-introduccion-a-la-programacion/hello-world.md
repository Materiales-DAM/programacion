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

`java HellowWorld`
