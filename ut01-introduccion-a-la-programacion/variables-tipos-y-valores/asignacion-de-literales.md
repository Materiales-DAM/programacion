---
cover: ../../.gitbook/assets/java.jpeg
coverY: 0
---

# Asignación de literales

Como su nombre indica, el valor de una variable puede cambiar a lo largo del programa. Para cambiarlo se necesita usar una sentencia de asignación.

Es posible asignarle un **valor literal** a la variable en la misma sentencia en la que se declara. Esto se denomina **inline initialization**. Los valores literales aparecen explicitamente en el código.

```java
// En esta sentencia se declara la variable myNumber y se inicializa asignándole 
// el valor literal 3
int myNumber = 3;
```

También es posible separar la declaración y la inicialización en dos sentencias:

```java
// Se declara la variable myNumber
int myNumber;
// Se inicializa la variable myNumber asignándole el valor literal 3
myNumber = 3;
```

El valor de una variable se puede modificar tantas veces como se desee a lo largo del programa, simplemente se deben realizar nuevas asignaciones de valores.

```java
// Se declara la variable myNumber
int myNumber;
// Se inicializa con el valor literal 3
myNumber = 3;

System.out.println(myNumber);

// Se le asigna el valor literal 5 a la variable myNumber, a partir de aquí deja
// de tener el valor 3
myNumber = 5;
System.out.println(myNumber);

// ¿Qué saldrá impreso en pantalla al ejecutar estas sentencias?
```

#### Literales numéricos enteros

```java
// Un literal de tipo int se expresa simplemente escribiendo el número
int myInt = 4;
// Para escribir un literal de tipo long podemos añadir una L al final
long myLong = -6444L;
```

#### Literales de números reales en coma flotante

```java
// Un literal de tipo float. Se puede añadir una f al final para aclarar el tipo.
float myFloat = 4.34f;
// Un literal de tipo double. Se puede añadir una d al final para aclarar el tipo.
double myDouble = 432.34d;
```

#### Literales de caracteres

<pre class="language-java"><code class="lang-java"><strong>// Los literales de tipo char se ponen entre comillas simples
</strong>char myChar = 'a';
</code></pre>

#### Literales de cadenas de caracteres

<pre class="language-java"><code class="lang-java"><strong>// Los literales de tipo String se ponen entre comillas dobles
</strong>String myString =  "Esto es un literal de String";
</code></pre>

#### Literales de boolean

<pre class="language-java"><code class="lang-java"><strong>// Los literales de tipo boolean pueden ser true o false
</strong>boolean myBoolean1 = true;
</code></pre>
