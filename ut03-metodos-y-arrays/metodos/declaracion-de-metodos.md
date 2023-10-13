---
cover: ../../.gitbook/assets/method.jpg
coverY: 0
---

# Declaración de métodos

Antes de empezar a implementar el cuerpo de un método, debemos pensar bien la cabecera del mismo. Si la cabecera no es correcta, no habrá forma de implementar el cuerpo del método.

## La cabecera

En la cabecera del método vamos a definir las características generales del mismo:

* **Modificador de acceso**: Define desde qué partes del código se puede invocar el método. Por el momento, usaremos siempre la palabra reservada `public`.
* **Estático**: si ponemos la palabra reservada `static`, estamos indicando que el método es estático. De momento, todos los métodos serán estáticos.
* **Tipo del valor de retorno**: Muchos métodos realizan algún tipo cálculo y, al final, devuelven el resultado del mismo. El tipo de retorno define que tipo de valor se va a devolver. Por ejemplo, si definimos un método que calcula la división de dos números el tipo de retorno debería ser `double`, ya que el resultado de una división es de este tipo.
* **Nombre**: se debe usar siempre `lowerCamelCase`
* **Parámetros**: los parámetros son la lista de variables en las que se van a cargar los datos de entrada de ese método:
  * &#x20;Los parámetros vienen definidos entre paréntesis después del nombre del método.&#x20;
  * Cada parámetro se define por su tipo y el nombre del parámetro. Por ejemplo, `String name`
  * Si hay varios parámetros en un mismo método, la definición de cada uno se separa por el símbolo `,`

```java
// Modificador de acceso -> public
// Método estático
// Tipo de retorno double
// Nombre del método -> div
// Parámetros del método
//       numerator de tipo int
//       denominator de tipo int
public static double div(int numerator, int denominator){
    ... // Aquí va el cuerpo del método
}
```

### Métodos que no devuelven nada

En algunos casos vamos a crear métodos que en lugar de devolver un valor que calculamos, sirven para realizar alguna operación de entrada/salida. En este tipo de métodos pondremos la palabra reservada `void` en el tipo de retorno, lo que indica que no se devolverá nada.

Por ejemplo, si quiero implementar un método que recibe por parámetro un mensaje y lo imprime en pantalla añadiendo el texto "Mensaje " delante, haría lo siguiente

```java
public class PrintMessage {
    public static void printMessage(String message) {
        System.out.println("Mensaje " + message);
    }
    
    public static void main(String[] args){
        printMessage("Este es el primer mensaje");
        printMessage("Este es el segundo mensaje");
    }
}
```

## Cuerpo del método

En el cuerpo del método es donde se ponen la secuencia de instrucciones que deseamos que se ejecuten en este método.

Dentro de un método tenemos acceso a:

* Los parámetros del método
* Las variables definidas dentro del método
* Los campos estáticos definidos en la clase

Aquellos métodos que no sean `void`, deben incluir una sentencia final que devuelva un valor. Esta sentencia empieza con la palabra reservada `return` seguido del valor que se desea devolver. Después de la sentencia `return`, no es posible añadir más sentencias.

Veamos un ejemplo:

{% code lineNumbers="true" %}
```java
public class DivExample {
    
    public static void main(String[] args){
        int number1 = 4;
        int number2 = 5;
        
        // Se invoca el método div
        double res1 = div(number1, number2);
        
        System.out.println("El resultado es " + res1);
        
        // Se invoca el método div 
        double res2 = div(number2, number1);
        
        System.out.println("El resultado es " + res2);
    }

    public static double div(int numerator, int denominator){
        // Las variables disponibles son numerator y denominator
        // No están disponibles number1, number2, res1 ni res2 porque
        // no están definidas dentro de este método ni a nivel de clase
        // number1, number2, res1 y res2 solo existen en el método main
        double res = (double) numerator / denominator;
        return res;
    }
}
```
{% endcode %}

Cuando se llega a la línea 8 y se salta al interior del método `div`. En esta invocación `numerator` toma el valor 4 y `denominator` el valor 5, se computa el resultado y se devuelve 0.8 en la línea 24.

Una vez hecho el `return` la ejecución continua guardando el valor de retorno 0.8 en la variable `res1` (línea 8). Después muestra el resultado en pantalla.

Después, se llega a la línea 13, se salta al interior del método `div`. En esta invocación `numerator` toma el valor 5 y `denominator` el valor 4, se computa el resultado y se devuelve 1.25 en la línea 24.

Una vez hecho el `return` la ejecución continua guardando el valor de retorno 1.25 en la variable `res2` (línea 13). Después muestra el resultado en pantalla.
