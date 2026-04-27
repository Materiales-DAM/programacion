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

# Heapsort

Es un algoritmo de ordenación distinto a los anteriores: **no se basa en divide y vencerás**, sino en una estructura de datos llamada **heap binario**. Antes de poder entender el algoritmo, tenemos que conocer esa estructura. Por eso este tutorial dedica las primeras secciones al heap como objeto, y solo más adelante muestra cómo aprovecharlo para ordenar.

A cambio del esfuerzo conceptual extra, _heapsort_ tiene tres propiedades muy atractivas que lo hacen indispensable conocer:

* Funciona **in-place**, sin necesidad de arrays auxiliares (a diferencia de _merge sort_).
* Tiene **garantía O(n log n) en el peor caso** (a diferencia de _quicksort_, que se degrada a O(n²)).
* Su estructura subyacente, el heap, es la base de las **colas de prioridad**, que aparecen en algoritmos famosos como Dijkstra (caminos mínimos) o Huffman (compresión).

**Requisitos previos**

* **Recursión** (la operación interna del heap, `siftDown`, se define de forma natural recursivamente).
* Manejo cómodo con **índices de arrays** y aritmética sobre ellos.
* Las nociones de **árbol binario** y **profundidad de un árbol**, aunque sea de manera intuitiva.

### 1. ¿Qué es un heap binario?

Un **heap binario** es un árbol binario con dos restricciones:

**Restricción 1: el árbol es completo.** Todos los niveles del árbol están llenos excepto, posiblemente, el último, que se rellena de izquierda a derecha sin huecos. No se permiten "agujeros" en medio.

```
   Heap completo:        NO es heap completo:

       A                       A
      / \                     / \
     B   C                   B   C
    / \                     /     \      ← hueco en el último nivel
   D   E                   D       E
```

**Restricción 2: orden parental.** En un **max-heap**, cada nodo es mayor o igual que sus hijos. (En un **min-heap** ocurre lo contrario: cada nodo es menor o igual que sus hijos. Para _heapsort_ en orden ascendente usaremos max-heap.)

```
   Es un max-heap:       NO es max-heap:

       50                      50
      /  \                    /  \
     30   40                 30   40
    / \                     / \
   10  20                  60  20    ← 60 > 30, viola la propiedad
```

Fíjate en lo que **no** exige un heap: que esté ordenado entre hermanos, ni entre niveles distintos. Solo garantiza la relación padre-hijo. Es una estructura **parcialmente ordenada**: más estructurada que un array desordenado, pero menos que un array ordenado. Justo lo necesario para extraer eficientemente el máximo y reorganizarse rápido.

**La propiedad fundamental**

En un max-heap, **el máximo del conjunto está siempre en la raíz**. Esto es consecuencia inmediata de la restricción 2: si la raíz fuera menor que algún elemento, ese elemento estaría entre sus descendientes, y por la propiedad transitiva tendría que existir una violación padre-hijo en algún punto del camino hasta la raíz.

Esa propiedad es la base del algoritmo: **siempre sabemos dónde está el máximo, y podemos sacarlo**.

### 2. Cómo se representa un heap en un array

Aquí viene la parte ingeniosa. Aunque conceptualmente un heap es un árbol, en la práctica se almacena en un array sin necesidad de punteros ni nodos. La clave es que, al ser un árbol completo, cada posición del árbol tiene una correspondencia natural con un índice del array si recorremos por niveles, de izquierda a derecha.

```
Árbol:              Array:

       50            índices:  0   1   2   3   4   5
      /  \           valores: [50, 30, 40, 10, 20, 35]
     30   40
    / \   /
   10 20 35
```

Recorriendo el árbol por niveles (raíz, luego hijos de la raíz, luego nietos...) y asignando índices consecutivos, las relaciones padre-hijo siguen un patrón aritmético sencillo:

* **Hijo izquierdo del nodo en `i`**: posición `2i + 1`.
* **Hijo derecho del nodo en `i`**: posición `2i + 2`.
* **Padre del nodo en `i`** (con `i > 0`): posición `(i - 1) / 2` (división entera).

Para el ejemplo: el nodo en posición 1 (valor 30) tiene como padre el nodo en `(1-1)/2 = 0` (valor 50, ✅), y como hijos los nodos en `2·1+1 = 3` (valor 10, ✅) y `2·1+2 = 4` (valor 20, ✅).

**Por qué esto es importante**

Esta representación tiene tres ventajas que conviene apreciar:

1. **No hace falta crear clases ni objetos**: el heap es un simple `int[]`, exactamente como los arrays con los que ya trabajas.
2. **No hay punteros que mantener**: navegar al padre o a los hijos es pura aritmética O(1).
3. **No hay memoria desperdiciada**: el array es exactamente del tamaño del heap.

Esta es una de las razones por las que el heap es la estructura elegida para implementar colas de prioridad en bibliotecas estándar como `java.util.PriorityQueue`.

### 3. La operación fundamental: `siftDown`

Aquí viene la operación que mueve toda la maquinaria. Se llama `siftDown` ("hacer caer"), también conocida como `heapify`.

**El problema que resuelve**

Imagina que tienes un heap correcto excepto en un punto: el nodo de la posición `i` puede ser **menor que alguno de sus hijos**, violando la propiedad de max-heap. El resto del árbol sí cumple la propiedad. Queremos restaurar el heap **moviendo el nodo problemático hacia abajo** hasta que vuelva a estar en su sitio.

```
Antes de siftDown(0):       Después:

    5                          50
   / \                        /  \
  50  40                     20   40
 /  \                       /
20  30                    5
                            \
                             30
```

(El 5 ha "caído" desde la raíz hasta una posición donde ya respeta la propiedad).

**Pasos de `siftDown(i, n)`**

Aquí `n` es el tamaño actual del heap dentro del array (necesitamos saberlo porque, durante la ordenación, el heap se irá encogiendo).

1. Calcular las posiciones de los hijos: `izq = 2i + 1`, `der = 2i + 2`.
2. Determinar cuál de los tres (`i`, `izq`, `der`) tiene el valor mayor. Cuidado: si `izq` o `der` están fuera del heap (es decir, ≥ `n`), no existen y no se consideran.
3. Si el mayor es el propio `i`: la propiedad de heap se cumple en este nodo, terminar.
4. Si el mayor es uno de los hijos: intercambiar `arr[i]` con `arr[mayor]`, y llamar recursivamente a `siftDown(mayor, n)` para seguir bajando el elemento mientras siga siendo necesario.

**Traza visual de `siftDown(0, 5)` sobre `[5, 50, 40, 20, 30]`**

```
Estado inicial:  [5, 50, 40, 20, 30]
                  ↑
                  i=0 (valor 5)

       5  ←
      / \
    50   40
    / \
   20  30

Paso 1: hijos en 1 y 2. Comparar 5, 50, 40 → mayor es 50 (en posición 1).
        Intercambiar arr[0] ↔ arr[1].

Estado:  [50, 5, 40, 20, 30]

      50
      / \
     5   40   ←  ahora i=1
    / \
   20  30

Paso 2: hijos de 1 son 3 y 4. Comparar 5, 20, 30 → mayor es 30 (en posición 4).
        Intercambiar arr[1] ↔ arr[4].

Estado:  [50, 30, 40, 20, 5]

      50
      / \
     30  40
    / \
   20  5    ←  ahora i=4 (hoja)

Paso 3: hijos de 4 estarían en 9 y 10, fuera del heap. Termina.

Resultado:  [50, 30, 40, 20, 5]   max-heap correcto ✅
```

**Coste de `siftDown`**

En el peor caso, el elemento cae desde la raíz hasta una hoja. Como el árbol es completo y tiene `n` nodos, su altura es **`log₂ n`**. Cada paso del recorrido es O(1) (tres comparaciones y un intercambio). Total: **O(log n)**.

### 4. Construir un heap a partir de un array desordenado

Tenemos un array cualquiera y queremos convertirlo en un max-heap. Hay dos formas de hacerlo.

**Estrategia ingenua: insertar uno a uno**

Empezar con un heap vacío e ir añadiendo elementos uno a uno, restaurando la propiedad después de cada inserción. Cada inserción cuesta O(log n). Total: **O(n log n)**.

**Estrategia óptima: heapificación de abajo arriba**

Partimos del array entero como un "candidato a heap" que viola la propiedad por todas partes, y aplicamos `siftDown` desde el último nodo no-hoja hacia la raíz.

Las hojas (la mitad de los nodos) ya cumplen trivialmente la propiedad (no tienen hijos), así que no hay que tocarlas. El primer nodo que sí tiene hijos es el de índice `(n / 2) - 1`. Aplicamos `siftDown` allí, después en `(n/2) - 2`, y así hacia atrás hasta `0`.

```
para i desde (n/2 - 1) hasta 0:
    siftDown(i, n)
```

**Coste de la construcción**

