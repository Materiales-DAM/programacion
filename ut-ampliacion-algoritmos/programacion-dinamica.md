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

# Programación dinámica

## Programación dinámica

La **programación dinámica** (PD, o _dynamic programming_) es una técnica para resolver problemas que se descomponen en subproblemas **que se repiten**. La idea base es sencilla: si voy a tener que calcular lo mismo varias veces, lo calculo una sola vez y guardo el resultado.

No te dejes engañar por el nombre. "Programación dinámica" no tiene mucho que ver con "programación" en el sentido de escribir código, ni con "dinámico" en el sentido de cambiar en tiempo real. El término lo acuñó Richard Bellman en los años 50 buscando una etiqueta vendible a la administración militar estadounidense: "programación" sonaba a planificación, y "dinámica" sonaba bien. Lo lamentamos.

Lo importante es esto: si recuerdas el ejercicio 5 del capítulo de recursión, escribiste Fibonacci recursivamente y comprobaste que `fib(50)` se eternizaba. La razón era que la misma llamada se repetía cientos de millones de veces. **La programación dinámica es la cura para esa enfermedad.**

### 1. Los dos ingredientes de la programación dinámica

Un problema admite solución por PD cuando cumple dos condiciones:

**Subproblemas solapados.** El problema se descompone en subproblemas más pequeños del mismo tipo, y esos subproblemas **se repiten** entre sí. En Fibonacci, `fib(30)` aparece dentro de `fib(31)` y dentro de `fib(32)`, así que se calcula varias veces. Eso es solapamiento.

**Subestructura óptima.** La solución óptima del problema se puede construir a partir de las soluciones óptimas de sus subproblemas. Si conoces el camino más corto de A a Z y ese camino pasa por M, entonces la parte de A a M es necesariamente el camino más corto de A a M. Si fuera más largo, podrías sustituirlo y obtener uno más corto que el supuestamente óptimo: contradicción.

Conviene comparar la PD con divide y vencerás:

| Técnica               | Subproblemas | ¿Se solapan? |
| --------------------- | ------------ | ------------ |
| Divide y vencerás     | Sí           | **No**       |
| Programación dinámica | Sí           | **Sí**       |

En _merge sort_ divides el array por la mitad: las dos mitades son disjuntas, no comparten elementos. Cada subproblema se resuelve una sola vez de forma natural. Por eso _merge sort_ es divide y vencerás, no PD.

En Fibonacci las "mitades" `fib(n-1)` y `fib(n-2)` se solapan masivamente: `fib(n-1)` necesita `fib(n-2)` y `fib(n-3)`; `fib(n-2)` necesita `fib(n-3)` y `fib(n-4)`. Si no recordamos resultados, cada uno se recalcula desde cero. Por eso Fibonacci es candidato a PD.

### 2. Las dos formas: memoización y tabulación

Hay dos maneras de aplicar PD, y dan exactamente el mismo resultado. La elección es cuestión de estilo, claridad y, a veces, eficiencia.

**Memoización (**_**top-down**_**)**

Escribes la solución **recursiva** y le añades una caché: antes de calcular, miras si ya tienes el resultado guardado; si está, lo devuelves; si no, lo calculas y lo guardas. La estructura es idéntica a la recursión normal, pero con dos líneas extra.

Se llama _top-down_ porque empiezas por el problema grande y vas bajando hacia los subproblemas, igual que en la recursión normal.

**Tabulación (**_**bottom-up**_**)**

Identificas el orden en que necesitas calcular los subproblemas, creas una tabla (un array, una matriz) y la **rellenas iterativamente** desde los casos base hacia el problema final.

Se llama _bottom-up_ porque empiezas por los subproblemas pequeños y vas construyendo soluciones a partir de ellos.

| Aspecto                 | Memoización                           | Tabulación                     |
| ----------------------- | ------------------------------------- | ------------------------------ |
| Estructura              | Recursiva                             | Iterativa (bucles)             |
| Orden de cálculo        | Bajo demanda                          | Predeterminado                 |
| Coste de la pila        | O(profundidad)                        | O(1)                           |
| Cálculo de innecesarios | Evitado                               | A veces inevitable             |
| Comodidad               | Más natural si vienes de la recursión | Más fácil optimizar el espacio |

