---
cover: ../../.gitbook/assets/algorithm.jpg
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

# Quicksort

Es otro algoritmo de ordenación basado en **divide y vencerás**, igual que _merge sort_, pero con un reparto del trabajo radicalmente distinto.

Donde _merge sort_ divide el array por la mitad de forma trivial y concentra todo el esfuerzo en la fusión final, _quicksort_ hace justo lo contrario: invierte mucho trabajo en la división (eligiendo bien dónde partir) y, a cambio, **la combinación es gratis**. No hay nada que combinar al final: cuando las dos mitades quedan ordenadas, el array entero ya está ordenado.

Es uno de los algoritmos más usados del mundo. La función `Arrays.sort` de Java sobre arrays de primitivos usa una variante muy optimizada de _quicksort_ (concretamente, _Dual-Pivot Quicksort_ desde Java 7). Aprenderlo es entender por qué es la elección por defecto en miles de bibliotecas estándar.

**Requisitos previos**

* **Recursión** dominada.
* **Divide y vencerás** entendido (la página anterior).
* La técnica de **dos punteros** sobre arrays.

### 1. La idea central: el pivote y la partición

La estrategia de _quicksort_ parte de una observación muy sencilla. Imagina que tienes un array desordenado y eliges uno cualquiera de sus elementos al que llamarás **pivote**. Ahora reorganiza el array de forma que:

* Todos los elementos **menores o iguales** al pivote queden a su izquierda.
* Todos los elementos **mayores** queden a su derecha.
* El pivote ocupe su posición correcta entre ambos grupos.

A esa operación se le llama **particionar**. Después de hacerla, sabes una cosa importantísima: **el pivote ya está en su posición definitiva en el array ordenado**. Y aunque las dos mitades izquierda y derecha aún no estén ordenadas internamente, sí sabemos que la izquierda solo contiene elementos que pertenecen a esa zona, y la derecha solo elementos que pertenecen a la suya.

A partir de ahí, basta con ordenar cada mitad por separado, recursivamente, aplicando _quicksort_ sobre cada una. Cuando lleguen al caso base (subarrays de 0 o 1 elementos), el array entero estará ordenado.

**Analogía**

Imagina que tienes que ordenar por estatura a un grupo grande de alumnos. Eliges uno cualquiera, lo pones de pie como referencia, y le dices al resto: "los que sois más bajos que él, a su izquierda; los más altos, a su derecha". En un solo barrido el alumno-referencia queda en su sitio definitivo. Ahora repites el mismo procedimiento por separado con el grupo de la izquierda y con el de la derecha. Cuando los dos grupos pequeños estén ordenados, todos lo estarán.

Eso es _quicksort_: **un pivote por nivel de recursión, dos subgrupos a procesar, ningún esfuerzo de combinación al final**.

### 2. Las tres fases aplicadas a _quicksort_

Volvamos a la plantilla de divide y vencerás:

1. **Dividir:** elegir un pivote y particionar el array en dos zonas (≤ pivote y > pivote). El pivote queda colocado entre ambas en su posición final.
2. **Vencer:** ordenar cada zona por separado mediante una llamada recursiva. Caso base: subarrays de 0 o 1 elementos.
3. **Combinar:** **no hay nada que hacer**. Las dos mitades ya están en su sitio dentro del array, separadas por el pivote, así que el array entero está ordenado tras las recursiones.

Compara con _merge sort_: allí dividir era trivial (`mitad = (ini + fin) / 2`) y combinar era costoso (la operación `merge`, O(n)). Aquí ocurre lo opuesto: dividir es costoso (la partición, O(n)) y combinar es gratis. La cantidad total de trabajo es similar, pero está distribuida de otra manera.

### 3. El corazón del algoritmo: la operación _partición_

Vamos a ver cómo se hace una partición en la práctica. Hay varios esquemas posibles; usaremos el llamado **esquema de Lomuto**, que es el más sencillo de explicar y de implementar.

**Pasos del esquema de Lomuto**

