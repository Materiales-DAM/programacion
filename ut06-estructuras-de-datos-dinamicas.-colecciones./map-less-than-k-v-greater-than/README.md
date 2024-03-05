---
cover: ../../.gitbook/assets/tree.png
coverY: 94.60266666666666
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

# Map\<K, V>

Los mapas son estructuras de datos que almacenan elementos en **pares clave-valor**, donde **cada clave es única.** Se utilizan para acceder a un valor a partir de la clave de forma sencilla y eficiente.&#x20;

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption><p>Mapa que relaciona códigos de país con el nombre del país</p></figcaption></figure>

La interface para trabajar con mapas en Java es `Map`, que define un conjunto de métodos para manipular los datos almacenados. Algunas de las principales características de los mapas son:

* Almacenan **pares clave-valor**
* En cada mapa se debe definir el tipo de las claves y el tipo del valor:
  * **K**: es el tipo de las claves.
  * **V**:  es el tipo de los valores.
* En un mismo mapa, **no puede haber dos pares clave-valor con la misma clave**.&#x20;
* Los mapas están **optimizados para la realización de búsquedas por la clave**.
* &#x20;Las dos implementaciones más utilizadas son **HashMap** (hashtable asociativa) y TreeMap (SBT asociativo). Internamente, funcionan de manera parecida al HashSet y TreeSet de las claves, la diferencia es que además añaden a cada clave un valor asociado.

## Operaciones

### V put(K key, V value)

Almacena un nuevo par clave-valor. El primer parámetro es la clave a almacenar y el segundo parámetro es el valor que se desea asociar a la clave. Si la clave ya existía en el mapa, el nuevo valor sustituye al anterior.

<pre class="language-java"><code class="lang-java">Map&#x3C;String, Integer> prefixes = new HashMap&#x3C;>();
<strong>prefixes.put("ES", 34);
</strong><strong>prefixes.put("US", 1);
</strong>prefixes.put("UK", 44);
// Este par sustituye al par creado en el primer put
prefixes.put("ES", 34);
</code></pre>

### boolean containsKey(K key)

Comprueba si existe un elemento con la clave key. El tipo del parámetro debe ser el tipo de las claves

<pre class="language-java"><code class="lang-java">Map&#x3C;String, Integer> prefixes = new HashMap&#x3C;>();
<strong>prefixes.put("ES", 340);
</strong><strong>prefixes.put("US", 1);
</strong>prefixes.put("UK", 44);
prefixes.put("ES", 34);

if(prefixes.containsKey("ES")) {
    System.out.println("Existe el prefijo de España");
}
</code></pre>

### V get(K key)

Devuelve el valor asociado a la clave key, si no existe devuelve null.

<pre class="language-java"><code class="lang-java">Map&#x3C;String, Integer> prefixes = new HashMap&#x3C;>();
<strong>prefixes.put("ES", 340);
</strong><strong>prefixes.put("US", 1);
</strong>prefixes.put("UK", 44);
prefixes.put("ES", 34);

if(prefixes.containsKey("ES")) {
    // El método get devuleve un Integer porque en este mapa V es Integer
    Integer spainPrefix = prefixes.get("ES");
    System.out.println("El prefijo de España es " + spainPrefix);
}
</code></pre>

### int size()

Devuelve el tamaño del mapa

<pre class="language-java"><code class="lang-java">Map&#x3C;String, Integer> prefixes = new HashMap&#x3C;>();
<strong>prefixes.put("ES", 340);
</strong><strong>prefixes.put("US", 1);
</strong>prefixes.put("UK", 44);
prefixes.put("ES", 34);
System.out.println("Total prefijos " + prefixes.size());
</code></pre>

### V remove(K key)

Elimina el par clave-valor que tenga la clave key. Si la clave existía se devuelve el valor asociado a la misma, en caso de no existir devuelve null.

<pre class="language-java"><code class="lang-java">Map&#x3C;String, Integer> prefixes = new HashMap&#x3C;>();
<strong>prefixes.put("ES", 340);
</strong><strong>prefixes.put("US", 1);
</strong>prefixes.put("UK", 44);
prefixes.put("ES", 34);

<strong>int deletedValue = prefixes.remove("ES");
</strong>
System.out.println("Se ha eliminado la clave ES, cuyo valor era " + deletedValue);
</code></pre>

### boolean isEmpty()

Devuelve true si el mapa está vacío

### void clear()

Vacía el mapa

## Recorrer mapas

Existen varias formas de recorrer un mapa, dependiendo a qué valores queramos acceder

### Recorrer las claves

Es posible recorrer las claves de un mapa utilizando el método `keySet()` que devuelve un Set con las claves del mapa.

<pre class="language-java"><code class="lang-java">Map&#x3C;String, Integer> prefixes = new HashMap&#x3C;>();
<strong>prefixes.put("ES", 340);
</strong><strong>prefixes.put("US", 1);
</strong>prefixes.put("UK", 44);
prefixes.put("ES", 34);

for(String countryCode: prefixes.keySet()){
    System.out.println(countryCode);
}
</code></pre>

### Recorrer los valores

También es posible recorrer las valores de un mapa utilizando el método `values()` que devuelve una Collection con las claves del mapa.

<pre class="language-java"><code class="lang-java">Map&#x3C;String, Integer> prefixes = new HashMap&#x3C;>();
<strong>prefixes.put("ES", 340);
</strong><strong>prefixes.put("US", 1);
</strong>prefixes.put("UK", 44);
prefixes.put("ES", 34);

for(int prefix: prefixes.values()){
    System.out.println(prefix);
}
</code></pre>

### Recorrer los pares clave-valor

En algunas ocasiones, vamos a querer recorrer claves y valores al mismo tiempo. Para ello usaremos el método entrySet, dicho método devuelve un Set de Entry\<K,V>, cada objeto de tipo Entry continene una clave y un valor.

```java
Map<String, Integer> prefixes = new HashMap<>();
prefixes.put("ES", 340);
prefixes.put("US", 1);
prefixes.put("UK", 44);
prefixes.put("ES", 34);

for(var entry: prefixes.entrySet()){
    System.out.println(entry.getKey() + " -> " + entry.getValue());
}
```

## Implementaciones

Las dos implementaciones más importantes son TreeMap y HashMap, el funcionamiento interno de estas colecciones es similar al de TreeSet y HashSet, solo que añadiendo la parte asociativa, es decir los valores.

Normalmente los mapas se usan para indexar valores por una clave, por lo que la ordenación interna de las claves no es relevante. Debido a esto, la implementación que se utiliza en el 99% de los casos es HashMap, ya que es la más eficiente.

<figure><img src="../../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

Solo usaremos TreeMap cuando queramos que las claves sigan un orden determinado, algo poco habitual con este tipo de estructuras de datos.
