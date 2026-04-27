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

# Ordenación por selección

### 1. La idea

Imagina que tienes un montón de cromos desordenados y quieres ordenarlos por número. ¿Qué harías instintivamente? Probablemente algo así: buscas el cromo con el número más bajo de todo el montón, lo sacas y lo pones primero. Luego buscas el más bajo de los que quedan, lo sacas y lo pones segundo. Y así hasta terminar.

Eso es exactamente la ordenación por selección:

1. **Busca el menor elemento** de todo el array.
2. **Intercámbialo** con el que está en la primera posición.
3. Ahora el primero ya está en su sitio definitivo. Repite lo mismo con el resto del array (desde la segunda posición en adelante).

En cada pasada, un elemento más queda colocado. Tras `n-1` pasadas, todo está ordenado.

<figure><img src="../../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

#### ¿En qué se diferencia de la burbuja?

La burbuja trabaja con **pares adyacentes**: va intercambiando vecinos hasta que el mayor burbujea al final. Hace muchos intercambios pequeños.

La selección trabaja con **el mínimo global del subarray**: busca primero, intercambia una sola vez, y el elemento queda colocado definitivamente. Hace pocas escrituras pero muchas comparaciones.

|                           | Burbuja                       | Selección                   |
| ------------------------- | ----------------------------- | --------------------------- |
| Busca...                  | Pares adyacentes desordenados | El mínimo del resto         |
| Intercambios por pasada   | Muchos (potencialmente)       | Exactamente uno             |
| El elemento que se coloca | El **mayor** (al final)       | El **menor** (al principio) |

### 2. Traza paso a paso

Ordenamos `[29, 10, 14, 37, 13]` ascendente.

**Pasada 1**: buscar el mínimo de todo el array `[29, 10, 14, 37, 13]`.

| Comparamos con | ¿Nuevo mínimo? | Mínimo actual |
| -------------- | -------------- | ------------- |
| 29 (inicio)    | —              | 29 (pos 0)    |
| 10             | Sí, 10 < 29    | 10 (pos 1)    |
| 14             | No, 14 > 10    | 10 (pos 1)    |
| 37             | No, 37 > 10    | 10 (pos 1)    |
| 13             | No, 13 > 10    | 10 (pos 1)    |

Mínimo: 10 en posición 1. Intercambiamos posición 0 y posición 1:

```
[29, 10, 14, 37, 13]  →  [10 | 29, 14, 37, 13]
                            ✓
```

**Pasada 2**: buscar el mínimo del resto `[29, 14, 37, 13]` (posiciones 1 a 4).

| Comparamos con | ¿Nuevo mínimo? | Mínimo actual |
| -------------- | -------------- | ------------- |
| 29 (inicio)    | —              | 29 (pos 1)    |
| 14             | Sí             | 14 (pos 2)    |
| 37             | No             | 14 (pos 2)    |
| 13             | Sí             | 13 (pos 4)    |

Mínimo: 13 en posición 4. Intercambiamos posición 1 y posición 4:

```
[10 | 29, 14, 37, 13]  →  [10, 13 | 14, 37, 29]
 ✓    ✓
```

**Pasada 3**: buscar el mínimo de `[14, 37, 29]` (posiciones 2 a 4).

Mínimo: 14 en posición 2. Ya está en su sitio: el intercambio es consigo mismo (no pasa nada).

```
[10, 13 | 14, 37, 29]  →  [10, 13, 14 | 37, 29]
 ✓   ✓    ✓
```

**Pasada 4**: buscar el mínimo de `[37, 29]` (posiciones 3 a 4).

Mínimo: 29 en posición 4. Intercambiamos posición 3 y posición 4:

```
[10, 13, 14 | 37, 29]  →  [10, 13, 14, 29 | 37]
 ✓   ✓   ✓    ✓
```

El último elemento queda colocado automáticamente. Resultado final:

```
[10, 13, 14, 29, 37]   ✅
```

**Observaciones clave de la traza:**

* Hemos hecho **4 pasadas** para 5 elementos (siempre `n-1`).
* Hemos hecho **4 intercambios** como máximo (uno por pasada, siempre `n-1`). Con la burbuja habrían sido potencialmente muchos más.
* En la pasada 3, el mínimo ya estaba en su sitio. El intercambio se produce igualmente (consigo mismo), pero no cambia nada. Podríamos optimizarlo con un `if`, pero no cambia la complejidad.

### 3. El algoritmo descompuesto