1. Elegir como pivote el **último elemento** del rango (`arr[fin]`).
2. Mantener un índice `s` (de "store") que apunta a la primera posición todavía libre del grupo de los menores. Empieza en `ini`.
3. Recorrer el array con un índice `i` desde `ini` hasta `fin - 1`.
4. Si `arr[i] <= pivote`, intercambiar `arr[i]` con `arr[s]` y avanzar `s`.
5. Si `arr[i] > pivote`, no hacer nada (queda en la zona derecha).
6. Al final del recorrido, intercambiar `arr[s]` con `arr[fin]`. Eso coloca el pivote en su posición correcta, justo entre los dos grupos.
7. Devolver `s`: la posición final del pivote.

La intuición detrás del índice `s`: durante el recorrido, la zona `arr[ini..s-1]` siempre contiene los elementos ya confirmados como ≤ pivote, y la zona `arr[s..i-1]` los ya confirmados como > pivote. El intercambio final pone el pivote en la frontera entre ambas.

**Traza visual de una partición**

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

**Coste de una partición**

Cada elemento del rango se examina exactamente una vez en el bucle. Para un rango de tamaño `n`, la partición es **O(n)**.

### 4. El algoritmo completo

Una vez tenemos la operación de partición, _quicksort_ se reduce a tres líneas conceptuales:

```
quicksort(arr, ini, fin):
    si ini >= fin:                                ← caso base: 0 o 1 elementos
        no hacer nada (ya está ordenado)

    p = particionar(arr, ini, fin)                ← dividir

    quicksort(arr, ini, p - 1)                    ← vencer izquierda
    quicksort(arr, p + 1, fin)                    ← vencer derecha

    (no hay nada que combinar)
```

Fíjate en un detalle clave: el rango izquierdo es `[ini..p-1]` y el derecho es `[p+1..fin]`. **El pivote en la posición `p` se queda fuera de ambas recursiones**: ya está colocado en su sitio definitivo y no hay que volver a tocarlo. Esto es lo que hace que _quicksort_ "consuma" un elemento por nivel de recursión.

### 5. Traza completa: ordenando `[4, 2, 7, 1, 5, 3, 6]`

Vamos a desplegar todas las recursiones. Marcaremos cada llamada con el rango sobre el que opera y el pivote que elige (siempre el último del rango).

```
quicksort([4, 2, 7, 1, 5, 3, 6], rango 0..6, pivote = 6)
   particionar → [4, 2, 1, 5, 3, | 6 | 7]
                 izq: 0..4         der: 6..6
   ↓
   quicksort(izq = [4, 2, 1, 5, 3], rango 0..4, pivote = 3)
      particionar → [2, 1, | 3 | 5, 4]
                    izq: 0..1       der: 3..4
      ↓
      quicksort([2, 1], rango 0..1, pivote = 1)
         particionar → [| 1 | 2]
                       izq: 0..-1   der: 1..1
         ↓
         quicksort([], rango 0..-1) → caso base
         quicksort([2], rango 1..1) → caso base
      ↓
      quicksort([5, 4], rango 3..4, pivote = 4)
         particionar → [| 4 | 5]
                       izq: 3..2    der: 4..4
         ↓
         quicksort([], rango 3..2) → caso base
         quicksort([5], rango 4..4) → caso base
   ↓
   quicksort([7], rango 6..6) → caso base

Resultado final: [1, 2, 3, 4, 5, 6, 7]   ✅
```

Pinta este árbol en papel: cada nodo es una llamada, las flechas verticales son las llamadas recursivas. Observa cómo el pivote de cada llamada queda fijado en su posición correcta y nunca se vuelve a tocar.

### 6. Análisis de complejidad: el caso medio y el caso peor

Aquí _quicksort_ tiene una historia más rica que _merge sort_. Su comportamiento depende **mucho** de cómo de bien dividan los pivotes.

**Caso ideal: el pivote parte el array por la mitad**

