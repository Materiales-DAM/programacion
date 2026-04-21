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

# Recursión

**La recursión es una técnica en la que una función se llama a sí misma** para resolver un problema dividiéndolo en un problema más pequeño del mismo tipo. Suena abstracto, pero el patrón aparece por todas partes en la vida real.

Si abres un cajón y encuentras otro cajón dentro, y dentro de ese otro, y así sucesivamente, para "vaciar el cajón" tu procedimiento mental es: **vacío este cajón, y si encuentro otro dentro, aplico el mismo procedimiento a ese otro**. Eso es recursión: describir cómo se resuelve un problema apelando al mismo procedimiento sobre una versión más pequeña de sí mismo.

Matemáticamente la idea también resulta familiar. El factorial se define así:

```
0! = 1
n! = n · (n-1)!
```

Para calcular `5!` necesito saber `4!`. Para saber `4!` necesito `3!`. Y así hasta llegar a `0!`, que sé directamente que es `1`. Esa misma estructura —un caso trivial conocido y una regla que reduce un caso general a otro más simple— es la que vamos a traducir a código.

#### ¿Por qué aprender recursión?

Por tres motivos que se irán haciendo evidentes durante el curso:

Muchos problemas tienen una **estructura naturalmente recursiva**: recorrer directorios dentro de directorios, navegar árboles, dividir un problema por la mitad, generar todas las combinaciones posibles... En estos problemas, la solución iterativa existe pero resulta mucho más compleja que la recursiva.

La recursión es la base de técnicas de diseño algorítmico fundamentales, como **divide y vencerás** (que ya has visto o verás con _merge sort_), el _**backtracking**_ (resolver sudokus, laberintos) y la **programación dinámica**.

Entender la recursión **cambia tu forma de pensar sobre los problemas**. Te enseña a descomponer, a confiar en soluciones parciales, a razonar por inducción. Esa habilidad es transferible más allá de la programación.

### Los dos ingredientes de toda función recursiva

Una función recursiva bien diseñada tiene siempre dos partes:

**El caso base.** La situación más simple posible, tan simple que sabemos resolverla directamente **sin recursión**. Es lo que detiene la cadena de llamadas. Sin caso base, la función se llamaría a sí misma para siempre.

**El caso recursivo.** La regla que expresa el problema general en términos de una versión **más pequeña de sí mismo**. Es crucial que el "problema más pequeño" esté **más cerca del caso base**: si no, la recursión no termina.

La plantilla mental es siempre la misma:

```
función resolver(problema):
    si problema es trivial:
        devolver solución directa         ← caso base
    si no:
        reducir a un problema más pequeño
        resultado = resolver(problema más pequeño)   ← llamada recursiva
        combinar resultado y devolverlo   ← caso recursivo
```

Si interiorizas esta plantilla, la mitad del trabajo está hecho. Los errores al escribir funciones recursivas casi siempre son alguna de estas tres cosas: falta el caso base, el caso recursivo no reduce el problema, o la combinación del resultado está mal.

## Ejemplo guiado: el factorial

Vamos a traducir la definición matemática del factorial a Java, siguiendo la plantilla.

**Caso base:** `0! = 1`. Sabemos la respuesta directamente.

**Caso recursivo:** `n! = n · (n-1)!`. Para calcular `n!`, calculo primero `(n-1)!` (una versión más pequeña del mismo problema) y lo multiplico por `n`.

```java
public static long factorial(int n) {
    if (n == 0) {            // caso base
        return 1;
    }
    return n * factorial(n - 1);   // caso recursivo
}
```

Esta es toda la función. Cuatro líneas. Pero hay mucho que desempacar en ellas, así que veamos exactamente qué ocurre cuando la ejecutamos.

### La pila de llamadas: qué pasa por dentro

