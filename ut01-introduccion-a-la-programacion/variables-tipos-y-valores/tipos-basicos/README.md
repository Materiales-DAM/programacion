---
hidden: true
cover: ../../../.gitbook/assets/java.jpeg
coverY: 0
---

# Tipos básicos

Según Wikipedia "En [ciencias de la computación](https://es.wikipedia.org/wiki/Ciencias\_de\_la\_computaci%C3%B3n), un tipo de dato informático o simplemente tipo, es un atributo de los datos que indica al ordenador (y/o al [programador/programadora](https://es.wikipedia.org/wiki/Programador)) sobre la clase de datos que se va a manejar. Esto incluye imponer restricciones en los datos, como qué valores pueden tomar y qué operaciones se pueden realizar."​

La siguiente tabla contiene los conocidos como tipos primitivos de Java

<table><thead><tr><th width="130.33333333333331">Tipo</th><th width="100">Tamaño</th><th>Descripción</th></tr></thead><tbody><tr><td><code>byte</code></td><td>1 byte</td><td>Almacena enteros entre -128 y 127</td></tr><tr><td><code>short</code></td><td>2 bytes</td><td>Almacena enteros entre -32,768 y 32,767</td></tr><tr><td><code>int</code></td><td>4 bytes</td><td>Almacena enteros entre -2,147,483,648 y 2,147,483,647</td></tr><tr><td><code>long</code></td><td>8 bytes</td><td>Almacena enteros entre -9,223,372,036,854,775,808 y 9,223,372,036,854,775,807</td></tr><tr><td><code>float</code></td><td>4 bytes</td><td>Almacena número con decimales. Permite almacenar con precisiones mínimas de 6 a 7 digitos decimales.</td></tr><tr><td><code>double</code></td><td>8 bytes</td><td>Almacena número con decimales. Permite almacenar con precisiones mínimas de 15 digitos decimales.</td></tr><tr><td><code>boolean</code></td><td>1 bit</td><td>Almacena valores booleanos (true o false)</td></tr><tr><td><code>char</code></td><td>2 bytes</td><td>Almacena un caracter ASCII</td></tr></tbody></table>

Otro tipo básico en Java es `String`, este tipo nos permite almacenar cadenas de caracteres. Para definir un valor de tipo String usaremos las comillas dobles (`"texto"`) alrededor del texto que se quiera crear.

```java
String sentence = "Este texto se almacena en la variable sentence";
// ¿Qué aparecerá en pantalla?
System.out.println(sentence);
```

Haz click [aquí](https://www.w3schools.com/java/exercise.asp?filename=exercise\_data\_types1) para hacer unos ejercicios de tipos.