Si en cada partición el pivote resulta ser el elemento mediano del rango, las dos mitades resultantes tienen aproximadamente el mismo tamaño. Entonces el árbol de recursión tiene `log₂ n` niveles, y en cada nivel el trabajo total de las particiones es O(n). Total: **O(n log n)**.

```
log₂ n niveles  ×  n operaciones por nivel  =  n · log₂ n  →  O(n log n)
```

Igual que _merge sort_. De hecho, si los pivotes son mágicamente perfectos, los dos algoritmos hacen aproximadamente las mismas comparaciones.

**Caso peor: el pivote es siempre el extremo**

Imagina que el array está **ya ordenado** y tu estrategia es coger siempre el último como pivote. ¿Qué ocurre?

```
arr inicial: [1, 2, 3, 4, 5, 6, 7]
pivote = 7 → todos los demás van a la izquierda
particionar → [1, 2, 3, 4, 5, 6, | 7]
              ←── tamaño 6 ──→     ya colocado

quicksort([1, 2, 3, 4, 5, 6])
pivote = 6 → todos los demás van a la izquierda
particionar → [1, 2, 3, 4, 5, | 6 | 7]
              ←── tamaño 5 ──→

... y así sucesivamente.
```

En cada llamada, una de las dos mitades es de tamaño 0 y la otra de tamaño `n-1`. El árbol de recursión, en lugar de ser un árbol equilibrado de profundidad `log n`, se convierte en una cadena lineal de profundidad `n`. El coste total se vuelve:

```
n + (n-1) + (n-2) + ... + 1  ≈  n²/2  →  O(n²)
```

**Catastrófico**. Para un millón de elementos, eso es del orden de 500 mil millones de operaciones, indistinguible de la burbuja.

Lo desconcertante es que el peor caso ocurre con la entrada que parecería más fácil: **un array ya ordenado**.

**Caso medio: la magia probabilística**

¿Significa esto que _quicksort_ es peligroso en la práctica? La respuesta corta es no, gracias a un truco muy elegante.

Cuando los pivotes se eligen **al azar**, el caso medio sobre todas las posibles entradas resulta ser **O(n log n)**, y el peor caso O(n²) se vuelve extraordinariamente improbable: requeriría que la suerte fuese sistemáticamente mala en cada nivel de recursión.

| Estrategia de pivote | Mejor caso | Caso medio | Peor caso                           |
| -------------------- | ---------- | ---------- | ----------------------------------- |
| Último elemento      | O(n log n) | O(n log n) | **O(n²)** sobre arrays ya ordenados |
| Elemento aleatorio   | O(n log n) | O(n log n) | O(n²) (muy improbable)              |
| Mediana de tres      | O(n log n) | O(n log n) | O(n²) (extremadamente improbable)   |

Esto conecta con la sección "algoritmos probabilísticos" de la introducción: _quicksort con pivote aleatorio_ es el ejemplo canónico. Introducir aleatoriedad en un algoritmo determinista convierte un peor caso garantizado en un peor caso casi imposible.

**Comparación con&#x20;**_**merge sort**_

| Aspecto                  | _Merge sort_   | _Quicksort_                           |
| ------------------------ | -------------- | ------------------------------------- |
| Mejor caso               | O(n log n)     | O(n log n)                            |
| Caso medio               | O(n log n)     | O(n log n)                            |
| **Peor caso**            | **O(n log n)** | **O(n²)**                             |
| Espacio extra            | O(n)           | O(log n) (pila de recursión)          |
| Estable                  | Sí             | No                                    |
| In-place                 | No             | Sí                                    |
| Constante multiplicativa | Mayor          | **Menor** (más rápido en la práctica) |

En la práctica, _quicksort_ con buena elección de pivote es **más rápido** que _merge sort_ a pesar de tener peor garantía teórica, porque:

* Trabaja in-place, sin las copias a arrays auxiliares.
* La constante multiplicativa de la O grande es menor (menos operaciones por elemento).
* Aprovecha mejor la caché del procesador (acceso secuencial al array).

