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

# Ventana desliza

La **ventana deslizante** es una técnica para resolver problemas sobre arrays o cadenas en los que necesitamos calcular algo sobre un **subrango contiguo** (una "ventana") que se va moviendo por la estructura.

La idea clave: en lugar de recalcular todo el subrango cada vez que nos movemos una posición, **reutilizamos el cálculo anterior**, quitando lo que sale por la izquierda y sumando lo que entra por la derecha.

Esto reduce la complejidad típica de `O(n·k)` o `O(n²)` a **`O(n)`**.

<figure><img src="../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

#### Analogía

Imagina que miras por la ventanilla de un tren: no ves todo el paisaje a la vez, solo un trozo. A medida que el tren avanza, por un lado aparece algo nuevo y por el otro desaparece algo antiguo. No necesitas "mirar de nuevo" todo lo que ya habías visto.

## ¿Cuándo aplicarla?

Busca estas señales en el enunciado:

* "Subarray / subcadena **contigua**..."
* "...de tamaño **k**" → ventana de tamaño fijo.
* "...la más larga / más corta que cumpla X" → ventana de tamaño variable.
* "Máximo / mínimo / suma / promedio" sobre subrangos.

Si el problema requiere subrangos **no contiguos** (por ejemplo, elegir cualesquiera k elementos), esta técnica **no** aplica.

## Variantes

| Tipo         | Tamaño                              | Ejemplo                                 |
| ------------ | ----------------------------------- | --------------------------------------- |
| **Fija**     | `k` conocido de antemano            | Suma máxima de 3 elementos consecutivos |
| **Variable** | Crece y decrece según una condición | Subcadena más larga sin repetidos       |

***

## Ejemplo resuelto: suma máxima de k elementos consecutivos

**Problema:** Dado un array de enteros y un número `k`, encontrar la suma máxima de `k` elementos **consecutivos**.

```
array = [2, 1, 5, 1, 3, 2],  k = 3
Ventanas posibles:
  [2, 1, 5] = 8
  [1, 5, 1] = 7
  [5, 1, 3] = 9   ← máxima
  [1, 3, 2] = 6
Resultado: 9
```

#### Solución ingenua — O(n·k)

```java
public static int sumaMaximaIngenua(int[] arr, int k) {
    int max = Integer.MIN_VALUE;
    for (int i = 0; i <= arr.length - k; i++) {
        int suma = 0;
        for (int j = i; j < i + k; j++) {
            suma += arr[j];              // Recalculamos toda la ventana
        }
        max = Math.max(max, suma);
    }
    return max;
}
```

Para cada posición recorremos `k` elementos → `O(n·k)`. Ineficiente.

#### Solución con ventana deslizante — O(n)

La clave: al mover la ventana una posición a la derecha, la nueva suma es:

```
sumaNueva = sumaAnterior - arr[i-k] + arr[i]
            (quitamos el que sale)  (añadimos el que entra)
```

```java
public static int sumaMaximaVentana(int[] arr, int k) {
    if (arr.length < k) {
        throw new IllegalArgumentException("k mayor que el tamaño del array");
    }

    // 1) Suma de la primera ventana
    int sumaVentana = 0;
    for (int i = 0; i < k; i++) {
        sumaVentana += arr[i];
    }

    int max = sumaVentana;

    // 2) Deslizar la ventana: desde k hasta el final
    for (int i = k; i < arr.length; i++) {
        sumaVentana += arr[i] - arr[i - k];  // entra arr[i], sale arr[i-k]
        max = Math.max(max, sumaVentana);
    }

    return max;
}
```

#### Traza paso a paso (`[2, 1, 5, 1, 3, 2]`, `k = 3`)

| i | Entra | Sale | sumaVentana       | max |
| - | ----- | ---- | ----------------- | --- |
| - | -     | -    | 2+1+5 = **8**     | 8   |
| 3 | 1     | 2    | 8 + 1 - 2 = **7** | 8   |
| 4 | 3     | 1    | 7 + 3 - 1 = **9** | 9   |
| 5 | 2     | 5    | 9 + 2 - 5 = **6** | 9   |

Resultado: **9** ✅

Cada elemento entra y sale de la ventana exactamente una vez → **O(n)**.

***

## Plantilla general

#### Ventana fija

```java
int suma = 0;
// Primera ventana
for (int i = 0; i < k; i++) suma += arr[i];
int resultado = suma;

// Deslizar
for (int i = k; i < arr.length; i++) {
    suma += arr[i] - arr[i - k];
    resultado = Math.max(resultado, suma); // o min, o lo que toque
}
```