Aquí ocurre algo sorprendente. A primera vista parece O(n log n) (n llamadas a siftDown, cada una O(log n)). Pero en realidad es **O(n)**, gracias a un detalle sutil: la mayoría de los nodos están cerca de las hojas, donde `siftDown` apenas hace trabajo. Solo unos pocos nodos están cerca de la raíz, donde `siftDown` es costoso. La suma total resulta lineal.

No hace falta que demuestres esto en clase, pero conviene mencionarlo: **construir un heap es O(n)**, no O(n log n).

**Traza: convertir `[4, 10, 3, 5, 1]` en max-heap**

```
Array inicial: [4, 10, 3, 5, 1]

Visualización:
        4 (i=0)
       / \
      10  3   (i=1, i=2)
     / \
    5   1     (i=3, i=4)

Empezamos en (5/2) - 1 = 1.

siftDown(1, 5):
    Nodo: 10. Hijos: 5 y 1. Mayor: 10 (sí mismo).
    No hay intercambio. Termina.

Estado: [4, 10, 3, 5, 1]   (no cambia)

siftDown(0, 5):
    Nodo: 4. Hijos: 10 y 3. Mayor: 10 (en pos 1).
    Intercambio arr[0] ↔ arr[1]:
    Estado: [10, 4, 3, 5, 1]

         10
         / \
        4   3
       / \
      5   1

    Recursivamente, siftDown(1, 5):
        Nodo: 4. Hijos: 5 y 1. Mayor: 5 (en pos 3).
        Intercambio arr[1] ↔ arr[3]:
        Estado: [10, 5, 3, 4, 1]

             10
             / \
            5   3
           / \
          4   1

        Recursivamente, siftDown(3, 5):
            Nodo: 4. Hijos serían posiciones 7 y 8, fuera. Termina.

Heap final: [10, 5, 3, 4, 1]   ✅
```

### 5. El algoritmo de ordenación

Ya tenemos las dos piezas: la operación `siftDown` y la construcción del heap. Ahora _heapsort_ sigue una idea muy elegante:

> **Si el máximo está siempre en la raíz, y la raíz vive en `arr[0]`, entonces lo único que tengo que hacer es sacar el máximo, ponerlo al final del array, encoger el heap y reorganizar la raíz. Repetir n veces.**

**Las dos fases del algoritmo**

**Fase 1: convertir el array en max-heap.** Aplicar la heapificación de abajo arriba descrita en la sección 4. Coste: O(n).

**Fase 2: extraer el máximo repetidamente.** Hacer `n - 1` veces:

1. Intercambiar `arr[0]` (el máximo actual) con `arr[i]`, donde `i` es el último índice del heap. El máximo queda colocado en su posición final del array ordenado.
2. Reducir el tamaño del heap en uno (ahora `i` queda fuera del heap).
3. Aplicar `siftDown(0, nuevoTamaño)` para restaurar la propiedad de heap. La raíz tenía un valor que vino del fondo del heap, así que probablemente viole la propiedad y haya que hacerlo "caer".

Cada iteración de la fase 2 es O(log n) por el `siftDown`. Las `n - 1` iteraciones suman O(n log n).

**Pseudocódigo completo**

```
heapsort(arr):
    n = arr.length

    // Fase 1: construir el max-heap
    para i desde (n/2 - 1) hasta 0:
        siftDown(arr, i, n)

    // Fase 2: extraer el máximo repetidamente
    para i desde n-1 hasta 1:
        intercambiar arr[0] con arr[i]
        siftDown(arr, 0, i)
```

Solo seis líneas conceptuales. Toda la complejidad está en la operación `siftDown`.

**¿Por qué se usa max-heap si queremos orden ascendente?**

Es la pregunta más natural y conviene responderla. Un max-heap nos permite ir **sacando el máximo en cada iteración**. Si los vamos colocando desde el **final** del array hacia el principio, el resultado es un array ordenado ascendentemente:

```
Iteración 1: el máximo va a la posición n-1 (el mayor al final)
Iteración 2: el siguiente máximo va a n-2
...
Iteración n-1: el segundo menor va a la posición 1
              (el menor queda solo en la posición 0)
```

Si quisieras orden descendente, usarías min-heap y la misma lógica.

### 6. Traza completa: ordenando `[4, 10, 3, 5, 1]`

Reusamos el heap construido en la sección 4: `[10, 5, 3, 4, 1]`.

Notación: el separador `|` indica el límite del heap. A su derecha quedan los elementos ya ordenados.