Por eso es la opción por defecto en bibliotecas estándar para arrays de primitivos. Para objetos donde la estabilidad importa, se prefiere _merge sort_ (o variantes como Timsort).

### 7. La elección del pivote

La calidad de tu _quicksort_ depende casi por completo de cómo elijas el pivote en cada partición. Hay varias estrategias:

**Estrategia 1: el último elemento (ingenua)**

Es la que hemos usado en las trazas y la más simple de implementar. Pero tiene un peor caso garantizado sobre arrays ya ordenados o casi ordenados, situación lamentablemente común en la vida real (muchas veces los datos llegan con cierto orden).

**Cuándo usarla**: solo en ejercicios docentes para entender el algoritmo. Nunca en producción.

**Estrategia 2: elemento aleatorio**

Antes de cada partición, eliges un índice aleatorio entre `ini` y `fin`, e intercambias ese elemento con el último. Después aplicas el esquema normal con `arr[fin]` como pivote.

Esto convierte el peor caso O(n²) en algo prácticamente imposible: requeriría que el generador de aleatorios sacase mala suerte sistemática en cada nivel.

**Cuándo usarla**: implementaciones generales donde no hay garantía sobre los datos de entrada.

**Estrategia 3: mediana de tres**

En cada partición, mira tres elementos del rango (típicamente el primero, el último y el del medio), calcula cuál de los tres tiene el valor mediano, y úsalo como pivote.

Esta estrategia es determinista (no introduce aleatoriedad) pero rompe los patrones malignos más comunes (arrays ordenados ascendente o descendentemente). Es la que usan muchas bibliotecas profesionales.

**Cuándo usarla**: cuando no puedes o no quieres usar aleatoriedad pero necesitas robustez.

**Estrategia 4: pivote dual (avanzada)**

Java 7+ usa _Dual-Pivot Quicksort_: en lugar de un pivote, elige dos pivotes y particiona el array en tres zonas (menores que el menor, intermedios, mayores que el mayor). Es más complejo de implementar pero suele ser entre un 10% y un 20% más rápido en la práctica. Está fuera del alcance de este tutorial pero merece mencionarse: es lo que ejecuta tu programa cuando llamas a `Arrays.sort` con un `int[]`.

### 8. Propiedades de _quicksort_

**In-place: sí**

A diferencia de _merge sort_, _quicksort_ no necesita arrays auxiliares. Toda la reordenación ocurre intercambiando elementos dentro del propio array. La memoria adicional es solo la de la pila de llamadas recursivas: O(log n) en el caso medio.

**Estable: no**

El esquema de Lomuto (y también el de Hoare) puede alterar el orden relativo de elementos iguales. Si tu aplicación necesita estabilidad (por ejemplo, ordenar registros por varios criterios sucesivos), _quicksort_ no sirve. Usa _merge sort_ o Timsort.

**Adaptativo: no**

Detectar que un array ya está ordenado no le ayuda a _quicksort_. De hecho, con la estrategia ingenua de pivote, los arrays ya ordenados son justamente su peor caso.

**Resumen**

| Propiedad         | _Quicksort_                  |
| ----------------- | ---------------------------- |
| Mejor caso        | O(n log n)                   |
| Caso medio        | O(n log n)                   |
| Peor caso         | O(n²)                        |
| Espacio adicional | O(log n) (pila de recursión) |
| Estable           | No                           |
| In-place          | Sí                           |
| Adaptativo        | No                           |

### 9. Implementarlo tú mismo: guía de decisiones

**Firma de los métodos**

Igual que en _merge sort_, vas a necesitar:

* Un método `quicksort` recursivo que reciba el array y los índices `ini` y `fin`.
* Un método `particionar` que reciba lo mismo y devuelva un `int` con la posición final del pivote.
* Opcionalmente, un método fachada `quicksort(int[] arr)` para uso cómodo.

