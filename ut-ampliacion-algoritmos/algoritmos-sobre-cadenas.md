---
cover: ../.gitbook/assets/algorithm.jpg
coverY: 3.437014262938337
layout:
  width: default
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
  metadata:
    visible: true
  tags:
    visible: true
---

# Algoritmos sobre cadenas

### 1. ¿Por qué un bloque dedicado a cadenas?

Las cadenas de texto (_strings_) son el tipo de dato más omnipresente en la programación del mundo real. Formularios, bases de datos, logs, archivos de configuración, protocolos de red, URLs, JSON, XML, correos electrónicos, contraseñas... todo son cadenas. La mayor parte del código que escribirás en tu carrera profesional procesará texto de una forma u otra.

Desde el punto de vista algorítmico, las cadenas son esencialmente **arrays de caracteres**, así que todas las técnicas que ya conocéis (recorridos, dos punteros, ventana deslizante, fuerza bruta) se aplican directamente. Lo que cambia es el **vocabulario de operaciones**: en lugar de sumar o comparar números, trabajamos con caracteres, subcadenas, posiciones y frecuencias.

#### Lo que necesitas saber de `String` en Java antes de empezar

Java trata los strings como **objetos inmutables**: una vez creado un `String`, no puedes modificar sus caracteres. Cada operación que "cambia" una cadena en realidad crea una nueva. Esto tiene consecuencias de rendimiento que veremos, pero por ahora basta con conocer los métodos básicos:

| Método                  | Qué hace                                 | Ejemplo                                      |
| ----------------------- | ---------------------------------------- | -------------------------------------------- |
| `s.length()`            | Longitud de la cadena                    | `"hola".length()` → `4`                      |
| `s.charAt(i)`           | Carácter en la posición `i`              | `"hola".charAt(1)` → `'o'`                   |
| `s.substring(ini, fin)` | Subcadena desde `ini` hasta `fin-1`      | `"hola".substring(1, 3)` → `"ol"`            |
| `s.toCharArray()`       | Convierte a `char[]`                     | `"hola".toCharArray()` → `{'h','o','l','a'}` |
| `s.toLowerCase()`       | Pasa a minúsculas                        | `"Hola".toLowerCase()` → `"hola"`            |
| `s.equals(t)`           | Compara contenido                        | `"ab".equals("ab")` → `true`                 |
| `s.compareTo(t)`        | Orden lexicográfico                      | `"abc".compareTo("abd")` → negativo          |
| `s.indexOf(sub)`        | Posición de la primera aparición         | `"hola mundo".indexOf("mun")` → `5`          |
| `s.trim()`              | Elimina espacios al principio y al final | `" hola ".trim()` → `"hola"`                 |

Un apunte importante: **nunca compares strings con `==`**. El operador `==` compara referencias (si son el mismo objeto en memoria), no contenido. Usa siempre `.equals()`.

### 2. Recorrido de una cadena carácter a carácter

Antes de atacar problemas más sofisticados, el patrón fundamental es recorrer cada carácter. Es el equivalente al `for` sobre un array:

```java
for (int i = 0; i < s.length(); i++) {
    char c = s.charAt(i);
    // hacer algo con c
}
```

O, si prefieres trabajar con un array de caracteres:

```java
char[] chars = s.toCharArray();
for (char c : chars) {
    // hacer algo con c
}
```

La primera forma permite trabajar con los **índices** (necesario para dos punteros, ventana deslizante, etc.). La segunda es más limpia cuando solo necesitas los caracteres sin posiciones.

### 3. Ejemplo guiado: contar vocales

**Problema**: dada una cadena, contar cuántas vocales (a, e, i, o, u) contiene, sin distinguir mayúsculas de minúsculas.

```
contarVocales("Hola Mundo")  →  4  (o, a, u, o)
contarVocales("xyz")         →  0
contarVocales("aEiOu")       →  5
```

#### Implementación

```java
public static int contarVocales(String s) {
    int contador = 0;
    String vocales = "aeiouAEIOUáéíóúÁÉÍÓÚ";

    for (int i = 0; i < s.length(); i++) {
        if (vocales.indexOf(s.charAt(i)) != -1) {
            contador++;
        }
    }

    return contador;
}
```

Nada nuevo algorítmicamente: es el patrón "inicializar acumulador → recorrer → actualizar" que ya conocéis de los arrays numéricos. La única novedad es cómo comprobar si un carácter pertenece a un conjunto: usamos `indexOf` sobre una cadena que contiene todas las vocales posibles.