Empezar con memoización suele ser más cómodo: ya tienes la versión recursiva y solo añades la caché. Pasar a tabulación es un refinamiento posterior, útil cuando quieres reducir memoria o evitar desbordamientos de pila con entradas grandes.

### 3. Ejemplo guiado: Fibonacci, ahora bien hecho

Revisitemos el cálculo de Fibonacci. Recordatorio de la definición:

```
fib(0) = 0
fib(1) = 1
fib(n) = fib(n-1) + fib(n-2)   para n ≥ 2
```

**Versión naïve**

```java
public static long fib(int n) {
    if (n < 2) return n;
    return fib(n - 1) + fib(n - 2);
}
```

Coste **O(2ⁿ)**. `fib(50)` se cuelga.

**Por qué se cuelga: árbol de llamadas**

```
                  fib(5)
                /        \
           fib(4)          fib(3)
          /     \         /     \
       fib(3)  fib(2)   fib(2) fib(1)
       /   \    /  \     /  \
   fib(2) fib(1) ...   ...  ...
```

Fíjate: `fib(3)` aparece dos veces, `fib(2)` aparece tres veces, `fib(1)` cinco veces. Para `n = 50` el árbol tiene del orden de 2⁵⁰ hojas. **Más de un billón de llamadas para un problema que se resuelve con 50 sumas.**

**Versión con memoización**

Guardamos cada resultado calculado en un array. Antes de calcular, comprobamos si ya está.

```java
public static long fibMemo(int n) {
    long[] memo = new long[n + 1];
    Arrays.fill(memo, -1);   // -1 significa "aún no calculado"
    return fibMemoAux(n, memo);
}

private static long fibMemoAux(int n, long[] memo) {
    if (n < 2) return n;                  // caso base
    if (memo[n] != -1) return memo[n];    // ya calculado: devolverlo
    memo[n] = fibMemoAux(n - 1, memo) + fibMemoAux(n - 2, memo);
    return memo[n];
}
```

Traza con `n = 5`:

```
fibMemoAux(5)
├── fibMemoAux(4)
│   ├── fibMemoAux(3)
│   │   ├── fibMemoAux(2)
│   │   │   ├── fibMemoAux(1) → 1
│   │   │   └── fibMemoAux(0) → 0
│   │   │   memo[2] = 1
│   │   └── fibMemoAux(1) → 1
│   │   memo[3] = 2
│   └── fibMemoAux(2) → memo[2] = 1     ← ¡cache hit!
│   memo[4] = 3
└── fibMemoAux(3) → memo[3] = 2         ← ¡cache hit!
memo[5] = 5
```

Compáralo con el árbol exponencial de antes. Aquí cada `fib(k)` se calcula como mucho una vez; el resto son visitas a la caché. **Coste: O(n) en tiempo y O(n) en memoria** (el array `memo` más la pila de recursión).

**Versión con tabulación**

_Bottom-up_: para calcular `fib(n)` necesito `fib(n-1)` y `fib(n-2)`; para esos, los anteriores; y así hasta los casos base. Si los calculo en orden, nunca me faltará nada.

```java
public static long fibTab(int n) {
    if (n < 2) return n;
    long[] dp = new long[n + 1];
    dp[0] = 0;
    dp[1] = 1;
    for (int i = 2; i <= n; i++) {
        dp[i] = dp[i - 1] + dp[i - 2];
    }
    return dp[n];
}
```

Cuatro líneas en el núcleo. Esto es lo que habríamos querido escribir desde el principio.

**Coste: O(n) en tiempo, O(n) en memoria.** Sin recursión, sin pila.

**Optimización de espacio: O(1)**

Mira el bucle: para calcular `dp[i]` solo necesitas `dp[i-1]` y `dp[i-2]`. Todo lo demás es historia. Si no vas a consultar los anteriores, ¿para qué guardarlos?