Probablemente también te convenga un método auxiliar `intercambiar(int[] arr, int i, int j)` que se usará varias veces dentro de `particionar`.

**Caso base**

`if (ini >= fin) return;`. Igual que en _merge sort_.

**Implementación de `particionar` (esquema de Lomuto)**

Sigue al pie de la letra los siete pasos de la sección 3. Lo más fácil es empezar guardando `pivote = arr[fin]`, inicializar `s = ini`, recorrer con un `for` desde `ini` hasta `fin - 1`, y aplicar la lógica de intercambiar y avanzar `s` cuando proceda. Al salir del bucle, el intercambio final coloca el pivote en su sitio.

Devuelve `s`: la posición final del pivote.

**Errores típicos al implementarlo**

* **El bucle del particionado va hasta `fin - 1`, no hasta `fin`.** Si llega al pivote, lo intercambia consigo mismo y rompe la invariante. Es el error más común.
* **Olvidar el intercambio final** entre `arr[s]` y `arr[fin]`. Si lo olvidas, el pivote se queda al final y la "partición" no separa nada bien.
* **Confundir el rango de las recursiones.** La izquierda es `[ini, p-1]` y la derecha es `[p+1, fin]`. Si pones `p` en alguno de los dos, vuelves a procesar el pivote y entras en bucle infinito hasta el stack overflow.
* **No probar con arrays ya ordenados.** Tu código puede funcionar perfectamente con arrays aleatorios y degenerar a O(n²) con uno ya ordenado. Si quieres protegerte, implementa la estrategia 2 o 3 de elección de pivote.

**Pruébalo siempre con casos límite**

* Array vacío `{}` y de un elemento `{42}`.
* Array ya ordenado `{1, 2, 3, 4, 5}`. (Cronométralo con la versión ingenua y con la versión aleatoria. La diferencia es espectacular).
* Array ordenado al revés `{5, 4, 3, 2, 1}`.
* Array con muchos duplicados `{3, 3, 3, 3, 3}`. (Lomuto se comporta mal con esto: cae a O(n²). Hay variantes específicas que lo solucionan, pero quedan fuera de este tutorial).
* Array con un solo valor distinto al final.

***

### 10. Ejercicios

**Ejercicio 1 — Implementar la operación `particionar`** _**(básico)**_

Implementa **solo** la operación de partición con el esquema de Lomuto. Recibe el array y los índices `ini`, `fin` del rango sobre el que operar. Tras la llamada, todos los elementos ≤ pivote están a la izquierda de la posición devuelta y todos los > pivote a la derecha. Devuelve la posición final del pivote.

```
Antes:    arr = [4, 2, 7, 1, 5, 3, 6],  rango 0..6,  pivote = arr[6] = 6
Después:  arr = [4, 2, 1, 5, 3, 6, 7],  devuelve 5
```

**Firma:**

```
private static int particionar(int[] arr, int ini, int fin)
```

> _Pista:_ sigue los siete pasos de la sección 3. Pruébalo con varios rangos antes de meterlo en la recursión. Comprueba que tras la llamada los elementos antes de la posición devuelta son ≤ pivote y los de después son > pivote.

***

**Ejercicio 2 — Implementar `quicksort` recursivo&#x20;**_**(básico)**_

Una vez tengas `particionar` funcionando, implementa el método recursivo. Tres líneas hacen el trabajo: una llamada a `particionar` y dos llamadas recursivas. Recuerda que el pivote queda fuera de las dos recursiones.

**Firma:**

```
public static void quicksort(int[] arr, int ini, int fin)
```

Y opcionalmente la fachada:

```
public static void quicksort(int[] arr)
```

> _Pista:_ recuerda los rangos: izquierda `[ini, p-1]` y derecha `[p+1, fin]`. Si te lías, vuelve al pseudocódigo de la sección 4.

***

**Ejercicio 3 — Quicksort con pivote aleatorio&#x20;**_**(medio)**_

