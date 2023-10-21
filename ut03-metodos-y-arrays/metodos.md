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

<figure><img src="../.gitbook/assets/image (2) (1).png" alt=""><figcaption><p>Ejemplo de método que calcula la raíz cuadrada de c</p></figcaption></figure>

Por ejemplo, un método que, dado un nombre, devuelve un saludo:

{% code fullWidth="true" %}
```java
public class HelloMessageClass {
    // Esta es la cabecera del método
    // El  nombre de este método es buildHelloMessage
    // Tiene un parámetro de tipo String llamado name
    // Su modificador de acceso es public
    // Su tipo de retorno es String
    // Es un método estático
    public static String buildHelloMessage(String name){
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

Para invocar un método debemos poner su nombre, abrir y cerrar paréntesis y, dentro de los mismos, pasar los valores que queramos en esa invocación.

```java
String name1 = "Bob";
// Se invoca el método pasando por parámetro el valor "Bob"
String response1 = buildHelloMessage(name1);
```

Cuando se invoca un método el programa salta desde la sentencia de invocación a la primera sentencia que hay dentro del cuerpo del método invocado. Si el método tiene parámetros, los valores que toman durante la ejecución son los que se han pasado en la invocación.

En el ejemplo anterior, el parámetro `name` del método `buildHelloMessage` tomará el valor `"Bob"` durante su ejecución.

### Ejemplo completo HelloMessageClass

{% code lineNumbers="true" %}
```java
public class HelloMessageClass {

    // Si el método buildHelloMessage no se invoca desde el main
    // es como si no existiera
    public static void main(String[] args) {
        String name1 = "Bob";
        String name2 = "Peppa";
        
        // Se invoca el método por primera vez pasando
        // por parámetro el valor "Bob"
        String response1 = buildHelloMessage(name1);
        // Se invoca el método por segunda vez pasando
        // por parámetro el valor "Peppa"
        String response2 = buildHelloMessage(name2);
        
        // Aparecerá en pantalla "Hola Bob"
        System.out.println(response1);
        // Aparecerá en pantalla "Hola Peppa"
        System.out.println(response2);
    }
    
    // Declaración del método buildHelloMessage
    public static String buildHelloMessage(String name){
        String responseMessage = "Hola " + name;
        return responseMessage;
    }
} 
```
{% endcode %}

Por tanto, declarar un método en un programa no tiene ningún efecto si no es invocado nunca. Como hemos visto, un mismo método puede ser invocado varias veces en la ejecución de un programa y los parámetros tomarán los valores que se hayan pasado en cada invocación.&#x20;