Un detalle de robustez: hemos incluido las vocales con tilde. En un contexto real con texto en español, olvidar las tildes es un error frecuente.

### 4. Invertir una cadena

**Problema**: dada una cadena, devolver una nueva cadena con los caracteres en orden inverso.

```
invertir("hola")    →  "aloh"
invertir("abcde")   →  "edcba"
invertir("a")       →  "a"
invertir("")        →  ""
```

#### Versión con `StringBuilder`

```java
public static String invertir(String s) {
    StringBuilder sb = new StringBuilder();
    for (int i = s.length() - 1; i >= 0; i--) {
        sb.append(s.charAt(i));
    }
    return sb.toString();
}
```

#### ¿Por qué `StringBuilder` y no concatenar con `+`?

En Java, cada vez que escribes `resultado = resultado + c`, se crea un nuevo objeto `String` en memoria, se copia todo el contenido anterior y se añade el carácter nuevo. Para una cadena de `n` caracteres, eso son `n` copias de tamaño creciente: coste total **O(n²)**.

`StringBuilder` usa internamente un buffer redimensionable (como un `ArrayList`), así que `append` es O(1) amortizado. El coste total pasa a **O(n)**.

Esta diferencia no importa con cadenas de 10 caracteres, pero con cadenas de 100 000 caracteres la versión con `+` puede tardar varios segundos mientras que `StringBuilder` es instantáneo. **Regla práctica: si construyes una cadena dentro de un bucle, usa `StringBuilder`**.

#### Versión con dos punteros (in-place sobre char\[])

```java
public static String invertirConPunteros(String s) {
    char[] chars = s.toCharArray();
    int izq = 0;
    int der = chars.length - 1;

    while (izq < der) {
        char tmp = chars[izq];
        chars[izq] = chars[der];
        chars[der] = tmp;
        izq++;
        der--;
    }

    return new String(chars);
}
```

Aquí aparece la **técnica de la pinza** (dos punteros convergentes) que ya conocéis de los arrays. El `String` de Java es inmutable, así que convertimos a `char[]`, invertimos in-place, y reconstruimos el `String`. Es O(n) en tiempo y O(n) en espacio (por la copia a `char[]`).

### 5. Comprobar si una cadena es palíndromo

**Problema**: determinar si una cadena se lee igual de izquierda a derecha que de derecha a izquierda. Ignoramos mayúsculas, tildes y caracteres no alfabéticos.

```
esPalindromo("Ana")                    →  true
esPalindromo("Anilina")                →  true
esPalindromo("A man a plan a canal Panama")  →  true
esPalindromo("hola")                   →  false
esPalindromo("Dábale arroz a la zorra el abad")  →  true
```

#### Solución con dos punteros

La idea es elegante: un puntero al principio y otro al final. Si ambos caracteres coinciden (ignorando mayúsculas y no-letras), avanzan hacia el centro. Si en algún momento difieren, no es palíndromo.

```java
public static boolean esPalindromo(String s) {
    s = s.toLowerCase();
    int izq = 0;
    int der = s.length() - 1;

    while (izq < der) {
        // Saltar caracteres que no sean letras
        while (izq < der && !Character.isLetter(s.charAt(izq))) izq++;
        while (izq < der && !Character.isLetter(s.charAt(der))) der--;

        if (s.charAt(izq) != s.charAt(der)) {
            return false;
        }

        izq++;
        der--;
    }

    return true;
}
```

Dos detalles importantes:

* `Character.isLetter()` descarta espacios, signos de puntuación y cualquier otro carácter no alfabético. Así "A man a plan a canal Panama" se reduce a "amanaplanacanalpanama", que es palíndromo.
* Primero convertimos toda la cadena a minúsculas con `toLowerCase()` para no tener que comparar con doble condición en cada paso.

#### Complejidad

**O(n)** en tiempo (cada carácter se examina como mucho una vez por cada puntero). **O(n)** en espacio (por la copia que hace `toLowerCase`; si quisiéramos O(1) en espacio, compararíamos con `Character.toLowerCase()` carácter a carácter sin crear la copia).

### 6. Comprobar si dos cadenas son anagramas

**Problema**: dos cadenas son **anagramas** si contienen exactamente los mismos caracteres con las mismas frecuencias, sin importar el orden. Ejemplo: "listen" y "silent", "roma" y "amor".