```
Tras Fase 1:    [10, 5, 3, 4, 1 |]    heap completo, tamaño 5

──────────────────────────────────────
Iteración 1:  intercambio arr[0] ↔ arr[4]
              [1, 5, 3, 4 | 10]   heap tamaño 4
              siftDown(0, 4):
                  nodo 1, hijos 5 y 3 → mayor 5 (pos 1)
                  intercambio arr[0] ↔ arr[1]:
                  [5, 1, 3, 4 | 10]
                  siftDown(1, 4):
                      nodo 1, hijo 4 (pos 3, sin hijo derecho dentro del heap)
                      → mayor 4
                      intercambio arr[1] ↔ arr[3]:
                      [5, 4, 3, 1 | 10]
                      siftDown(3, 4): pos 3 sin hijos, termina.

──────────────────────────────────────
Iteración 2:  intercambio arr[0] ↔ arr[3]
              [1, 4, 3 | 5, 10]   heap tamaño 3
              siftDown(0, 3):
                  nodo 1, hijos 4 y 3 → mayor 4 (pos 1)
                  intercambio arr[0] ↔ arr[1]:
                  [4, 1, 3 | 5, 10]
                  siftDown(1, 3): pos 1 sin hijos en el heap reducido, termina.

──────────────────────────────────────
Iteración 3:  intercambio arr[0] ↔ arr[2]
              [3, 1 | 4, 5, 10]   heap tamaño 2
              siftDown(0, 2):
                  nodo 3, hijo 1 (sin hijo derecho dentro del heap)
                  → mayor 3 (sí mismo). Termina.

──────────────────────────────────────
Iteración 4:  intercambio arr[0] ↔ arr[1]
              [1 | 3, 4, 5, 10]   heap tamaño 1
              siftDown(0, 1): pos 0 sin hijos en el heap reducido, termina.

──────────────────────────────────────

Resultado final: [1, 3, 4, 5, 10]   ✅
```

Pinta este recorrido a mano la primera vez. La parte más difícil es seguir cómo se "encoge" el heap en cada iteración mientras la zona ordenada crece desde el final.

### 7. Análisis de complejidad

**Coste por fases**

| Fase                          | Coste              |
| ----------------------------- | ------------------ |
| Construcción del max-heap     | O(n)               |
| n - 1 extracciones del máximo | (n − 1) · O(log n) |
| **Total**                     | **O(n log n)**     |

La fase 2 domina la complejidad total. La fase 1, aunque sorprendentemente sea O(n), no cambia el orden asintótico.

**Garantía en todos los casos**

Una propiedad muy valiosa: _heapsort_ es **O(n log n) en el mejor, medio y peor caso**. No tiene casos malignos como _quicksort_. La estructura del heap garantiza el coste sin importar el contenido del array.

**Comparación con los otros algoritmos eficientes**

| Aspecto            | _Merge sort_ | _Quicksort_          | _Heapsort_ |
| ------------------ | ------------ | -------------------- | ---------- |
| Mejor caso         | O(n log n)   | O(n log n)           | O(n log n) |
| Caso medio         | O(n log n)   | O(n log n)           | O(n log n) |
| Peor caso          | O(n log n)   | **O(n²)**            | O(n log n) |
| Espacio extra      | O(n)         | O(log n) (recursión) | **O(1)**   |
| Estable            | Sí           | No                   | No         |
| In-place           | No           | Sí                   | Sí         |
| Velocidad práctica | Buena        | **Muy buena**        | Buena      |

_Heapsort_ es la opción "robusta": no es el más rápido en la práctica (quicksort suele ganarle por la mejor utilización de la caché del procesador y la menor constante), pero es el único que garantiza simultáneamente **O(n log n) en todos los casos** y **espacio O(1)**. Por eso se usa en sistemas donde el peor caso importa: drivers, kernels, código embebido.

### 8. Propiedades de _heapsort_

**In-place: sí**

Toda la reorganización ocurre dentro del propio array. La memoria adicional es solo la pila de llamadas recursivas de `siftDown`, que tiene profundidad O(log n) en el peor caso. Si se implementa `siftDown` iterativamente, el espacio adicional es **O(1)** estricto.

**Estable: no**

Durante los intercambios de la fase 2, dos elementos iguales pueden cambiar su orden relativo respecto al array original. Si necesitas estabilidad, usa _merge sort_.

**Adaptativo: no**

Detectar que el array ya está ordenado no le ayuda. La fase de construcción del heap se hace siempre, sin importar el orden inicial.

