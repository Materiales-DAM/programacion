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

# Divide y vencerás (Divide & conquer)

**Divide y vencerás** (_divide and conquer_) es una estrategia general para diseñar algoritmos. La idea es engañosamente simple: si un problema es demasiado grande para resolverlo directamente, **pártelo en trozos más pequeños**, resuelve cada trozo **por separado** y luego **junta las soluciones parciales** para obtener la solución del problema original.

La estrategia tiene tres fases:

1. **Dividir**: partir el problema en subproblemas más pequeños del mismo tipo.
2. **Vencer**: resolver cada subproblema. Si aún es demasiado grande, volver a dividir (aquí entra la **recursión**). Cuando el subproblema es trivial, resolverlo directamente: ese es el **caso base**.
3. **Combinar**: juntar las soluciones de los subproblemas para construir la solución del problema original.

Es un paradigma muy potente: la búsqueda binaria, _merge sort_, _quicksort_ y muchos otros algoritmos fundamentales lo usan. Pero antes de verlos, vamos a practicar la técnica con problemas que ya sabéis resolver con un bucle. Así toda la atención va al **patrón**, no al problema en sí.

#### Analogía

Imagina que tienes que contar cuántas monedas hay en un montón enorme. Hacerlo tú solo es factible pero lento. Si repartes el montón a partes iguales entre dos personas, cada una cuenta su mitad, y luego sumáis los dos conteos... el resultado es correcto y habéis terminado en la mitad de tiempo. Si cada persona repite la misma estrategia con otras dos, el montón se reduce rápidamente a pilas de una sola moneda, que son triviales de "contar".

Eso es divide y vencerás: **repartir el trabajo dividiéndolo, resolver las partes simples directamente, y combinar las respuestas**.

## 1. La plantilla

Toda solución divide y vencerás sigue esta estructura:

```
función resolver(datos, inicio, fin):
    si el subproblema es trivial:              ← caso base
        devolver solución directa

    mitad = (inicio + fin) / 2

    resultadoIzq = resolver(datos, inicio, mitad)      ← dividir + vencer (izquierda)
    resultadoDer = resolver(datos, mitad + 1, fin)      ← dividir + vencer (derecha)

    devolver combinar(resultadoIzq, resultadoDer)       ← combinar
```

Lo que cambia de un algoritmo a otro es:

* **Cómo se divide**: normalmente por la mitad, pero no siempre.
* **Cuál es el caso base**: un solo elemento, cero elementos, un problema lo bastante pequeño...
* **Cómo se combinan los resultados**: sumar, tomar el máximo, mezclar, multiplicar...

La división y la recursión son casi siempre mecánicas. **La parte creativa es la combinación.** Cuando veas un problema y pienses "si alguien me diera la respuesta de cada mitad, ¿sabría obtener la respuesta total?", estás pensando en divide y vencerás.

## 2. Ejemplo guiado: suma de un array

**El problema**: calcular la suma de todos los elementos de un array de enteros.

Ya sabéis resolverlo con un `for`:

```java
public static int sumaIterativa(int[] arr) {
    int total = 0;
    for (int x : arr) total += x;
    return total;
}
```

Ahora vamos a resolverlo con divide y vencerás. La solución será "peor" en este caso (más código, más coste de llamadas), pero nos servirá para ver el patrón en un contexto donde no hay dudas sobre la corrección.

#### Las tres fases

**Dividir**: partimos el array en dos mitades, la izquierda `[inicio..mitad]` y la derecha `[mitad+1..fin]`.

**Vencer**: calculamos la suma de cada mitad recursivamente. El caso base es un subarray de un solo elemento, cuya suma es el propio elemento.

**Combinar**: sumamos los dos resultados parciales. Eso es todo: `sumaIzq + sumaDer`.

#### Implementación en Java

```java
public static int suma(int[] arr, int ini, int fin) {
    // Caso base: un solo elemento
    if (ini == fin) {
        return arr[ini];
    }

    // Dividir
    int mitad = (ini + fin) / 2;

    // Vencer (resolver cada mitad recursivamente)
    int sumaIzq = suma(arr, ini, mitad);
    int sumaDer = suma(arr, mitad + 1, fin);

    // Combinar
    return sumaIzq + sumaDer;
}
```