```
sonAnagramas("listen", "silent")  →  true
sonAnagramas("roma", "amor")      →  true
sonAnagramas("hola", "hole")      →  false
sonAnagramas("aab", "abb")        →  false
```

#### Solución 1 — Ordenar y comparar

Si dos cadenas son anagramas, al ordenar sus caracteres ambas producen la misma cadena:

```java
public static boolean sonAnagramasOrdenando(String a, String b) {
    if (a.length() != b.length()) return false;

    char[] charsA = a.toLowerCase().toCharArray();
    char[] charsB = b.toLowerCase().toCharArray();
    Arrays.sort(charsA);
    Arrays.sort(charsB);

    return Arrays.equals(charsA, charsB);
}
```

Complejidad: **O(n log n)** por la ordenación. Es la solución más intuitiva.

#### Solución 2 — Conteo de frecuencias

Contamos cuántas veces aparece cada carácter en cada cadena y comparamos los conteos:

```java
public static boolean sonAnagramasFrecuencias(String a, String b) {
    if (a.length() != b.length()) return false;

    int[] frecuencias = new int[256];   // tabla para cada carácter ASCII

    for (char c : a.toLowerCase().toCharArray()) frecuencias[c]++;
    for (char c : b.toLowerCase().toCharArray()) frecuencias[c]--;

    for (int f : frecuencias) {
        if (f != 0) return false;
    }

    return true;
}
```

El truco es usar **un solo array**: sumamos para la primera cadena y restamos para la segunda. Si al final todo es cero, las frecuencias coinciden exactamente.

Complejidad: **O(n)**, mejor que la versión con ordenación. Este patrón de **conteo de frecuencias** es una técnica reutilizable que aparece en muchos otros problemas de cadenas.

### 7. Búsqueda de subcadena por fuerza bruta

**Problema**: dada una cadena `texto` y una cadena `patron`, encontrar la posición de la primera aparición de `patron` dentro de `texto`, o `-1` si no aparece. Es lo que hace internamente `texto.indexOf(patron)`.

```
buscar("hola mundo cruel", "mundo")  →  5
buscar("abcabcabc", "cab")          →  2
buscar("aaaa", "aab")               →  -1
buscar("abc", "abcd")               →  -1
```

#### La idea

Probamos **todas las posiciones posibles** del texto donde podría empezar el patrón. En cada posición, comparamos carácter a carácter. Si en algún punto difieren, pasamos a la siguiente posición. Si coinciden todos, hemos encontrado la aparición.

#### Traza con texto = `"ABCABDA"`, patrón = `"ABD"`

| Posición | Comparaciones | Resultado                    |
| -------- | ------------- | ---------------------------- |
| 0        | A=A, B=B, C≠D | No coincide                  |
| 1        | B≠A           | No coincide                  |
| 2        | C≠A           | No coincide                  |
| 3        | A=A, B=B, D=D | **Encontrado en posición 3** |

#### Implementación

```java
public static int buscarSubcadena(String texto, String patron) {
    int n = texto.length();
    int m = patron.length();

    if (m > n) return -1;

    for (int i = 0; i <= n - m; i++) {          // cada posición de inicio posible
        int j = 0;
        while (j < m && texto.charAt(i + j) == patron.charAt(j)) {
            j++;                                 // avanzar mientras coincidan
        }
        if (j == m) {                            // ¿coincidieron todos?
            return i;
        }
    }

    return -1;
}
```

#### Complejidad

**Peor caso: O(n·m)**, donde `n` es la longitud del texto y `m` la del patrón. Ocurre cuando hay muchas coincidencias parciales que fallan al final, como buscar `"AAAB"` en `"AAAAAAAAAA"`.

**Caso medio: O(n)**, porque la mayoría de las comparaciones fallan en los primeros caracteres y no llegan a recorrer todo el patrón.

Existen algoritmos más eficientes (KMP, Boyer-Moore, Rabin-Karp) que garantizan O(n+m) incluso en el peor caso, pero su complejidad de implementación los deja fuera de 1º. La fuerza bruta es la referencia: saber que existe y entender por qué es O(n·m) es suficiente para este nivel.

### 8. Contar palabras en una frase

**Problema**: contar el número de palabras en una cadena, donde las palabras están separadas por uno o más espacios, y puede haber espacios al principio y al final.