**Resumen**

| Propiedad         | _Heapsort_         |
| ----------------- | ------------------ |
| Mejor caso        | O(n log n)         |
| Caso medio        | O(n log n)         |
| Peor caso         | O(n log n)         |
| Espacio adicional | O(log n) recursivo |
|                   | O(1) iterativo     |
| Estable           | No                 |
| In-place          | Sí                 |
| Adaptativo        | No                 |

### 9. Implementarlo tú mismo: guía de decisiones

**Estructura general**

Vas a necesitar tres métodos:

* `siftDown(arr, i, n)`: la operación fundamental, que hace caer el nodo en posición `i` mientras el heap tiene tamaño `n`.
* `buildMaxHeap(arr)`: convierte un array desordenado en max-heap usando `siftDown`.
* `heapsort(arr)`: orquesta las dos fases del algoritmo.

**Implementación de `siftDown`**

Tienes dos opciones: recursiva o iterativa. La recursiva es más limpia y traduce el pseudocódigo casi línea a línea; la iterativa es marginalmente más eficiente y usa O(1) de espacio (cero pila).

Pasos:

1. Calcular las posiciones de los hijos: `izq = 2*i + 1`, `der = 2*i + 2`.
2. Encontrar el mayor entre `arr[i]`, `arr[izq]` (si `izq < n`) y `arr[der]` (si `der < n`). Guarda el índice del mayor en una variable.
3. Si el mayor es el propio `i`: termina.
4. Si no: intercambia `arr[i]` con `arr[mayor]` y llama recursivamente (o continúa el bucle) con `i = mayor`.

**Implementación de `buildMaxHeap`**

Un solo bucle desde `(n/2) - 1` hasta `0` (descendente, inclusive 0) que llama a `siftDown(arr, i, n)` en cada iteración.

**Implementación de `heapsort`**

Llamar a `buildMaxHeap`, después un bucle desde `n-1` hasta `1` que en cada iteración intercambia `arr[0]` con `arr[i]` y llama a `siftDown(arr, 0, i)`.

**Errores típicos al implementarlo**

* **Confundir `2*i + 1` con `2*i` para el hijo izquierdo**. La fórmula correcta para arrays con índice 0 es `2*i + 1`. Si lo tomas mal, todo el heap se desbarata.
* **Olvidar comprobar los límites en `siftDown`**. Si el hijo derecho está fuera del heap (`der >= n`), no existe y no se debe consultar `arr[der]`. Si lo haces, leerás basura o lanzarás `IndexOutOfBoundsException`.
* **Empezar el bucle de `buildMaxHeap` en `n/2` en vez de `n/2 - 1`**. La diferencia es que `n/2` es la primera hoja, no el último nodo no-hoja. Si lo confundes, te ahorras una llamada importante.
* **Olvidar reducir el tamaño del heap en la fase 2**. Si `siftDown` siempre se llama con `n` original, el elemento ya colocado al final volvería a entrar en el heap y arruinarías la ordenación. La llamada correcta es `siftDown(arr, 0, i)`, no `siftDown(arr, 0, n)`.
* **Usar `<` en vez de `>` al comparar (o viceversa)**. Si te equivocas en la dirección, construyes un min-heap en lugar de un max-heap, y la ordenación sale al revés.

**Pruébalo siempre con casos límite**

* Array vacío y de un elemento.
* Array ya ordenado ascendente.
* Array ordenado descendente.
* Array con todos los elementos iguales.
* Array con números negativos.

***

### 10. Ejercicios

**Ejercicio 1 — Implementar `siftDown`** _**(básico)**_

Implementa la operación `siftDown` siguiendo los pasos de la sección 3. Pruébala con casos preparados a mano: un array que ya es max-heap excepto por un nodo "caído" en alguna posición.

```
arr antes:   [5, 50, 40, 20, 30]   (5 está mal en la raíz)
siftDown(arr, 0, 5)
arr después: [50, 30, 40, 20, 5]
```

**Firma:**

```
private static void siftDown(int[] arr, int i, int n)
```

> _Pista:_ sigue al pie de la letra los cuatro pasos. Hazlo recursivamente la primera vez (es más fácil de razonar) y, si te queda tiempo, escribe también la versión iterativa con un `while`.

***

**Ejercicio 2 — Implementar `buildMaxHeap`** _**(básico)**_

Una vez tengas `siftDown` funcionando, implementa la heapificación de abajo arriba.