#### Ventana variable (dos punteros)

```java
int ini = 0;
int acumulado = 0;
int resultado = 0;

for (int fin = 0; fin < arr.length; fin++) {
    // 1) Expandir: añadir arr[fin] al estado
    acumulado += arr[fin];

    // 2) Contraer mientras la ventana NO sea válida
    while (/* condición de invalidez */) {
        acumulado -= arr[ini];
        ini++;
    }

    // 3) Actualizar el resultado con la ventana actual [ini..fin]
    resultado = Math.max(resultado, fin - ini + 1);
}
```

***

## Ejercicios

Se presentan de menor a mayor dificultad. Intenta resolverlos antes de mirar las pistas.

#### Ejercicio 1 — Promedios de tamaño k _(fácil)_

Dado un array `double[]` y un entero `k`, devuelve un array con el promedio de cada ventana contigua de tamaño `k`.

```
arr = [1, 3, 2, 6, -1, 4, 1, 8, 2],  k = 5
salida = [2.2, 2.8, 2.4, 3.6, 2.8]
```

**Firma:**

```java
public static double[] promediosVentana(double[] arr, int k)
```

> _Pista:_ idéntico al ejemplo resuelto, pero guarda cada promedio en el array de salida en vez de quedarte con el máximo.

***

#### Ejercicio 2 — Número de subarrays con suma exactamente k _(medio)_

Dado un array de enteros **no negativos** y un entero `k`, cuenta cuántos subarrays contiguos suman exactamente `k`.

```
arr = [1, 1, 1],  k = 2  →  2
arr = [2, 1, 4, 1, 1, 1, 2],  k = 4  →  3
```

**Firma:**

```java
public static int contarSubarraysSuma(int[] arr, int k)
```

> _Pista:_ ventana variable. Como los elementos son no negativos, la suma crece al expandir y decrece al contraer. Mantén dos punteros `ini` y `fin`, y cuando la suma se pase de `k`, contrae por la izquierda.
>
> _Atención:_ si el array pudiera tener negativos, la ventana deslizante **no** funciona directamente; habría que usar un `HashMap` de sumas acumuladas.

***

#### Ejercicio 3 — Subcadena más larga sin caracteres repetidos _(medio)_

Dada una cadena, devuelve la **longitud** de la subcadena más larga que no contenga ningún carácter repetido.

```
"abcabcbb"  →  3   ("abc")
"bbbbb"     →  1   ("b")
"pwwkew"    →  3   ("wke")
```

**Firma:**

```java
public static int subcadenaMasLargaSinRepetidos(String s)
```

> _Pista:_ ventana variable con un `HashSet<Character>` (o un `HashMap<Character, Integer>` con la última posición vista). Cuando aparece un repetido, contrae la ventana desde `ini` hasta que deje de haber conflicto.

***

#### Ejercicio 4 — Subarray más corto con suma ≥ objetivo _(difícil)_

Dado un array de enteros **positivos** y un entero `objetivo`, devuelve la **longitud mínima** de un subarray contiguo cuya suma sea ≥ `objetivo`. Si no existe, devuelve `0`.

```
arr = [2, 3, 1, 2, 4, 3],  objetivo = 7  →  2   ([4, 3])
arr = [1, 1, 1, 1],        objetivo = 10 →  0
```

**Firma:**

```java
public static int subarrayMinimoSuma(int[] arr, int objetivo)
```

> _Pista:_ ventana variable que **se expande** con `fin` hasta alcanzar el objetivo, y entonces **se contrae** por `ini` mientras siga cumpliendo la condición, guardando la longitud mínima vista.

***

#### Ejercicio 5 — Máximo en cada ventana de tamaño k _(reto)_

Dado un array y un entero `k`, devuelve un array con el **máximo** de cada ventana de tamaño `k`.

```
arr = [1, 3, -1, -3, 5, 3, 6, 7],  k = 3
salida = [3, 3, 5, 5, 6, 7]
```

**Firma:**

```java
public static int[] maximoPorVentana(int[] arr, int k)
```

> _Pista:_ hay una solución trivial en `O(n·k)`. La solución óptima en `O(n)` usa un **`Deque<Integer>`** (doble cola) que guarda **índices** en orden decreciente de valor. Al entrar un elemento nuevo, quitas por la cola todos los índices cuyo valor sea menor; al avanzar la ventana, descartas por el frente el índice si ya queda fuera.
>
> Este ejercicio es un clásico de entrevistas técnicas.ç
