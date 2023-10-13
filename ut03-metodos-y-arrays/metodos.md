---
cover: ../.gitbook/assets/method.jpg
coverY: 0
---

# Métodos

Un método en Java es un conjunto de instrucciones definidas dentro de una clase, que realizan una determinada tarea y a las que podemos invocar mediante un nombre.

Normalmente un mismo método suele ser invocado varias veces en una misma ejecución de un programa.

## Declaración de métodos estáticos

Los métodos se declaran dentro de clases y constan de dos partes:

* **Cabecera del método**: la cabecera es la línea en la que se definen las características del método:
  * **Nombre** del método: la convención es `lowerCamelCase` (como en las variables)
  * **Parámetros** del método: los parámetros son los datos que va a recibir el método en su invocación y se deben utilizar en el cuerpo del método
  * **Modificador de acceso**: de momento será siempre `public`
  * **Tipo de retorno**: Algunos métodos devuelven valores al finalizar su ejecución, el tipo de retorno definde que tipo de valor va a devolver.
* **Cuerpo del método**: El cuerpo del método empieza después de los paréntesis

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption><p>Ejemplo de método que calcula la raíz cuadrada de c</p></figcaption></figure>

Por ejemplo, un método que, dado un nombre, devuelve un saludo:

{% code fullWidth="true" %}
```java
public class MyClass{
    // Esta es la cabecera del método
    // El  nombre de este método es helloMessage
    // Tiene un parámetro de tipo String llamado name
    // Su modificador de acceso es public
    // Su tipo de retorno es String
    // Es un método estático
    public static String helloMessage(String name){
        // Este es el cuerpo del método.
        // Contiene la secuencia de instrucciones que
        // se van a ejecutar cada vez que se invoca
        // el método
        String responseMessage = "Hola " + name;
        return responseMessage;
    }
}
```
{% endcode %}

## Invocación de métodos estáticos

Declarar un método en un programa no tiene ningún efecto sobre el mismo si dicho método no es invocado nunca. Un mismo método puede ser invocado varias veces en la ejecución de un programa.

Para invocar un método debemos poner su nombre, abrir y cerrar paréntesis y, dentro de los mismos, pasar los valores que queramos en esa invocación.

```java
public class MyClass{

    // Si el método myMethod no se invoca desde el main
    // es como si no existiera
    public static void main(String[] args) {
        String name1 = "Bob";
        String name2 = "Peppa";
        
        // Se invoca el método por primera vez pasando
        // por parámetro el valor "Bob"
        String response1 = helloMessage(name1);
        // Se invoca el método por segunda vez pasando
        // por parámetro el valor "Peppa"
        String response2 = helloMessage(name2);
        
        // Aparecerá en pantalla "Hola Bob"
        System.out.println(response1);
        // Aparecerá en pantalla "Hola Peppa"
        System.out.println(response2);
    }
    
    // Declaración del método helloMessage
    public static String helloMessage(String name){
        String responseMessage = "Hola " + name;
        return responseMessage;
    }
}
```

