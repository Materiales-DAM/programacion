---
cover: ../../.gitbook/assets/lambda.jpeg
coverY: 0
layout:
  cover:
    visible: true
    size: hero
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Optional\<E>

`Optional` es una clase que nos permite representar si un determinado valor puede ser nulo o no, sin tener que usar el valor `null`. Es un concepto de programación funcional que evita la excepción más común en programación estructurada, `NullPointerException`.

Una variable de tipo Optional\<E> puede:

* **Contener un valor de tipo E**
* **Estar vacía**: no contiene ningún valor de tipo E, por tanto está vacía.

A continuación se muestran varios ejemplos de cómo crear varios objetos de tipo `Optional<String>`

<pre class="language-java"><code class="lang-java"><strong>// Este Optional nal contiene el valor "Hello"
</strong><strong>Optional&#x3C;String> optionalWithValue = Optional.of("Hello");
</strong><strong>// Este Optional está vacío
</strong>Optional&#x3C;String> optionalWithNullable = Optional.ofNullable(null);
// Este Optional está vacío
Optional&#x3C;String> emptyOptional = Optional.empty();
</code></pre>

## Optional en Streams

Existen numerosos métodos terminales de&#x20;

## Métodos

### **isPresent() | isEmpty()**

Devuelve true si el `Optional` contiene un valor o no.

### **ifPresent(v -> Void)**

&#x20;Sirve para ejecutar una lambda&#x20;

```java
Optional<String> optionalMessage = Optional.of("Hola");

// Muestra el mensaje porque optionalMessage no es empty
optionalMessage.ifPresent(message -> System.out.println("Msg: " + message));

Optional<String> optionalEmptyMessage = Optional.empty();
// No hace nada porque optionalEmptyMessage es empty
optionalEmptyMessage.ifPresent(message -> System.out.println("Msg: " + message));

```

### orElse(E default)

Sirve para extraer el valor que contiene el optional, en caso de que el Optional esté vacío devolverá el valor que se pasa al método orElse

```java
Optional<String> optionalMessage = Optional.of("Hola");

// message1 es Hola, porque optionalMessage no está vacío
var message1 = optionalMessage.orElse("Hello");

Optional<String> optionalEmptyMessage = Optional.empty();
// message2 es Hello, porque optionalEmptyMessage está vacío
var message2 = optionalEmptyMessage.orElse("Hello");
```

### **get()**

Devuelve el valor si está presente, o lanza una excepción si no lo está.

```java
Optional<String> optionalMessage = Optional.of("Hola");

// message1 es Hola, porque optionalMessage no está vacío
var message1 = optionalMessage.get();

Optional<String> optionalEmptyMessage = Optional.empty();
// Lanza la excepción NoSuchElementException optionalEmptyMessage está vacío
var message2 = optionalEmptyMessage.get();
```

### map(A -> B)

&#x20;Transforma el valor si está presente, o devuelve un `Optional` vacío si no lo está.

```java
Optional<String> optionalMessage = Optional.of("Hola");

// Devuelve un Optional<Integer> que contiene el valor 4
Optional<Integer> lengthOpt1 = optionalMessage.map(message -> message.length());

Optional<String> optionalEmptyMessage = Optional.empty();
// Devuelve un Optional<Integer> vacío, porque optionalEmptyMessage está vacío
var lengthOpt2 = optionalEmptyMessage.map(message -> message.length());
```
