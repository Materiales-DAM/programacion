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

<pre class="language-java"><code class="lang-java">Optional&#x3C;String> optionalMessage = Optional.of("Hola");

// Muestra el mensaje porque optionalMessage no es empty
<strong>optionalMessage.ifPresent(message -> System.out.println("Msg: " + message));
</strong>
Optional&#x3C;String> optionalEmptyMessage = Optional.empty();
// No hace nada porque optionalEmptyMessage es empty
<strong>optionalEmptyMessage.ifPresent(message -> System.out.println("Msg: " + message));
</strong></code></pre>

### `orElse(E default)`

Sirve para extraer el valor que contiene el optional, en caso de que el Optional esté vacío devolverá el valor que se pasa al método orElse

<pre class="language-java"><code class="lang-java">// message1 es Hola, porque optionalMessage no está vacío
<strong>var message1 = optionalMessage.orElse("Hello");
</strong>System.out.println(message1);
        
// message2 es Hello, porque optionalEmptyMessage está vacío
<strong>var message2 = optionalEmptyMessage.orElse("Hello");
</strong>System.out.println(message2);
</code></pre>

### **`get()`**

Devuelve el valor si está presente, o lanza una excepción si no lo está.

```java
// message1 es Hola, porque optionalMessage no está vacío
var getMessage1 = optionalMessage.get();

// Lanza la excepción NoSuchElementException optionalEmptyMessage está vacío
var getMessage2 = optionalEmptyMessage.get();
```

### `map(A -> B)`

&#x20;Transforma el valor si está presente, o devuelve un `Optional` vacío si no lo está.

<pre class="language-java"><code class="lang-java">// Devuelve un Optional&#x3C;Integer> que contiene el valor 4
<strong>Optional&#x3C;Integer> lengthOpt1 = optionalMessage.map(message -> message.length());
</strong>System.out.println(lengthOpt1);

// Devuelve un Optional&#x3C;Integer> vacío, porque optionalEmptyMessage está vacío
<strong>Optional&#x3C;Integer> lengthOpt2 = optionalEmptyMessage.map(message -> message.length());
</strong>System.out.println(lengthOpt2);
</code></pre>

### `flatMap(A -> Optional<B>)`

Este método es de utilidad cuando la transformación que se va a aplicar al contenido del `Optional` produce otro `Optional`.

Por ejemplo, si queremos buscar un pedido dentro de un `Optional<Customer>`

<pre class="language-java"><code class="lang-java">// En este flatMap A es Customer y B es Order
<strong>Optional&#x3C;Order> orderOpt = customerOpt.flatMap(customer ->
</strong>                        customer.getOrders()
                                .stream()
                                .filter(order -> order.getId() == orderId)
                                .findFirst()
                );
</code></pre>