Se invoca con `suma(arr, 0, arr.length - 1)`.

#### Traza con `[3, 1, 4, 2]`

```
                    suma([3,1,4,2], 0, 3)
                   /                     \
          suma([3,1], 0, 1)         suma([4,2], 2, 3)
          /             \            /             \
    suma([3], 0, 0)  suma([1], 1, 1)  suma([4], 2, 2)  suma([2], 3, 3)
         = 3              = 1              = 4              = 2

    Combinaciones (de abajo hacia arriba):
        suma([3,1]) = 3 + 1 = 4
        suma([4,2]) = 4 + 2 = 6
        suma([3,1,4,2]) = 4 + 6 = 10   ✅
```

Dibuja este árbol en papel o en pizarra. Lo que estás viendo es:

* **Descenso**: el problema se parte sucesivamente en mitades hasta llegar a arrays de un elemento (los **casos base**, las hojas del árbol).
* **Ascenso**: las soluciones se combinan de abajo hacia arriba sumando los resultados de cada mitad.

Este árbol de recursión tiene una propiedad importante: su **profundidad** es `log₂ n`. Un array de 4 elementos tiene 2 niveles de división, uno de 8 tiene 3, uno de 1 024 tiene 10, uno de un millón tiene unos 20. Esa profundidad logarítmica es la que dará lugar a las complejidades O(n log n) que veremos pronto.

## 3. Segundo ejemplo: máximo de un array

Mismo patrón, distinta combinación.

**Dividir**: partir el array por la mitad.

**Vencer**: encontrar el máximo de cada mitad recursivamente. Caso base: un solo elemento, que es trivialmente su propio máximo.

**Combinar**: el máximo del array completo es el mayor de los dos máximos parciales.

```java
public static int maximo(int[] arr, int ini, int fin) {
    // Caso base
    if (ini == fin) {
        return arr[ini];
    }

    // Dividir
    int mitad = (ini + fin) / 2;

    // Vencer
    int maxIzq = maximo(arr, ini, mitad);
    int maxDer = maximo(arr, mitad + 1, fin);

    // Combinar
    return Math.max(maxIzq, maxDer);
}
```

Fíjate: el código es **prácticamente idéntico** al de la suma. Solo cambia la línea de combinación: `+` se convierte en `Math.max`. El paradigma es siempre el mismo; la creatividad está en qué haces al combinar.

#### Traza con `[2, 7, 1, 9]`

```
                   maximo([2,7,1,9], 0, 3)
                   /                      \
         maximo([2,7], 0, 1)        maximo([1,9], 2, 3)
          /            \             /            \
   maximo([2])    maximo([7])   maximo([1])    maximo([9])
       = 2            = 7           = 1            = 9

    Combinaciones:
        maximo([2,7]) = max(2, 7) = 7
        maximo([1,9]) = max(1, 9) = 9
        maximo([2,7,1,9]) = max(7, 9) = 9   ✅
```

## 4. Donde divide y vencerás marca la diferencia: exponenciación rápida

Los dos ejemplos anteriores eran didácticos: divide y vencerás los resuelve, pero no mejor que un `for`. Ahora viene el primer caso donde **cambia la complejidad** y la ventaja es real.

#### El problema

Calcular `xⁿ`. La versión ingenua multiplica `x` por sí mismo `n` veces:

```java
public static long potenciaIngenua(int x, int n) {
    long resultado = 1;
    for (int i = 0; i < n; i++) {
        resultado *= x;
    }
    return resultado;
}
```

Esto es **O(n)**: `n` multiplicaciones. Para `n = 1 000 000 000` (mil millones), es lento.

#### La observación matemática

Podemos explotar una propiedad de los exponentes:

```
x⁰ = 1

Si n es par:    xⁿ = (x^(n/2))²            → calculo la mitad y elevo al cuadrado
Si n es impar:  xⁿ = x · (x^(n/2))²        → lo mismo, pero multiplico por x una vez más
```

En lugar de `n` multiplicaciones, reducimos el exponente **a la mitad** en cada paso. Eso es divide y vencerás.