Cuando llamas a `factorial(6)`, el programa no sabe todavía el resultado. Antes de poder devolver 6 `* factorial(5)`, necesita el valor de `factorial(5)`. Así que **pausa** la ejecución de `factorial(6)` y empieza a ejecutar `factorial(5)`. Pero `factorial(5)` tampoco puede terminar sin saber `factorial(4)`, y así sucesivamente.

Java almacena cada llamada pausada en una estructura llamada **pila de llamadas** (_call stack_). Cada llamada a la función crea una nueva entrada en la pila con sus propias variables locales. Cuando una llamada devuelve un valor, se elimina de la pila y su resultado se entrega a la llamada que la invocó.

Visualmente, para `factorial(6)`:

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

Un detalle importante: **cada llamada tiene sus propias variables `n`**. Cuando estás dentro de `factorial(2)`, su `n` vale 2 y no se ve afectado por el `n=3` de la llamada que la invocó. Esta independencia de variables locales es lo que hace que la recursión funcione correctamente.

## Ejercicios

#### Ejercicio 1 — Suma de los N primeros naturales _(básico)_

Implementa recursivamente una función que calcule `1 + 2 + 3 + ... + n`.

```
sumaNaturales(0)  →  0
sumaNaturales(1)  →  1
sumaNaturales(5)  →  15   (1+2+3+4+5)
sumaNaturales(10) →  55
```

```java
public static int sumaNaturales(int n)
```

> _Pista:_ mismo patrón que el factorial. ¿Cuál es el caso base? ¿Cómo se reduce?
>
> _Reflexión después de resolverlo:_ escribe también la versión iterativa con un `for`. ¿Cuál es más clara en este caso? ¿Por qué?

***

#### Ejercicio 2 — Potencia _(básico)_

Calcula `xⁿ` recursivamente, para `n ≥ 0`.

```
potencia(2, 0)  →  1
potencia(2, 3)  →  8
potencia(5, 4)  →  625
potencia(3, 10) →  59049
```

```java
public static long potencia(int x, int n)
```

> _Pista:_ `x⁰ = 1`. Para el caso recursivo, recuerda la propiedad `xⁿ = x · xⁿ⁻¹`. Fíjate en un detalle: la reducción ocurre sobre `n`, no sobre `x`. Solo uno de los dos parámetros cambia en cada llamada.

***

#### Ejercicio 3 — Suma de dígitos _(medio)_

Calcula la suma de los dígitos de un número entero positivo.

```
sumaDigitos(0)     →  0
sumaDigitos(7)     →  7
sumaDigitos(123)   →  6    (1+2+3)
sumaDigitos(9999)  →  36
sumaDigitos(12345) →  15
```

```java
public static int sumaDigitos(int n)
```

> _Pista:_ aquí la reducción **no es `n - 1`**. Piensa: si `n = 123`, ¿cómo obtienes el último dígito?, ¿cómo obtienes el número que queda tras quitar ese último dígito? Una vez tengas estas dos operaciones, la recursión sale sola.
>
> Este ejercicio es importante porque rompe el patrón mental "reducir = restar 1". Hay muchas formas de hacer un problema más pequeño.

***

#### Ejercicio 4 — Invertir una cadena _(medio)_

Invierte una cadena usando recursión, sin usar bucles.

```
invertir("")      →  ""
invertir("a")     →  "a"
invertir("hola")  →  "aloh"
invertir("abcde") →  "edcba"
```

```java
public static String invertir(String s)
```

> _Pista:_ piensa "optimistamente": si alguien ya sabe invertir `"ola"` (y te da `"alo"`), ¿cómo usarías eso para invertir `"hola"`? La primera letra de la cadena original tiene que acabar al final del resultado.
>
> Usa `s.substring(1)` para obtener la cadena sin el primer carácter, y `s.charAt(0)` para obtener el primer carácter. Caso base: cadena de 0 o 1 caracteres (ya está "invertida" trivialmente).

***

#### Ejercicio 5 — Fibonacci _(medio-difícil)_

La sucesión de Fibonacci se define recursivamente:

```
fib(0) = 0
fib(1) = 1
fib(n) = fib(n-1) + fib(n-2)  para n ≥ 2
```

Los primeros términos son: 0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, ...

Implementa la función recursivamente.

```
fib(0)  →  0
fib(1)  →  1
fib(10) →  55
fib(20) →  6765
```

```java
public static long fib(int n)
```

> _Pista:_ necesitas **dos casos base** (para `n == 0` y `n == 1`) y **dos llamadas recursivas** en el caso general. Es la primera vez que ves esto: hasta ahora todas las funciones recursivas tenían una sola llamada.
>
> **Ejercicio adicional que no puedes saltarte:** ejecuta `fib(30)`, `fib(40)`, `fib(45)` y `fib(50)` midiendo el tiempo con `System.nanoTime()`. Verás que el tiempo se multiplica por 2 aproximadamente cada vez que `n` aumenta en 1. Esto se llama **coste exponencial**, y es catastrófico. Luego escribe una versión iterativa con un `for` y ejecuta `fib(50)`: tarda microsegundos. La recursión **puede ser desastrosa** si no se diseña con cuidado. Esta lección la vas a recordar siempre.

***

#### Ejercicio 6 — Palíndromo recursivo _(medio-difícil)_

Comprueba si una cadena es palíndromo (se lee igual de izquierda a derecha que de derecha a izquierda), usando recursión.

```
esPalindromo("")        →  true
esPalindromo("a")       →  true
esPalindromo("oso")     →  true
esPalindromo("radar")   →  true
esPalindromo("hola")    →  false
esPalindromo("anilina") →  true
```

```java
public static boolean esPalindromo(String s)
```

> _Pista:_ una cadena es palíndromo si el primer y último carácter coinciden **y** el resto de la cadena (quitando el primero y el último) también es palíndromo. Casos base: cadenas de 0 o 1 caracteres, que siempre son palíndromos.
>
> Fíjate cómo esta solución recursiva es prácticamente la definición matemática del problema, casi sin código intermedio. Por eso la recursión brilla aquí: captura la esencia sin ruido.

***

#### Ejercicio 7 — Torres de Hanói _(reto)_

Las **Torres de Hanói** son un rompecabezas clásico: tienes tres postes (A, B, C) y `n` discos de tamaños distintos apilados en el poste A en orden decreciente (el mayor abajo, el menor arriba). Debes moverlos todos al poste C respetando dos reglas:

1. No es posible mover más de un disco a la vez.
2. Un disco grande **nunca** puede reposar sobre uno más pequeño.

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

Implementa una función que imprima por pantalla la secuencia de movimientos necesarios para resolverlo.

```
hanoi(3, 'A', 'C', 'B');

Salida esperada:
Mover disco 1 de A a C
Mover disco 2 de A a B
Mover disco 1 de C a B
Mover disco 3 de A a C
Mover disco 1 de B a A
Mover disco 2 de B a C
Mover disco 1 de A a C
```

```java
public static void hanoi(int n, char origen, char destino, char auxiliar)
```

> _Pista:_ este es el problema donde la recursión brilla de verdad. Piénsalo con la mentalidad del paso 3 de la plantilla: **confía en que la recursión funciona**.
>
> Para mover `n` discos de A a C usando B como auxiliar:
>
> 1. Mueves los `n-1` discos de arriba desde A hasta B (usando C como auxiliar). _¿Cómo? No lo sabes, pero confías en la recursión._
> 2. Mueves el disco `n` (el más grande) directamente de A a C.
> 3. Mueves los `n-1` discos desde B hasta C (usando A como auxiliar). _Otra vez, confías en la recursión._
>
> Caso base: si `n == 0`, no hay nada que mover. (También puedes usar `n == 1` como caso base y mover ese disco directamente; ambas opciones son válidas).
>
> La solución cabe en **cinco líneas de código**. Si la encuentras, entenderás por qué mucha gente dice que descubrir la recursión cambia la forma de pensar.