Antes de escribir el código completo, fíjate en que la selección se compone de **dos operaciones** que ya conocéis:

**Operación 1: encontrar la posición del mínimo** en un subarray. Esto ya lo sabéis hacer desde el primer tema de arrays.

```java
// Buscar la posición del mínimo desde 'desde' hasta el final
public static int posicionMinimo(int[] arr, int desde) {
    int posMin = desde;
    for (int j = desde + 1; j < arr.length; j++) {
        if (arr[j] < arr[posMin]) {
            posMin = j;
        }
    }
    return posMin;
}
```

**Operación 2: intercambiar dos elementos** de un array. Esto ya lo visteis con la burbuja.

```java
public static void intercambiar(int[] arr, int i, int j) {
    int tmp = arr[i];
    arr[i] = arr[j];
    arr[j] = tmp;
}
```

La ordenación por selección no es más que **aplicar estas dos operaciones repetidamente**: para cada posición `i`, busca el mínimo del resto y ponlo en `i`.

### 4. Implementación en Java

```java
public static void seleccion(int[] arr) {
    int n = arr.length;

    for (int i = 0; i < n - 1; i++) {
        // Buscar la posición del mínimo en arr[i..n-1]
        int posMin = i;
        for (int j = i + 1; j < n; j++) {
            if (arr[j] < arr[posMin]) {
                posMin = j;
            }
        }

        // Intercambiar arr[i] con arr[posMin]
        int tmp = arr[i];
        arr[i] = arr[posMin];
        arr[posMin] = tmp;
    }
}
```

Entender cada pieza:

* **Bucle externo** (`i`): recorre las posiciones de izquierda a derecha. En cada iteración, la posición `i` recibirá su elemento definitivo. Llega hasta `n-2` porque el último elemento queda colocado solo.
* **Bucle interno** (`j`): busca el mínimo desde `i+1` hasta el final. Empieza en `i+1` porque `posMin` ya se inicializa a `i`.
* **Intercambio**: coloca el mínimo encontrado en la posición `i`. Si `posMin == i`, se intercambia consigo mismo (inofensivo).

#### El invariante

Tras cada iteración del bucle externo se cumple:

> Los elementos de `arr[0]` a `arr[i]` están ordenados y son los menores del array. Ningún elemento de `arr[i+1..n-1]` es menor que `arr[i]`.

Este invariante es lo que garantiza que el algoritmo es correcto. Cada pasada extiende la zona ordenada en una posición.

### 5. Análisis

#### Comparaciones

El bucle interno siempre recorre el subarray restante completo, independientemente de los datos:

```
Pasada 1: n-1 comparaciones
Pasada 2: n-2 comparaciones
...
Pasada n-1: 1 comparación

Total = (n-1) + (n-2) + ... + 1 = n·(n-1)/2
```

Esto es **O(n²) siempre**. No hay mejor caso ni peor caso para las comparaciones: la selección mira todo el subarray restante en cada pasada, da igual si el array ya está ordenado o no.

#### Intercambios

Exactamente **n-1 intercambios**: uno por pasada, ni más ni menos. Este es el punto fuerte de la selección frente a la burbuja:

|           | Comparaciones | Intercambios (peor caso) |
| --------- | ------------- | ------------------------ |
| Burbuja   | n·(n-1)/2     | n·(n-1)/2                |
| Selección | n·(n-1)/2     | n-1                      |

Mismas comparaciones, pero la selección hace muchos menos intercambios. Si mover datos es caro (registros grandes, escrituras en disco), la selección es preferible.

#### Memoria

**O(1)**. Solo usa una variable auxiliar para el intercambio. Es _in-place_.

#### Estabilidad

**No es estable.** El intercambio a distancia puede alterar el orden relativo de elementos iguales. Veamos un ejemplo concreto:

```
Array: [3a, 2, 3b]    (3a y 3b son dos "3" distintos)

Pasada 1: mínimo es 2 (pos 1). Intercambiamos pos 0 y pos 1:
[2, 3a, 3b]  →  [2, 3a, 3b]   ... espera, este sale bien.

Probemos otro: [5, 3a, 3b, 1]

Pasada 1: mínimo es 1 (pos 3). Intercambiamos pos 0 y pos 3:
[1, 3a, 3b, 5]   ← correcto hasta aquí

Pasada 2: mínimo de [3a, 3b, 5] es 3a (pos 1). Se queda.
[1, 3a, 3b, 5]   ← orden relativo de 3a y 3b preservado
```