#### Implementación en Java

```java
public static long potenciaRapida(long x, int n) {
    // Caso base
    if (n == 0) {
        return 1;
    }

    // Dividir: resolver la mitad del exponente
    long mitad = potenciaRapida(x, n / 2);

    // Combinar
    if (n % 2 == 0) {
        return mitad * mitad;              // n par: resultado²
    } else {
        return mitad * mitad * x;          // n impar: resultado² · x
    }
}
```

#### ¿Por qué es más rápida?

Cada llamada recursiva divide `n` entre 2. Hacen falta `log₂ n` divisiones para llegar al caso base `n = 0`. Cada paso hace como mucho 2 multiplicaciones.

| Versión         | Multiplicaciones para `n = 1 000 000 000` |
| --------------- | ----------------------------------------- |
| Ingenua O(n)    | 1 000 000 000                             |
| Rápida O(log n) | \~30                                      |

Sí, has leído bien: **30 multiplicaciones frente a mil millones**. Esa es la potencia (nunca mejor dicho) de divide y vencerás cuando la división reduce genuinamente el trabajo.

#### Traza con `potenciaRapida(2, 10)`

```
potenciaRapida(2, 10)
  mitad = potenciaRapida(2, 5)
    mitad = potenciaRapida(2, 2)
      mitad = potenciaRapida(2, 1)
        mitad = potenciaRapida(2, 0)
          = 1                                  ← caso base
        n=1 es impar → 1 * 1 * 2 = 2
      n=2 es par → 2 * 2 = 4
    n=5 es impar → 4 * 4 * 2 = 32
  n=10 es par → 32 * 32 = 1024

Resultado: 1024 = 2¹⁰   ✅
```

Solo 4 niveles de recursión para calcular `2¹⁰`. La versión ingenua habría hecho 10 multiplicaciones. Para exponentes grandes, esta diferencia es abismal.

## 5. Búsqueda binaria: divide y vencerás que ya conocéis

Si ya habéis visto la búsqueda binaria, la conocéis como un bucle que va descartando mitades. Ahora podéis reinterpretarla con las gafas de divide y vencerás:

**Dividir**: partir el array en dos mitades por el punto medio.

**Vencer**: si el elemento buscado es igual al del medio, lo hemos encontrado (caso base). Si es menor, resolvemos recursivamente sobre la mitad izquierda. Si es mayor, sobre la mitad derecha.

**Combinar**: no hay nada que combinar. El resultado del subproblema **es** el resultado del problema. Esto es una particularidad: en divide y vencerás no siempre necesitas combinar las dos mitades. A veces solo necesitas resolver **una** de ellas.

```java
public static int busquedaBinaria(int[] arr, int ini, int fin, int objetivo) {
    // Caso base: no encontrado
    if (ini > fin) {
        return -1;
    }

    int mitad = (ini + fin) / 2;

    // Caso base: encontrado
    if (arr[mitad] == objetivo) {
        return mitad;
    }

    // Vencer: solo UNA de las dos mitades
    if (objetivo < arr[mitad]) {
        return busquedaBinaria(arr, ini, mitad - 1, objetivo);
    } else {
        return busquedaBinaria(arr, mitad + 1, fin, objetivo);
    }
}
```

Comparar con los ejemplos anteriores es instructivo:

| Algoritmo        | ¿Cuántas mitades resuelve?       | Combinación                        | Complejidad |
| ---------------- | -------------------------------- | ---------------------------------- | ----------- |
| Suma del array   | Las **dos**                      | Sumar resultados                   | O(n)        |
| Máximo del array | Las **dos**                      | `Math.max`                         | O(n)        |
| Potencia rápida  | **Una** (la mitad del exponente) | Elevar al cuadrado (± multiplicar) | O(log n)    |
| Búsqueda binaria | **Una** (izquierda o derecha)    | Ninguna                            | O(log n)    |

Cuando resuelves **las dos mitades**, el trabajo total es O(n) como mínimo, porque acabas tocando todos los elementos. Cuando resuelves **una sola mitad**, descartas la otra y el coste se reduce a O(log n). Esta distinción es la clave para intuir la complejidad de cualquier algoritmo divide y vencerás.