Modifica tu `particionar` para que, antes de tomar `arr[fin]` como pivote, intercambie `arr[fin]` con un elemento elegido aleatoriamente del rango `[ini, fin]`. El resto del algoritmo no cambia.

Ejecuta tu _quicksort_ original y la versión aleatoria sobre un array ya ordenado de 10 000 elementos, y mide el tiempo de ambas. Anota la diferencia: con la versión ingenua puedes esperar cientos de milisegundos o más; con la aleatoria, microsegundos.

> _Pista:_ usa `java.util.Random` o `Math.random()` para elegir el índice aleatorio. Asegúrate de que cae en el rango `[ini, fin]` inclusive. Es exactamente el mismo `particionar` con dos líneas extra al inicio.

***

**Ejercicio 4 — Detectar el caso peor&#x20;**_**(medio)**_

Mide empíricamente el tiempo que tarda tu _quicksort_ ingenuo (último elemento como pivote) sobre arrays de tamaños crecientes con tres tipos de entrada:

* **Aleatoria**: array generado con valores aleatorios.
* **Ordenada ascendente**: `[1, 2, 3, ..., n]`.
* **Ordenada descendente**: `[n, n-1, ..., 1]`.

Para `n = 10 000` y `n = 100 000`, anota los tiempos. Verás que para entrada aleatoria los tiempos crecen linealmente con `n log n`, mientras que para entradas ordenadas crecen cuadráticamente.

> _Pista:_ este ejercicio es importante porque convierte la advertencia teórica del peor caso en una experiencia tangible. Después de verlo en tu propia máquina, no se te olvida por qué se prefiere el pivote aleatorio.

***

**Ejercicio 5 — Mediana de tres&#x20;**_**(medio-difícil)**_

Implementa la estrategia de pivote "mediana de tres": antes de particionar, calcula cuál de los tres elementos `arr[ini]`, `arr[mitad]` y `arr[fin]` tiene el valor mediano (no el mayor ni el menor), e intercámbialo con `arr[fin]`. A partir de ahí aplica la partición normal.

Demuestra que con esta estrategia, los casos malignos del ejercicio 4 (arrays ya ordenados) ya no causan O(n²).

> _Pista:_ solo necesitas tres comparaciones para encontrar la mediana de tres elementos. Hazlo paso a paso: si `a > b`, intercambia. Después si `b > c`, intercambia. Después si `a > b` otra vez, intercambia. Tras esos tres intercambios, `b` contiene la mediana.

***

**Ejercicio 6 —&#x20;**_**Quickselect**_**: encontrar el k-ésimo menor&#x20;**_**(reto)**_

Adapta _quicksort_ para resolver un problema relacionado: dado un array y un entero `k`, encontrar el **k-ésimo menor elemento** (el que ocuparía la posición `k` si ordenásemos). La gracia es que se puede hacer en **O(n) caso medio**, sin ordenar todo el array.

```
quickselect([7, 2, 1, 8, 6, 3, 5, 4], k = 0)  →  1   (el menor)
quickselect([7, 2, 1, 8, 6, 3, 5, 4], k = 3)  →  4   (el cuarto menor)
quickselect([7, 2, 1, 8, 6, 3, 5, 4], k = 7)  →  8   (el mayor)
```

**Firma:**

```
public static int quickselect(int[] arr, int k)
```

> _Pista:_ la idea es la misma que _quicksort_ pero con una optimización: tras particionar, sabes que el pivote ocupa la posición `p`. Si `p == k`, has encontrado la respuesta. Si `p > k`, el k-ésimo menor está en la mitad izquierda → recurre solo allí. Si `p < k`, está en la mitad derecha → recurre solo allí. Como solo recurres en **una** de las dos mitades, el coste medio cae a O(n) (la suma de la serie geométrica `n + n/2 + n/4 + ... ≤ 2n`).
>
> Este algoritmo se llama **quickselect** y es la base del método "mediana de medianas" para encontrar la mediana de un array en tiempo lineal garantizado, un resultado teórico importante de la informática.
