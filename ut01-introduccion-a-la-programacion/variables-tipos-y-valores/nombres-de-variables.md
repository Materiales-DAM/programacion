# Nombres de variables

Aunque los nombres de las variables se pueden establecer de manera más o menos libre, es conveniente seguir las convenciones de nombrado establecidas en cada lenguajes. De esta forma conseguiremos que el código sea más legible.

Las restricciones principales a la hora de darle nombre a una variable son:

* No puede haber espacios
* Solo se permiten caracteres alfanuméricos (letras y números) y los símbolos `$` y `_` ​
* El primer carácter no puede ser un número​
* No se puede usar como identificador una [palabra reservada de Java](https://www.w3schools.com/java/java\_ref\_keywords.asp) (existen 53 palabras reservadas como `public`, `class`, `static`...)​

La convención de nombres de variable en Java se llama [lower camel case](https://es.wikipedia.org/wiki/Camel\_case). Según esta convención los nombres de las variables deben empezar por minúscula y sólo se utilizará la mayúscula para marcar el inicio de una palabra. Además, los nombres deben estar en inglés. Los programas no dejarán de funcionar por no seguir estas normas pero su legibilidad empeorará.​

Algunos nombres de ejemplo

<pre class="language-java"><code class="lang-java"><strong>// El nombre de esta varialbe es "my number" que en lower camel case es
</strong>int myNumber = 3;
// Cuando el nombre de una variable es una soloa palabra se escribe todo en minúsculas
int number = 2;
// Cuantas más palabras, más mayúsculas
int myOtherNumber = 5;
</code></pre>