## 6. El patrón visual: el árbol de recursión

En todos los ejemplos hemos dibujado el mismo tipo de diagrama: un **árbol** donde cada nodo se divide en dos hijos. Familiarizarse con esta estructura es fundamental, porque la veremos una y otra vez:

**Profundidad del árbol**: `log₂ n`. Cada nivel divide el tamaño del problema por 2.

**Nodos por nivel**: depende de cuántas mitades resuelvas. Si resuelves las dos, el número de nodos se duplica en cada nivel (1, 2, 4, 8...). Si resuelves solo una, hay un único nodo por nivel.

**Trabajo total**: profundidad × trabajo por nivel.

| Patrón                                  | Nodos por nivel | Trabajo por nivel | Trabajo total  |
| --------------------------------------- | --------------- | ----------------- | -------------- |
| Resolver las dos mitades, combinar O(1) | Se duplican     | O(n) total        | O(n)           |
| Resolver las dos mitades, combinar O(n) | Se duplican     | O(n) total        | **O(n log n)** |
| Resolver una sola mitad                 | Constante (1)   | O(1) o O(log n)   | O(log n)       |

La segunda fila de la tabla es la que importa para lo que viene después: cuando la combinación es O(n) —como será en _merge sort_—, el trabajo total es O(n log n).

## 7. Resumen: divide y vencerás en tres preguntas

Cuando te enfrentes a un problema y pienses en aplicar divide y vencerás, hazte estas tres preguntas:

1. **¿Puedo partir el problema en subproblemas del mismo tipo?** Si no, divide y vencerás no aplica.
2. **¿Cómo combino las soluciones parciales?** Esta es la pregunta creativa. Si la respuesta es fácil (sumar, tomar el máximo), el algoritmo sale casi solo. Si la respuesta es compleja (como mezclar dos arrays ordenados), ahí es donde necesitas más trabajo.
3. **¿Cuántas mitades necesito resolver?** Una sola → probablemente O(log n). Las dos → probablemente O(n) u O(n log n) según el coste de la combinación.

***

## 8. Ejercicios

#### Ejercicio 1 — Mínimo de un array _(básico)_

Encuentra el elemento mínimo de un array usando divide y vencerás.

```
minimo([4, 2, 7, 1, 5])  →  1
minimo([9])               →  9
minimo([3, 3, 3])         →  3
```

**Firma:**

```java
public static int minimo(int[] arr, int ini, int fin)
```

> _Pista:_ es idéntico al máximo. Solo cambia una función en la combinación.

***

#### Ejercicio 2 — Contar ocurrencias _(básico)_

Cuenta cuántas veces aparece un valor dado en un array, usando divide y vencerás.

```
contar([1, 3, 2, 3, 3, 1], 3)  →  3
contar([5, 5, 5, 5], 5)        →  4
contar([1, 2, 3], 7)            →  0
```

**Firma:**

```java
public static int contar(int[] arr, int ini, int fin, int valor)
```

> _Pista:_ el caso base es un solo elemento: devuelve `1` si es igual al valor buscado, `0` si no. La combinación es sumar los conteos de las dos mitades.

***

#### Ejercicio 3 — Comprobar si un array está ordenado _(medio)_

Determina si un array está ordenado ascendentemente usando divide y vencerás.

```
estaOrdenado([1, 2, 3, 4, 5])  →  true
estaOrdenado([1, 3, 2, 4])     →  false
estaOrdenado([5])               →  true
estaOrdenado([2, 2, 2])        →  true
```

**Firma:**

```java
public static boolean estaOrdenado(int[] arr, int ini, int fin)
```

> _Pista:_ la combinación no es solo "izquierda ordenada AND derecha ordenada". Piensa: ¿qué pasa si la mitad izquierda termina en `5` y la derecha empieza en `3`? Ambas están ordenadas internamente, pero el array completo no lo está. Necesitas comprobar **también** que el último elemento de la izquierda es ≤ el primero de la derecha. Es decir: `arr[mitad] <= arr[mitad + 1]`.
>
> Este ejercicio es importante porque muestra que a veces la combinación es algo más que una operación aritmética simple.