El contraejemplo más claro:

```
[2a, 2b, 1]

Pasada 1: mínimo es 1 (pos 2). Intercambiamos pos 0 y pos 2:
[1, 2b, 2a]

2b ahora está ANTES que 2a. En el original, 2a estaba antes.
El orden relativo de los dos "2" se ha invertido. → NO estable.
```

Esto importa en la práctica cuando ordenas objetos por una clave: si dos alumnos tienen la misma nota y quieres que conserven el orden original, la selección no te lo garantiza.

#### Adaptabilidad

**No es adaptativa.** Siempre hace exactamente las mismas comparaciones, esté el array como esté. Un array ya ordenado tarda exactamente lo mismo que uno al revés. La burbuja (con flag) y la inserción sí aprovechan los datos parcialmente ordenados; la selección no.

#### Tabla comparativa actualizada

| Algoritmo     | Mejor     | Medio     | Peor      | Memoria  | Estable | Adaptativa    |
| ------------- | --------- | --------- | --------- | -------- | ------- | ------------- |
| Burbuja       | O(n)      | O(n²)     | O(n²)     | O(1)     | Sí      | Sí (con flag) |
| **Selección** | **O(n²)** | **O(n²)** | **O(n²)** | **O(1)** | **No**  | **No**        |
| Inserción     | O(n)      | O(n²)     | O(n²)     | O(1)     | Sí      | Sí            |

### 6. ¿Cuándo tiene sentido usar selección?

En la práctica profesional, casi nunca. `Arrays.sort` siempre será mejor. Pero hay dos situaciones donde tiene una ventaja real:

**Cuando el coste de escribir/mover es muy superior al de leer/comparar.** En dispositivos con memoria flash (donde las escrituras desgastan las celdas), minimizar intercambios alarga la vida del hardware. La selección garantiza como máximo `n-1` escrituras.

**Cuando necesitas los `k` menores elementos.** Si solo necesitas encontrar los 3 menores de un array de 1000, puedes hacer 3 pasadas de selección y parar. Es O(k·n), mejor que ordenar todo el array con O(n log n) cuando `k` es muy pequeño.

***

### 7. Ejercicios

#### Ejercicio 1 — Selección descendente _(básico)_

Implementa una versión de la selección que ordene **de mayor a menor**.

```
entrada:  [3, 1, 4, 1, 5, 9, 2, 6]
salida:   [9, 6, 5, 4, 3, 2, 1, 1]
```

**Firma:**

```java
public static void seleccionDescendente(int[] arr)
```

> _Pista:_ en lugar de buscar el mínimo en cada pasada, busca el **máximo**. Solo cambia la condición del `if` dentro del bucle interno.

***

#### Ejercicio 2 — Contar comparaciones e intercambios _(básico)_

Modifica la selección para que cuente por separado el número de **comparaciones** y el número de **intercambios** realizados. Devuelve ambos valores en un `int[2]`.

Ejecútalo con estos arrays y anota los resultados:

```
[1, 2, 3, 4, 5]        ← ya ordenado
[5, 4, 3, 2, 1]        ← ordenado al revés
[3, 1, 4, 1, 5, 9]     ← aleatorio
```

**Firma:**

```java
public static int[] seleccionConContadores(int[] arr)
// devuelve {comparaciones, intercambios}
```

> _Pista:_ una comparación es cada ejecución de `if (arr[j] < arr[posMin])`. Un intercambio es cada ejecución del bloque de intercambio. Verás que las comparaciones son **siempre las mismas** (n·(n-1)/2) independientemente del array: esa es la diferencia clave con la burbuja optimizada, que puede hacer menos comparaciones si el array ya está casi ordenado.

***

#### Ejercicio 3 — Selección con intercambio condicional _(básico)_

En la versión básica, siempre hacemos el intercambio aunque `posMin == i` (el mínimo ya está en su sitio). Modifica la selección para que **solo intercambie cuando sea necesario** (`posMin != i`). Usa el ejercicio 2 para verificar que el número de intercambios se reduce en algunos casos.

```
[1, 5, 3, 2, 4]
Sin optimización: 4 intercambios
Con optimización: 3 intercambios (pasada 1 se ahorra porque 1 ya está al principio)
```

**Firma:**

```java
public static void seleccionOptimizada(int[] arr)
```

> _Pista:_ un solo `if` antes del intercambio. Sencillo, pero reflexiona: ¿cambia esto la complejidad temporal? ¿Y la complejidad en número de comparaciones?