```java
public static long fibOpt(int n) {
    if (n < 2) return n;
    long anterior = 0;
    long actual = 1;
    for (int i = 2; i <= n; i++) {
        long siguiente = anterior + actual;
        anterior = actual;
        actual = siguiente;
    }
    return actual;
}
```

**Coste: O(n) en tiempo, O(1) en memoria.** Lo más eficiente que se puede.

Esta técnica de "deslizar" solo las variables que necesitamos es muy frecuente en PD: empiezas con una tabla completa para entenderlo, luego te das cuenta de que solo necesitas las últimas `k` filas o columnas, y reduces la memoria a una fracción.

**Comparativa final para `n = 50`**

| Versión     | Tiempo  | Memoria   |
| ----------- | ------- | --------- |
| Recursiva   | minutos | O(n) pila |
| Memoización | < 1 ms  | O(n)      |
| Tabulación  | < 1 ms  | O(n)      |
| Optimizada  | < 1 ms  | O(1)      |

La diferencia entre la recursión naïve y cualquiera de las versiones PD son **miles de millones de veces más rápido**. Por eso la PD es una de las técnicas más útiles que vais a aprender.

### 4. Segundo ejemplo: subir escaleras

**El problema**: tienes una escalera con `n` escalones. En cada paso puedes subir **1 o 2 escalones**. ¿De cuántas formas distintas puedes llegar arriba?

```
formas(0) = 1   (estás arriba, no haces nada — una forma)
formas(1) = 1   (un paso de 1)
formas(2) = 2   (1+1, o 2)
formas(3) = 3   (1+1+1, 1+2, 2+1)
formas(4) = 5   (1+1+1+1, 1+1+2, 1+2+1, 2+1+1, 2+2)
formas(5) = 8
```

¿Te suena la secuencia? **1, 1, 2, 3, 5, 8, ...** Es Fibonacci. Pero antes de cantar victoria, intenta justificar **por qué** es Fibonacci.

**Razonamiento**

Pregúntate: ¿cómo es el **último paso** para llegar al escalón `n`?

* O bien diste un salto de 1 desde el escalón `n-1`. En ese caso, el número de formas de llegar a `n` por esta vía es exactamente el número de formas de llegar a `n-1`.
* O bien diste un salto de 2 desde el escalón `n-2`. En ese caso son las formas de llegar a `n-2`.

Como son las dos únicas opciones y son disjuntas, sumamos:

```
formas(n) = formas(n-1) + formas(n-2)
```

Casos base: `formas(0) = formas(1) = 1`.

Es Fibonacci con índices desplazados, sí, pero el ejercicio importante no era reconocer la secuencia: era **razonar sobre las decisiones**. Decisiones sobre el último paso, fijar casos base, sumar contribuciones de cada decisión. Este patrón es el corazón de la PD.

**Implementación**

```java
public static long formasSubir(int n) {
    if (n < 2) return 1;
    long[] dp = new long[n + 1];
    dp[0] = 1;
    dp[1] = 1;
    for (int i = 2; i <= n; i++) {
        dp[i] = dp[i - 1] + dp[i - 2];
    }
    return dp[n];
}
```

Idéntica a Fibonacci. La lección no es el código: es que **dos problemas aparentemente distintos comparten la misma estructura recursiva**. Identificar esa estructura es la habilidad clave.

### 5. Cambio de monedas: cuando greedy no basta

En el capítulo de algoritmos voraces viste que el problema del cambio "funciona" si el sistema de monedas está bien diseñado. Vamos a ver qué hacemos cuando no lo está.

**El problema**: dado un conjunto de denominaciones `monedas[]` y una cantidad `cantidad`, devuelve el **mínimo número de monedas** necesarias para sumar exactamente esa cantidad. Si es imposible, devuelve `-1`. Puedes usar cada moneda cuantas veces quieras.

```
monedas = [1, 2, 5],   cantidad = 11   →  3    (5 + 5 + 1)
monedas = [2],         cantidad = 3    →  -1   (imposible)
monedas = [1],         cantidad = 0    →  0
monedas = [1, 7, 10],  cantidad = 14   →  2    (7 + 7)
```