***

#### Ejercicio 4 — Producto de los elementos _(básico)_

Calcula el producto de todos los elementos de un array.

```
producto([1, 2, 3, 4])    →  24
producto([5])              →  5
producto([2, 3, 0, 4])    →  0
producto([1, 1, 1, 1, 1]) →  1
```

**Firma:**

```java
public static long producto(int[] arr, int ini, int fin)
```

> _Pista:_ si has hecho los tres anteriores, este sale solo. Caso base: un elemento (el propio valor). Combinación: multiplicar.

***

#### Ejercicio 5 — Exponenciación rápida iterativa _(medio)_

En el tutorial has visto la exponenciación rápida recursiva. Ahora impleméntala de forma **iterativa** (sin recursión). El truco es ir elevando al cuadrado y reduciendo el exponente, en un bucle.

```
potencia(2, 10)    →  1024
potencia(3, 13)    →  1594323
potencia(5, 0)     →  1
```

**Firma:**

```java
public static long potenciaIterativa(long x, int n)
```

> _Pista:_ en cada iteración del bucle, si `n` es impar multiplicas el resultado acumulado por `x`, luego elevas `x` al cuadrado (`x = x * x`) y divides `n` entre 2. Cuando `n` llega a 0, has terminado. Es la misma lógica que la versión recursiva pero "desenrollada".

***

#### Ejercicio 6 — Máximo y mínimo simultáneos _(medio-difícil)_

Encuentra el máximo **y** el mínimo de un array usando divide y vencerás, **en una sola pasada**. Devuelve ambos valores (puedes usar un `int[2]` donde `[0]` es el mínimo y `[1]` es el máximo).

```
maxMin([3, 1, 7, 2, 5])  →  [1, 7]
maxMin([4])               →  [4, 4]
maxMin([8, 2])            →  [2, 8]
```

**Firma:**

```java
public static int[] maxMin(int[] arr, int ini, int fin)
```

> _Pista:_ caso base de un elemento: devuelve `{arr[ini], arr[ini]}`. Caso base de dos elementos (optimización): compáralos directamente con una sola comparación. Para la combinación, el mínimo global es el menor de los dos mínimos parciales, y el máximo global es el mayor de los dos máximos parciales.
>
> Lo interesante de este ejercicio es que la versión divide y vencerás hace **menos comparaciones** que la versión ingenua. Un recorrido lineal clásico necesita `2·(n-1)` comparaciones (una para actualizar el mínimo, otra para el máximo, en cada posición). La versión divide y vencerás necesita solo `3n/2 - 2`. Para un array de 100 elementos, eso es 148 frente a 198. La diferencia proviene de que los casos base de dos elementos hacen una sola comparación en lugar de dos.

***

#### Ejercicio 7 — Suma de un array de forma equilibrada _(reto)_

Cuando se suman números con punto flotante (`double`), el orden de las sumas afecta a la precisión del resultado. Sumar de izquierda a derecha acumula errores porque un acumulador grande "aplasta" las contribuciones de números pequeños.

La suma por divide y vencerás es más precisa porque siempre suma valores de magnitud similar (las sumas parciales de mitades del mismo tamaño).

Implementa una función que sume un `double[]` usando divide y vencerás y compara su resultado con la suma iterativa de izquierda a derecha para el siguiente array de prueba:

```java
double[] arr = new double[1_000_000];
for (int i = 0; i < arr.length; i++) {
    arr[i] = 0.1;
}
// La suma exacta debería ser 100000.0
```

**Firma:**

```java
public static double sumaEstable(double[] arr, int ini, int fin)
```

> _Pista:_ el código es prácticamente idéntico al de la suma de enteros. Lo interesante está en los resultados: la suma iterativa da algo como `99999.99999999861` (error visible), mientras que la divide y vencerás da algo mucho más próximo a `100000.0`.
>
> Este ejercicio demuestra que divide y vencerás no solo puede ser más rápido: a veces puede ser **más preciso**. Es una de las razones por las que las bibliotecas científicas y de machine learning usan sumas jerárquicas internamente.
