---
cover: ../../.gitbook/assets/method.jpg
coverY: 0
---

# Cabecera del método

Antes de empezar a implementar el cuerpo de un método, debemos pensar bien la cabecera del mismo. Si la cabecera no es correcta, no habrá forma de implementar el cuerpo del método.

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
    return (double) numerator / denominator;
}
```