```
contarPalabras("hola mundo")        →  2
contarPalabras("  hola   mundo  ")  →  2
contarPalabras("")                  →  0
contarPalabras("   ")              →  0
contarPalabras("una")              →  1
```

#### Solución con recorrido manual

En lugar de usar `split` (que oculta la lógica), vamos a resolverlo recorriendo la cadena. La idea: contamos una palabra cada vez que **entramos** en una secuencia de caracteres no-espacio.

```java
public static int contarPalabras(String s) {
    int contador = 0;
    boolean dentroDepalabra = false;

    for (int i = 0; i < s.length(); i++) {
        if (s.charAt(i) != ' ') {
            if (!dentroDepalabra) {
                contador++;                // empieza una palabra nueva
                dentroDepalabra = true;
            }
        } else {
            dentroDepalabra = false;       // hemos salido de la palabra
        }
    }

    return contador;
}
```

El flag `dentroDepalabra` actúa como una máquina de estados con dos estados: "dentro" y "fuera" de una palabra. Solo contamos cuando la transición es de "fuera" a "dentro". Este patrón de **máquina de estados simple** aparece en muchos problemas de procesamiento de texto.

### 9. Resumen de patrones

A lo largo de este tutorial han aparecido varios patrones reutilizables. Conviene tenerlos identificados:

| Patrón                           | Descripción                                                  | Ejemplo                           |
| -------------------------------- | ------------------------------------------------------------ | --------------------------------- |
| **Recorrido lineal**             | Recorrer carácter a carácter con un acumulador               | Contar vocales                    |
| **Dos punteros convergentes**    | Un puntero al inicio, otro al final, avanzan hacia el centro | Palíndromo, invertir cadena       |
| **Conteo de frecuencias**        | Array o mapa con la frecuencia de cada carácter              | Anagramas                         |
| **Fuerza bruta con ventana**     | Probar cada posición de inicio y verificar una subcadena     | Búsqueda de subcadena             |
| **Máquina de estados**           | Un flag o variable que indica en qué "estado" estamos        | Contar palabras                   |
| **StringBuilder para construir** | Buffer para construir cadenas sin coste cuadrático           | Invertir cadena, transformaciones |

Estos seis patrones cubren la inmensa mayoría de los problemas de cadenas de 1º DAM. Cuando te enfrentes a un problema nuevo, pregúntate cuál de estos patrones encaja.

***

### 10. Ejercicios

#### Ejercicio 1 — Contar consonantes _(básico)_

Dada una cadena, cuenta cuántas consonantes contiene (letras que no son vocales), sin distinguir mayúsculas de minúsculas. Los caracteres no alfabéticos (espacios, números, signos) no cuentan como consonantes.

```
contarConsonantes("Hola Mundo")  →  4  (H, l, M, n, d)... 5
contarConsonantes("aeiou")       →  0
contarConsonantes("xyz 123")     →  3
```

**Firma:**

```java
public static int contarConsonantes(String s)
```

> _Pista:_ un carácter es consonante si es letra (`Character.isLetter`) pero NO es vocal. Puedes reutilizar la lógica de contar vocales invirtiendo la condición.

***

#### Ejercicio 2 — Primera letra mayúscula de cada palabra _(básico)_

Dada una cadena, devuelve una nueva cadena donde la primera letra de cada palabra está en mayúscula y el resto en minúscula.

```
capitalizar("hola mundo cruel")       →  "Hola Mundo Cruel"
capitalizar("  juan   garcía  lópez") →  "  Juan   García  López"
capitalizar("YA ESTOY EN MAYÚSCULAS") →  "Ya Estoy En Mayúsculas"
capitalizar("a")                      →  "A"
```

**Firma:**

```java
public static String capitalizar(String s)
```

> _Pista:_ usa `StringBuilder`. Recorre la cadena llevando un flag `inicioDepalabra` (similar al patrón de máquina de estados de contar palabras). Cuando detectas que empieza una palabra, conviertes ese carácter a mayúscula; el resto va en minúscula.

***

#### Ejercicio 3 — Comprimir cadena _(medio)_

Implementa una compresión básica por conteo de caracteres consecutivos (_run-length encoding_). Si un carácter aparece consecutivamente `n` veces, se reemplaza por el carácter seguido de `n`. Si la cadena comprimida **no es más corta** que la original, devuelve la original.