El último caso es la trampa: si vas tomando siempre la moneda más grande disponible (greedy), 14 = 10 + 1 + 1 + 1 + 1, cinco monedas. Pero 7 + 7 lo hace con dos. **Greedy falla.** Necesitamos algo más potente.

**Razonamiento**

Para hacer cambio de una cantidad `c`, considera todas las monedas que podrías usar **como última moneda**:

* Si uso la moneda `m`, me queda hacer cambio de `c - m`, y eso me cuesta `monedasMin(c - m)` monedas. Total: `1 + monedasMin(c - m)`.
* Pruebo con cada moneda y me quedo con el mínimo.

Formalmente:

```
monedasMin(0) = 0
monedasMin(c) = 1 + min{ monedasMin(c - m) : m en monedas, m ≤ c }
monedasMin(c) = ∞   si no hay ninguna m válida
```

**Implementación con tabulación**

```java
public static int monedasMin(int[] monedas, int cantidad) {
    int[] dp = new int[cantidad + 1];
    Arrays.fill(dp, Integer.MAX_VALUE);
    dp[0] = 0;   // caso base: 0 monedas para hacer 0

    for (int c = 1; c <= cantidad; c++) {
        for (int m : monedas) {
            if (m <= c && dp[c - m] != Integer.MAX_VALUE) {
                dp[c] = Math.min(dp[c], dp[c - m] + 1);
            }
        }
    }

    return dp[cantidad] == Integer.MAX_VALUE ? -1 : dp[cantidad];
}
```

**Traza con `monedas = [1, 2, 5]`, `cantidad = 11`**

```
dp[0]  = 0
dp[1]  = 1     (1)
dp[2]  = 1     (2)
dp[3]  = 2     (1+2)
dp[4]  = 2     (2+2)
dp[5]  = 1     (5)
dp[6]  = 2     (5+1)
dp[7]  = 2     (5+2)
dp[8]  = 3     (5+2+1)
dp[9]  = 3     (5+2+2)
dp[10] = 2     (5+5)
dp[11] = 3     (5+5+1)
```

Resultado: **3**.

**Coste: O(cantidad × |monedas|)** en tiempo, O(cantidad) en memoria.

Fíjate cómo se nota la **subestructura óptima**: para calcular `dp[11]` óptimamente, miramos a `dp[10]`, `dp[9]` y `dp[6]`, asumimos que cada uno ya está calculado de forma óptima, y construimos `dp[11]` a partir de ellos. Esa es la esencia.

### 6. La mochila 0/1: PD en dos dimensiones

Hasta ahora la PD se ha resuelto con un array unidimensional. Pasemos a un problema clásico que necesita dos.

**El problema**: tienes una mochila con capacidad `C` (en kg) y `n` objetos. Cada objeto `i` tiene un peso `w[i]` y un valor `v[i]`. Quieres meter en la mochila un subconjunto de objetos (puedes coger cada uno como mucho una vez, de ahí el "0/1") maximizando el valor total sin pasarte de capacidad.

**Por qué greedy falla aquí**

Tentación: ordenar por **ratio valor/peso** y coger codiciosamente. Pongamos:

```
Capacidad: 50 kg
Objetos:
  A: peso 10, valor 60   (ratio 6.0)
  B: peso 20, valor 100  (ratio 5.0)
  C: peso 30, valor 120  (ratio 4.0)
```

Greedy por ratio: cojo A (queda 40), cojo B (queda 20), C no cabe. Total: 30 kg, valor **160**.

Solución óptima: cojo B y C. Total: 50 kg, valor **220**.

Greedy se equivoca por **60**. El problema con la mochila 0/1 es que las decisiones interactúan: aceptar un objeto consume capacidad que ya no estará disponible para combinaciones potencialmente mejores. Greedy no contempla esa interacción. **PD sí.**

(Curiosidad: si los objetos pudieran trocearse —la _mochila fraccionaria_— sí se resuelve con greedy. Pero esa es otra historia.)

**Razonamiento**

Considera los objetos uno a uno. Para el objeto `i` con capacidad restante `c` tienes **dos opciones**:

* **No cogerlo.** Pasas al objeto `i-1` con la misma capacidad: `mochila(i-1, c)`.
* **Cogerlo** (solo si `w[i] ≤ c`). Sumas su valor y pasas al objeto `i-1` con capacidad reducida: `v[i] + mochila(i-1, c - w[i])`.

Eliges el mayor de los dos. Si `w[i] > c`, solo está la opción de no cogerlo.

Casos base: si `i < 0` (no quedan objetos) o `c == 0` (no queda capacidad), el valor es 0.

**El estado tiene dos dimensiones**

A diferencia de Fibonacci o el cambio de monedas, aquí el estado son **dos** variables: qué objeto estamos considerando y qué capacidad nos queda. Por eso necesitamos una **tabla 2D**: `dp[i][c]` = mejor valor usando los primeros `i` objetos con capacidad `c`.

```java
public static int mochila01(int[] pesos, int[] valores, int capacidad) {
    int n = pesos.length;
    int[][] dp = new int[n + 1][capacidad + 1];

    // Casos base: dp[0][c] = 0 (sin objetos) y dp[i][0] = 0 (sin capacidad)
    // ya están inicializados a 0 por Java.

    for (int i = 1; i <= n; i++) {
        for (int c = 0; c <= capacidad; c++) {
            // No coger el objeto i-1 (índice base 0 en los arrays)
            dp[i][c] = dp[i - 1][c];

            // Coger el objeto i-1, si cabe
            if (pesos[i - 1] <= c) {
                int cogerlo = dp[i - 1][c - pesos[i - 1]] + valores[i - 1];
                dp[i][c] = Math.max(dp[i][c], cogerlo);
            }
        }
    }

    return dp[n][capacidad];
}
```

**Traza con el ejemplo**

Objetos `A(10,60)`, `B(20,100)`, `C(30,120)`, capacidad `50`. Construyamos `dp`:

```
              c=0   c=10   c=20   c=30   c=40   c=50
i=0 (∅)        0     0      0      0      0      0
i=1 (A)        0    60     60     60     60     60
i=2 (A,B)      0    60     100    160    160    160
i=3 (A,B,C)    0    60     100    160    180    220
```

Resultado: `dp[3][50] = 220`. ✓

**Coste: O(n · C)** en tiempo y memoria, donde `n` es el número de objetos y `C` la capacidad. Esto se llama complejidad **pseudo-polinómica**: polinómica en los valores numéricos, pero exponencial en el número de bits necesarios para representarlos. Para `n = 100` y `C = 10⁹` la tabla es ingestionable. Pero para tamaños razonables, es perfectamente práctico.

### 7. Cómo abordar un problema nuevo de PD

Después de estos ejemplos podemos extraer un método.

**Paso 1: identifica el estado.** ¿Qué información necesitas para definir un subproblema? En Fibonacci es solo `n`. En la mochila son `(i, c)`. El estado define las dimensiones de tu tabla.

**Paso 2: escribe la recurrencia.** Expresa el resultado del estado actual en función de estados más pequeños. Suele ayudar pensar en la **última decisión**: el último escalón, la última moneda, el último objeto. Las opciones para esa última decisión son los términos de la recurrencia.

**Paso 3: define los casos base.** Los estados más pequeños donde la respuesta es directa. En Fibonacci, `fib(0)` y `fib(1)`. En la mochila, `i = 0` o `c = 0`.

**Paso 4: elige memoización o tabulación.** Empieza con memoización si vienes de la versión recursiva. Pasa a tabulación si necesitas más eficiencia o quieres evitar pila.

**Paso 5 (opcional): optimiza el espacio.** Si en tu recurrencia `dp[i]` solo depende de un puñado de filas anteriores, puedes guardar solo esas y reducir memoria.

Cuando te enfrentes a un problema que no sabes resolver, no busques "el código de la PD para esto" — eso no existe en general. Busca **el estado** y **la recurrencia**. Una vez los tienes, escribir el código es mecánico.

***

### 8. Ejercicios

**Ejercicio 1 — Tribonacci&#x20;**_**(básico)**_

La sucesión de Tribonacci se define así:

```
trib(0) = 0
trib(1) = 1
trib(2) = 1
trib(n) = trib(n-1) + trib(n-2) + trib(n-3)   para n ≥ 3
```

Implementa una versión tabulada con coste O(n) en tiempo y O(1) en memoria.

```
trib(0)  →  0
trib(1)  →  1
trib(4)  →  4    (0+1+1+2)
trib(10) →  149
trib(25) →  1389537
```

```java
public static long trib(int n)
```

> _Pista:_ la misma idea que Fibonacci optimizado, pero con tres variables deslizantes en vez de dos.

***

**Ejercicio 2 — Subir escaleras con pasos variables&#x20;**_**(básico)**_

Generaliza el problema de las escaleras: ahora puedes subir cualquier número de pasos del conjunto `pasos[]`. Calcula de cuántas formas distintas puedes llegar arriba.

```
formas(n=4, pasos=[1, 2])     →  5
formas(n=3, pasos=[1, 2, 3])  →  4    (1+1+1, 1+2, 2+1, 3)
formas(n=5, pasos=[1, 3, 5])  →  5
```

```java
public static long formasSubir(int n, int[] pasos)
```

> _Pista:_ la recurrencia pasa a ser `dp[i] = sum(dp[i - p] para p en pasos si p <= i)`. Sigue siendo PD unidimensional, simplemente con más términos en cada suma.

***

**Ejercicio 3 — El ladrón de casas&#x20;**_**(medio)**_

Un ladrón quiere robar en una calle con casas en línea. Cada casa `i` tiene una cantidad de dinero `dinero[i]`. La pega: si roba en dos casas **adyacentes**, salta la alarma. Calcula el máximo botín posible.

```
dinero = [2, 7, 9, 3, 1]   →  12   (casas 0, 2, 4: 2+9+1)
dinero = [1, 2, 3, 1]      →  4    (casas 0, 2: 1+3)
dinero = [5, 1, 1, 5]      →  10   (casas 0, 3)
dinero = []                →  0
```

```java
public static int maxBotin(int[] dinero)
```

> _Pista:_ para cada casa `i`, dos opciones: robarla (entonces el botín máximo es `dinero[i] + maxBotin(0..i-2)`) o no robarla (entonces es `maxBotin(0..i-1)`). Es decir, `dp[i] = max(dp[i-1], dp[i-2] + dinero[i])`. Casos base: `dp[0] = dinero[0]`, `dp[1] = max(dinero[0], dinero[1])`.
>
> Se puede optimizar a O(1) en memoria con dos variables deslizantes, como Fibonacci.

***

**Ejercicio 4 — Camino de coste mínimo en una matriz&#x20;**_**(medio)**_

Tienes una matriz `m × n` de enteros no negativos donde cada celda tiene un coste. Empiezas en la esquina superior izquierda `(0, 0)` y debes llegar a la inferior derecha `(m-1, n-1)`. En cada paso solo puedes moverte **a la derecha o hacia abajo**. Calcula el coste mínimo de la ruta.

```
matriz = [[1, 3, 1],
          [1, 5, 1],
          [4, 2, 1]]

Resultado: 7   (ruta 1 → 3 → 1 → 1 → 1)
```

```java
public static int costeMinimo(int[][] matriz)
```

> _Pista:_ aquí el estado tiene dos dimensiones, `(fila, columna)`. Para llegar a `(i, j)` debes venir de `(i-1, j)` (desde arriba) o de `(i, j-1)` (desde la izquierda), así que `dp[i][j] = matriz[i][j] + min(dp[i-1][j], dp[i][j-1])`. Casos base: primera fila y primera columna se acumulan en una sola dirección.

***

**Ejercicio 5 — Número de formas de hacer cambio&#x20;**_**(medio)**_

Variante del problema del tutorial. En vez de calcular el **mínimo** número de monedas, calcula **cuántas combinaciones distintas** hay para obtener exactamente la cantidad. Cada moneda puede usarse cuantas veces quieras.