```
arr antes:   [4, 10, 3, 5, 1]
buildMaxHeap(arr)
arr después: [10, 5, 3, 4, 1]   (un max-heap válido)
```

**Firma:**

```
private static void buildMaxHeap(int[] arr)
```

> _Pista:_ un solo bucle. Empieza en `(n/2) - 1` y baja hasta `0` (incluido). Llama a `siftDown(arr, i, n)` en cada iteración. Tres líneas.

***

**Ejercicio 3 — Implementar `heapsort`** _**(básico)**_

Combina las dos operaciones anteriores en el algoritmo final.

```
heapsort([4, 10, 3, 5, 1])  →  [1, 3, 4, 5, 10]
heapsort([])                 →  []
heapsort([42])               →  [42]
heapsort([3, 3, 3])         →  [3, 3, 3]
```

**Firma:**

```
public static void heapsort(int[] arr)
```

> _Pista:_ primero `buildMaxHeap(arr)`. Después un bucle desde `n - 1` hasta `1` (inclusive 1) que en cada iteración hace dos cosas: intercambiar `arr[0]` con `arr[i]`, y llamar `siftDown(arr, 0, i)`. Cuatro o cinco líneas.

***

**Ejercicio 4 — Verificación con `assert`** _**(básico)**_

Después de la fase 1 de `heapsort`, escribe una función `esMaxHeap(int[] arr)` que devuelva `true` si el array cumple la propiedad de max-heap, `false` en caso contrario. Llámala justo después de `buildMaxHeap` para comprobar que tu construcción es correcta.

**Firma:**

```
public static boolean esMaxHeap(int[] arr)
```

> _Pista:_ recorre el array desde `i = 0` hasta el último nodo no-hoja. Para cada `i`, comprueba que `arr[i] >= arr[2*i+1]` (si el hijo izquierdo existe) y `arr[i] >= arr[2*i+2]` (si el hijo derecho existe). Si alguna comprobación falla, devuelve `false`. Si todas pasan, `true`.
>
> Esta función es muy útil como herramienta de depuración: te permite saber en qué iteración rompes el invariante.

***

**Ejercicio 5 — Los k mayores de un array&#x20;**_**(medio)**_

Dado un array y un entero `k`, devuelve los `k` elementos más grandes (sin que importe el orden entre ellos).

```
kMayores([7, 2, 8, 1, 9, 3, 5, 4], 3)  →  [9, 8, 7]
kMayores([1, 2, 3, 4, 5], 2)           →  [5, 4]
```

**Firma:**

```
public static int[] kMayores(int[] arr, int k)
```

> _Pista:_ la solución obvia es ordenar todo el array y coger los últimos `k`. Eso es O(n log n).
>
> Pero hay una solución más eficiente: construye un max-heap del array (O(n)) y haz solo `k` extracciones del máximo (O(k log n)). Total: **O(n + k log n)**, que es mejor que O(n log n) cuando `k` es pequeño respecto a `n`.
>
> Para `n = 1 000 000` y `k = 10`, la mejora es de un factor 10⁶ aproximadamente.

***

**Ejercicio 6 — Cola de prioridad casera&#x20;**_**(reto)**_

Un **heap binario** sirve como base para implementar una **cola de prioridad**: una estructura donde insertas elementos con una prioridad y siempre puedes extraer el de mayor prioridad rápidamente.

Implementa una clase `MaxPriorityQueue` con dos métodos:

* `add(int valor)`: añade un elemento al final del heap y lo "sube" mientras sea mayor que su padre (operación llamada `siftUp`).
* `extractMax()`: devuelve y elimina el máximo, restaurando la propiedad con `siftDown`.

Ambas operaciones deben ser O(log n).

```java
MaxPriorityQueue pq = new MaxPriorityQueue();
pq.add(5); pq.add(10); pq.add(3); pq.add(8);
pq.extractMax()  →  10
pq.extractMax()  →  8
pq.extractMax()  →  5
pq.extractMax()  →  3
```

> _Pista:_ internamente usa un `int[]` que crezca dinámicamente (o un `ArrayList<Integer>`) que actúe como heap. La operación `siftUp` es la simétrica de `siftDown`: dado un elemento en posición `i`, comparas con su padre `(i-1)/2`, e intercambias mientras sea mayor que él. La complejidad es O(log n) porque la altura del árbol está acotada.
>
> Esta es la estructura que está detrás de `java.util.PriorityQueue`. Implementarla a mano una vez te ayuda a entender lo que pasa por dentro de la biblioteca.