```
comprimir("aabcccccaaa")  →  "a2b1c5a3"
comprimir("abcde")        →  "abcde"       (comprimida sería "a1b1c1d1e1", más larga)
comprimir("aaaa")         →  "a4"
comprimir("aabb")         →  "a2b2"        (misma longitud → devuelve original "aabb")
```

**Firma:**

```java
public static String comprimir(String s)
```

> _Pista:_ recorre la cadena con un índice `i` y un contador. Mientras `s.charAt(i) == s.charAt(i+1)`, incrementa el contador. Cuando el carácter cambie, escribe el carácter y el contador en un `StringBuilder`. Al final, compara longitudes y devuelve la más corta.

***

#### Ejercicio 4 — ¿Es rotación? _(medio)_

Dadas dos cadenas `a` y `b`, determina si `b` es una **rotación** de `a`. Una rotación es mover uno o más caracteres del principio al final (o viceversa). Por ejemplo, `"bcdea"` es una rotación de `"abcde"`.

```
esRotacion("abcde", "bcdea")       →  true   (rotación de 1 posición)
esRotacion("abcde", "cdeab")       →  true   (rotación de 2 posiciones)
esRotacion("abcde", "abced")       →  false
esRotacion("abc", "abc")           →  true   (rotación de 0 posiciones)
esRotacion("a", "a")               →  true
```

**Firma:**

```java
public static boolean esRotacion(String a, String b)
```

> _Pista:_ hay una solución elegante en una línea (más las comprobaciones de longitud). Piénsalo así: si concatenas `a` consigo misma (`a + a`), todas las posibles rotaciones de `a` aparecen como subcadenas de esa concatenación. Entonces, `b` es rotación de `a` si y solo si `a.length() == b.length()` y `(a + a).contains(b)`.
>
> Antes de usar esa solución, intenta resolverlo también con un bucle que pruebe cada punto de rotación posible. Es más largo pero te obliga a pensar en la mecánica.

***

#### Ejercicio 5 — Primer carácter no repetido _(medio)_

Dada una cadena, encuentra el **primer carácter que no se repite** y devuelve su índice. Si todos se repiten, devuelve `-1`.

```
primerUnico("abacabad")    →  4  (la primera 'c')
primerUnico("abab")        →  -1
primerUnico("aabbc")       →  4  (la 'c')
primerUnico("a")           →  0
primerUnico("aabbccdde")   →  8  (la 'e')
```

**Firma:**

```java
public static int primerUnico(String s)
```

> _Pista:_ usa el patrón de **conteo de frecuencias**. Primer paso: recorre la cadena y cuenta la frecuencia de cada carácter en un `int[256]` (o un `HashMap<Character, Integer>`). Segundo paso: recorre la cadena otra vez y devuelve el índice del primer carácter cuya frecuencia sea 1. Son dos pasadas O(n) → total O(n).

***

#### Ejercicio 6 — Cifrado César _(reto)_

El **cifrado César** es un cifrado clásico que desplaza cada letra un número fijo de posiciones en el alfabeto. Por ejemplo, con desplazamiento 3: A→D, B→E, ..., X→A, Y→B, Z→C. Los caracteres no alfabéticos se dejan tal cual.

Implementa las funciones de **cifrar** y **descifrar**.

```
cifrar("Hola Mundo", 3)       →  "Krod Pxqgr"
descifrar("Krod Pxqgr", 3)    →  "Hola Mundo"
cifrar("XYZ xyz", 3)          →  "ABC abc"     (el desplazamiento da la vuelta)
cifrar("abc", 26)              →  "abc"         (vuelta completa)
```

**Firmas:**

```java
public static String cifrarCesar(String s, int desplazamiento)
public static String descifrarCesar(String s, int desplazamiento)
```

> _Pista:_ para cada carácter que sea letra, calcula su nueva posición con aritmética modular. Si es minúscula: `char cifrado = (char) ('a' + (c - 'a' + desplazamiento) % 26)`. Análogo para mayúsculas con `'A'`. Los demás caracteres pasan sin cambiar. Descifrar es cifrar con desplazamiento `26 - desplazamiento` (o equivalentemente, con `-desplazamiento`).
>
> Ojo con desplazamientos negativos: en Java, el operador `%` puede devolver negativos. Para evitar problemas usa `((c - 'a' + desplazamiento) % 26 + 26) % 26`.

###
