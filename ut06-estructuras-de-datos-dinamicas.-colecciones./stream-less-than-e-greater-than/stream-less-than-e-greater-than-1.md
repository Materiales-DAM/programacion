---
cover: ../../.gitbook/assets/lambda.jpeg
coverY: 0
---

# Optional\<E>

`Optional` es una clase que nos permite representar si un determinado valor puede ser nulo o no, sin tener que usar el valor `null`. Es un concepto de programación funcional que evita la excepción más común en programación estructurada, `NullPointerException`.

Una variable de tipo `Optional<E>` puede:

* **Contener un valor de tipo `E`**
* **Estar vacía**: no contiene ningún valor de tipo `E`, por tanto está vacía.

A continuación se muestran varios ejemplos de cómo crear varios objetos de tipo `Optional<String>`

```java
// Este Optional nal contiene el valor "Hello"
Optional<String> optionalWithValue = Optional.of("Hello");
// Este Optional está vacío
Optional<String> optionalWithNullable = Optional.ofNullable(null);
// Este Optional está vacío
Optional<String> emptyOptional = Optional.empty();
```

## `Optional` en Streams

Existen numerosos métodos terminales que devuelven un `Optional`:

* `reduce`
* `findFirst`
* `max`
* `min`

## Métodos

### **`isPresent()` | `isEmpty()`**

Devuelve true si el `Optional` contiene un valor o no.

### **`ifPresent(v -> Void)`**

&#x20;Sirve para ejecutar una lambda&#x20;

<pre class="language-java"><code class="lang-java">
public void showMessage(Optional&#x3C;String> optionalMessage) {
    // Muestra el mensaje porque optionalMessage no es empty
<strong>    optionalMessage.ifPresent(message -> System.out.println("Msg: " + message));
</strong>}

// Mostrará el mensaje
showMessage(Optional.of("Hello, world"));
// No mostrará nada
showMessage(Optional.empty());
</code></pre>

### `orElse(E default)`

Sirve para extraer el valor que contiene el optional, en caso de que el Optional esté vacío devolverá el valor que se pasa al método orElse

<pre class="language-java"><code class="lang-java">public String extractValueOrDefault(Optional&#x3C;String> optionalMessage) {
<strong>    return optionalMessage.orElse("Hello");
</strong>}
Optional&#x3C;String> optionalMessage = Optional.of("Hola");
// message1 es Hola, porque optionalMessage no está vacío
String message1 = extractValueOrDefault(optionalMessage);
System.out.println(message1);
        
// message2 es Hello, porque optionalEmptyMessage está vacío
String message2 = extractValueOrDefault(Optional.empty());
System.out.println(message2);
</code></pre>

### **`get()`**

Devuelve el valor si está presente, o lanza una excepción si no lo está.

<pre class="language-java"><code class="lang-java">public String extractValue(Optional&#x3C;String> optionalMessage) {
    // El método get es mejor no utilizarlo nunca
<strong>    return optionalMessage.get("Hello");
</strong>}

// message1 es Hola, porque optionalMessage no está vacío
String getMessage1 = extractValue(Optional.of("Hola"));

// Lanza la excepción NoSuchElementException optionalEmptyMessage está vacío
String getMessage2 = extractValue(Optional.empty());
</code></pre>

### `map(A -> B)`

&#x20;Transforma el valor si está presente, o devuelve un `Optional` vacío si no lo está.

<pre class="language-java"><code class="lang-java">public Optional&#x3C;Integer> getMessageLength(Optional&#x3C;String> optionalMessage) {
    // El método get es mejor no utilizarlo nunca
<strong>    return optionalMessage.map(message -> message.length());
</strong>}
// Devuelve un Optional&#x3C;Integer> que contiene el valor 4
Optional&#x3C;Integer> lengthOpt1 = getMessageLength(Optional.of("Hola"));
System.out.println(lengthOpt1);

// Devuelve un Optional&#x3C;Integer> vacío, porque optionalEmptyMessage está vacío
Optional&#x3C;Integer> lengthOpt2 = getMessageLength(Optional.empty());
System.out.println(lengthOpt2);
</code></pre>

### `flatMap(A -> Optional<B>)`

Este método es de utilidad cuando la transformación que se va a aplicar al contenido del `Optional` produce otro `Optional`.

Por ejemplo, si queremos buscar un pedido dentro de un `Optional<Customer>`

<pre class="language-java"><code class="lang-java">    public static Optional&#x3C;Order> findOrder(Optional&#x3C;Customer> customerOpt, int orderId) {
<strong>        return customerOpt.flatMap((customer) ->
</strong>                customer.getOrders()
                        .stream()
                        .filter(order -> order.getId() == orderId)
                        // Devuelve un Optional&#x3C;Order>
<strong>                        .findFirst()
</strong>        );
    }
</code></pre>