***

#### Ejercicio 4 — Ordenar Strings por longitud _(medio)_

Ordena un array de `String` usando selección, pero el criterio de ordenación es la **longitud** de la cadena (de más corta a más larga). En caso de empate en longitud, mantén el orden en que aparecen (intenta hacerlo... y descubre que **no puedes garantizarlo** con selección. Explica por qué).

```
entrada:  ["casa", "yo", "sol", "a", "ventana"]
salida:   ["a", "yo", "sol", "casa", "ventana"]

entrada:  ["bb", "aa", "cc"]  (las tres de longitud 2)
salida:   el orden podría alterarse → selección NO lo garantiza
```

**Firma:**

```java
public static void seleccionPorLongitud(String[] arr)
```

> _Pista:_ donde antes comparabas `arr[j] < arr[posMin]`, ahora comparas `arr[j].length() < arr[posMin].length()`. El código apenas cambia. La pregunta de reflexión sobre la estabilidad es lo importante: ¿por qué la selección no puede garantizar que `"bb"` y `"aa"` mantengan su orden original si tienen la misma longitud?

***

#### Ejercicio 5 — Encontrar los k menores _(medio)_

Dado un array y un número `k`, devuelve un array con los `k` elementos **más pequeños**, ordenados. No ordenes todo el array: haz solo `k` pasadas de selección y para.

```
kMenores([7, 10, 4, 3, 20, 15], 3)  →  [3, 4, 7]
kMenores([5, 1, 3], 1)              →  [1]
kMenores([5, 1, 3], 3)              →  [1, 3, 5]
```

**Firma:**

```java
public static int[] kMenores(int[] arr, int k)
```

> _Pista:_ ejecuta el bucle externo de la selección solo `k` veces en lugar de `n-1` veces. Después, copia las primeras `k` posiciones del array a un nuevo array y devuélvelo.
>
> Reflexiona: ¿cuál es la complejidad de esta solución? ¿Es mejor que ordenar todo el array con selección y quedarte con los primeros `k`?

***

#### Ejercicio 6 — Selección sobre posiciones pares e impares _(medio-difícil)_

Ordena un array de forma que las **posiciones pares** (0, 2, 4...) contengan los valores en orden **ascendente** y las **posiciones impares** (1, 3, 5...) contengan los valores en orden **descendente**, rellenando primero las pares con los menores y las impares con los mayores.

```
entrada:    [5, 3, 8, 1, 4, 7, 2, 6]
pares  (↑): posiciones 0,2,4,6 reciben los 4 menores ordenados: 1,2,3,4
impares(↓): posiciones 1,3,5,7 reciben los 4 mayores ordenados al revés: 8,7,6,5
salida:     [1, 8, 2, 7, 3, 6, 4, 5]
```

**Firma:**

```java
public static void ordenarParImpar(int[] arr)
```

> _Pista:_ primero ordena el array completo con selección (o cualquier método). Luego construye el array resultado distribuyendo los menores en posiciones pares y los mayores en posiciones impares. Es un ejercicio de manipulación de arrays que usa la selección como herramienta.

***

#### Ejercicio 7 — Demostrar la inestabilidad _(reto conceptual)_

Este ejercicio no es de código sino de razonamiento. Dado el siguiente array de objetos:

```java
// Alumnos con nombre y nota
Alumno[] alumnos = {
    new Alumno("Ana", 7),
    new Alumno("Luis", 5),
    new Alumno("María", 7),
    new Alumno("Pedro", 5)
};
```

**Parte A:** ejecuta mentalmente (o en papel) la ordenación por selección usando la **nota** como criterio ascendente. Escribe el array resultante indicando el nombre de cada alumno.

**Parte B:** comprueba si los alumnos con la misma nota mantienen su orden original. ¿Ana sigue antes que María? ¿Luis sigue antes que Pedro?

**Parte C:** repite el ejercicio usando la **burbuja** como algoritmo. ¿Los empates se resuelven igual o distinto?

**Parte D:** explica con tus propias palabras por qué la selección no es estable y la burbuja sí.

> _Pista:_ la clave está en la diferencia entre **intercambio a distancia** (selección) e **intercambio de adyacentes** (burbuja). Cuando intercambias a distancia, puedes "saltar" por encima de un elemento igual, alterando su orden relativo. Los intercambios de adyacentes nunca cruzan elementos iguales (porque la condición es `>` estricto, no `>=`).