```
monedas = [1, 2, 5],   cantidad = 5    →  4    ({5}, {2+2+1}, {2+1+1+1}, {1+1+1+1+1})
monedas = [2],         cantidad = 3    →  0
monedas = [10],        cantidad = 10   →  1
```

```java
public static int formasDeCambio(int[] monedas, int cantidad)
```

> _Pista:_ **muy importante**: el orden de los bucles afecta a si cuentas combinaciones (sin orden) o permutaciones (con orden). Para combinaciones, el bucle externo recorre las **monedas** y el interno las **cantidades**:
>
> ```java
> for (int m : monedas)
>     for (int c = m; c <= cantidad; c++)
>         dp[c] += dp[c - m];
> ```
>
> Empiezas con `dp[0] = 1` (una sola forma de hacer 0: no usar nada). Si inviertes los bucles contarás secuencias ordenadas y obtendrás más respuestas de las que debes. Es un error clásico de PD: no es lo mismo "cuántos conjuntos" que "cuántas secuencias".

***

**Ejercicio 6 — Subsecuencia común más larga (LCS)&#x20;**_**(medio-difícil)**_

Dadas dos cadenas `a` y `b`, encuentra la **longitud** de la subsecuencia común más larga (no necesariamente contigua). Una subsecuencia mantiene el orden relativo de los caracteres, pero pueden faltar caracteres intermedios.

```
lcs("abcde", "ace")        →  3   ("ace")
lcs("abc", "def")          →  0
lcs("AGGTAB", "GXTXAYB")   →  4   ("GTAB")
lcs("hola", "olas")        →  3   ("ola")
```

```java
public static int lcs(String a, String b)
```

> _Pista:_ PD 2D. Estado: `dp[i][j]` = LCS de los prefijos `a[0..i-1]` y `b[0..j-1]`. Recurrencia:
>
> * Si `a.charAt(i-1) == b.charAt(j-1)`: `dp[i][j] = dp[i-1][j-1] + 1` (extiende el match anterior).
> * Si no: `dp[i][j] = max(dp[i-1][j], dp[i][j-1])` (descarta un carácter de una de las dos).
>
> Casos base: `dp[0][j] = dp[i][0] = 0` (la subsecuencia con cadena vacía es vacía).
>
> Este es uno de los clásicos de PD. Es la base del comando `diff` en Linux y de muchos algoritmos de bioinformática para comparar secuencias de ADN.

***

**Ejercicio 7 — Partición en dos subconjuntos de igual suma&#x20;**_**(reto)**_

Dado un array de enteros positivos, determina si se puede particionar en dos subconjuntos con la **misma suma**.

```
puedeParticionar([1, 5, 11, 5])  →  true    ({1,5,5} y {11})
puedeParticionar([1, 2, 3, 5])   →  false
puedeParticionar([1, 2, 3])      →  true    ({3} y {1,2})
puedeParticionar([])             →  true    (dos subconjuntos vacíos)
```

```java
public static boolean puedeParticionar(int[] nums)
```

> _Pista:_ primer paso: si la suma total es impar, es imposible (no podrías repartirla en dos enteros iguales). Si es par, llama a esa mitad `objetivo = suma / 2`. El problema se reduce a: **¿se puede formar un subconjunto que sume exactamente `objetivo`?**
>
> Eso es la mochila 0/1 disfrazada. Estado: `dp[i][s]` = "se puede formar la suma `s` usando los primeros `i` elementos". Recurrencia: `dp[i][s] = dp[i-1][s] OR (s >= nums[i-1] AND dp[i-1][s - nums[i-1]])`. Caso base: `dp[i][0] = true` (suma 0 siempre se puede, con el subconjunto vacío).
>
> Es un clásico de entrevistas técnicas (LeetCode #416). Si lo resuelves, has entendido cómo reducir un problema aparentemente distinto a la mochila.

***

Con esto tenéis lo necesario para reconocer y atacar problemas de PD: dos ingredientes (solapamiento y subestructura óptima), dos formas (memoización y tabulación) y un método de cinco pasos para diseñar la solución. Como en recursión, la primera vez es la más difícil. A partir del tercer o cuarto problema, empiezas a ver el patrón antes de leer el enunciado entero.
