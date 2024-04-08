---
cover: ../../.gitbook/assets/method.jpg
coverY: 0
---

# Cómo deducir la cabecera a partir de enunciados

Que la cabecera del método sea correcta es fundamental para poder implementarlo. Veamos unas orientaciones para hacerla correctamente:&#x20;

* **Modificador de acceso**: Define desde qué partes del código se puede invocar el método. Por el momento, usaremos siempre la palabra reservada `public`.
* **Estático**: si ponemos la palabra reservada `static`, estamos indicando que el método es estático. De momento, todos los métodos serán estáticos. En POO los métodos no serán estáticos.
* **Tipo del valor de retorno**: En el enunciado el tipo de retorno es el tipo de lo que vamos a devolver. Por ejemplo:
  * Dados dos números enteros, **devuelve la suma de los mismos**: como la suma de dos enteros es otro entero el tipo de retorno será `int`
  * Dado un nif, **devuelve el cliente** con ese nif: el tipo de retorno será Customer
* **Nombre**: se debe usar siempre `lowerCamelCase`, que sea descriptivo de la acción que realiza el método:
  * Dados dos números enteros, devuelve la **suma** de los mismos: el método se puede llamar sumar
  * Dado un nif, **devuelve el cliente** con ese nif: el método se puede llamar buscarCliente
* **Parámetros**: los parámetros son los valores que recibe el método, en los enunciados estarán indicados con las palabras **dado un**:
  * **Dados dos números enteros**, devuelve la suma de los mismos:  tiene dos parámetros de tipo entero
  * **Dado un nif**, devuelve el cliente con ese nif: el método tiene un parámetro de tipo String llamado nif.
