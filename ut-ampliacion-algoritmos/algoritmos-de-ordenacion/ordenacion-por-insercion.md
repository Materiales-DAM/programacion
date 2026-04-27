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

# Ordenación por inserción

### 1. La idea

Piensa en cómo ordenas las cartas cuando juegas. No las tiras todas sobre la mesa para buscar la menor como haría la selección. Tampoco comparas adyacentes una y otra vez como haría la burbuja. Haces algo mucho más natural: **coges una carta nueva y la deslizas entre las que ya tienes en la mano hasta encontrar su sitio**.

Eso es exactamente la ordenación por inserción:

1. Consideras que el primer elemento **ya está ordenado** (un solo elemento siempre lo está).
2. Coges el **siguiente elemento** (el primero de la parte no ordenada).
3. Lo **insertas en la posición correcta** dentro de la parte ya ordenada, desplazando hacia la derecha todos los que sean mayores que él.
4. Repites hasta que no queden elementos sin insertar.

<figure><img src="../../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>

#### ¿En qué se diferencia de las otras dos?

|                           | Burbuja                                       | Selección                               | Inserción                                   |
| ------------------------- | --------------------------------------------- | --------------------------------------- | ------------------------------------------- |
| ¿Qué hace en cada pasada? | Burbujea el mayor al final                    | Busca el mínimo y lo coloca             | Inserta el siguiente en su sitio            |
| Mecanismo de movimiento   | **Intercambio** de adyacentes                 | **Intercambio** a distancia             | **Desplazamiento** (mover hacia la derecha) |
| Dirección del trabajo     | Izquierda → derecha (burbujea hacia el final) | Izquierda → derecha (busca en el resto) | Derecha → izquierda (desplaza hacia atrás)  |

La diferencia fundamental está en el mecanismo. La inserción no intercambia: **desplaza**. Cada elemento mayor que el que estamos insertando se mueve una posición a la derecha para hacerle hueco. Este desplazamiento es más eficiente que múltiples intercambios porque evita la variable temporal repetida.

### 2. Traza paso a paso

Ordenamos `[5, 2, 4, 6, 1, 3]` ascendente.

Convenio visual: la barra `|` separa la parte ya ordenada (izquierda) de la parte por procesar (derecha). El elemento subrayado es el que estamos insertando.

**Estado inicial:**

```
[5 | 2, 4, 6, 1, 3]
 ✓   ← el primer elemento se considera "ordenado"
```

**Pasada 1** — insertamos el `2`:

Comparamos 2 con los elementos de la parte ordenada, de derecha a izquierda:

* 2 < 5 → desplazamos 5 una posición a la derecha.
* No hay más elementos a la izquierda → colocamos 2 en la posición 0.

```
[5 | 2, 4, 6, 1, 3]
   ← 2
[_, 5, 4, 6, 1, 3]    desplazamos 5
[2, 5 | 4, 6, 1, 3]   colocamos 2
```

**Pasada 2** — insertamos el `4`:

* 4 < 5 → desplazamos 5.
* 4 > 2 → paramos. Colocamos 4 en la posición 1.

```
[2, 5 | 4, 6, 1, 3]
       ← 4
[2, _, 5, 6, 1, 3]    desplazamos 5
[2, 4, 5 | 6, 1, 3]   colocamos 4
```

**Pasada 3** — insertamos el `6`:

* 6 > 5 → no desplazamos nada. El 6 ya está en su sitio.

```
[2, 4, 5 | 6, 1, 3]
           ← 6 ya está bien
[2, 4, 5, 6 | 1, 3]
```

Fíjate: **no hemos hecho ninguna operación** en esta pasada. El elemento ya estaba donde debía. Esta es la razón por la que la inserción es rápida con datos casi ordenados.

**Pasada 4** — insertamos el `1`:

* 1 < 6 → desplazamos 6.
* 1 < 5 → desplazamos 5.
* 1 < 4 → desplazamos 4.
* 1 < 2 → desplazamos 2.
* No hay más elementos → colocamos 1 en la posición 0.

```
[2, 4, 5, 6 | 1, 3]
               ← 1
[_, 2, 4, 5, 6, 3]    desplazamos todo
[1, 2, 4, 5, 6 | 3]   colocamos 1
```

Esta es la **pasada más costosa**: el elemento más pequeño tiene que recorrer toda la parte ordenada. Es el peor caso local.

**Pasada 5** — insertamos el `3`:

* 3 < 6 → desplazamos 6.
* 3 < 5 → desplazamos 5.
* 3 < 4 → desplazamos 4.
* 3 > 2 → paramos. Colocamos 3 en la posición 2.

```
[1, 2, 4, 5, 6 | 3]
                 ← 3
[1, 2, _, 4, 5, 6]    desplazamos 4, 5, 6
[1, 2, 3, 4, 5, 6]    colocamos 3
```

Resultado final:

```
[1, 2, 3, 4, 5, 6]   ✅
```

#### Resumen de la traza

| Pasada    | Elemento | Desplazamientos       | Comentario                     |
| --------- | -------- | --------------------- | ------------------------------ |
| 1         | 2        | 1                     | Se coloca al principio         |
| 2         | 4        | 1                     | Se coloca entre 2 y 5          |
| 3         | 6        | 0                     | Ya estaba en su sitio          |
| 4         | 1        | 4                     | Recorre toda la parte ordenada |
| 5         | 3        | 3                     | Se coloca entre 2 y 4          |
| **Total** |          | **9 desplazamientos** |                                |

### 3. Implementación en Java

```java
public static void insercion(int[] arr) {
    for (int i = 1; i < arr.length; i++) {
        int valor = arr[i];          // el elemento a insertar
        int j = i - 1;              // empezamos por el último de la parte ordenada

        // Desplazar hacia la derecha mientras sean mayores que valor
        while (j >= 0 && arr[j] > valor) {
            arr[j + 1] = arr[j];    // desplazamiento (no intercambio)
            j--;
        }

        arr[j + 1] = valor;         // colocar en el hueco que ha quedado
    }
}
```

Vamos a entender cada pieza:

**`int valor = arr[i]`** — Guardamos el elemento a insertar en una variable. Es necesario porque los desplazamientos van a sobreescribir su posición original. Sin esta copia, lo perderíamos.

**`int j = i - 1`** — Empezamos a comparar desde el último elemento de la parte ya ordenada, moviéndonos hacia la izquierda.

**`while (j >= 0 && arr[j] > valor)`** — La condición del bucle comprueba dos cosas: que no nos hayamos salido del array por la izquierda (`j >= 0`) y que el elemento actual sea mayor que el valor a insertar (`arr[j] > valor`). Si alguna de las dos falla, paramos.

**`arr[j + 1] = arr[j]`** — Desplazamos el elemento una posición a la derecha. No es un intercambio: simplemente copiamos. El "hueco" se va moviendo hacia la izquierda.

**`arr[j + 1] = valor`** — Cuando el bucle termina, `j + 1` es la posición donde debe ir el valor. Si terminó porque `j < 0`, el valor va al principio. Si terminó porque `arr[j] <= valor`, va justo después de `arr[j]`.

#### La importancia del `>` estricto

La condición usa `arr[j] > valor`, no `arr[j] >= valor`. Esto significa que si encontramos un elemento **igual** al valor, **no lo desplazamos** y colocamos el nuevo justo después de él. Consecuencia: los elementos iguales conservan su orden original. **Esto es lo que hace a la inserción estable.**

Si cambiáramos `>` por `>=`, el algoritmo seguiría ordenando correctamente, pero dejaría de ser estable.

### 4. Desplazamiento vs. intercambio

Existe una versión alternativa de la inserción que usa **intercambios adyacentes** en lugar de desplazamientos:

```java
// Versión con intercambios (menos eficiente pero más fácil de entender)
public static void insercionConIntercambios(int[] arr) {
    for (int i = 1; i < arr.length; i++) {
        for (int j = i; j > 0 && arr[j] < arr[j - 1]; j--) {
            int tmp = arr[j];
            arr[j] = arr[j - 1];
            arr[j - 1] = tmp;
        }
    }
}
```

Ambas versiones producen el mismo resultado y tienen la misma complejidad O(n²). La diferencia es que cada intercambio hace **3 asignaciones** (con la variable `tmp`), mientras que cada desplazamiento hace **1 sola asignación**. Para arrays grandes, la versión con desplazamientos es aproximadamente **3 veces más rápida** en la práctica.

La versión con intercambios es útil para entender la lógica al principio; la versión con desplazamientos es la que se usa de verdad. Intenta entender ambas y quédate con la segunda.

### 5. Análisis

#### Mejor caso: O(n)

Si el array **ya está ordenado**, cada elemento se compara una sola vez con su predecesor, descubre que ya está en su sitio, y el `while` no ejecuta ninguna iteración. Solo se ejecuta el `for` externo: `n-1` comparaciones, 0 desplazamientos. **Coste lineal.**

```
[1, 2, 3, 4, 5]

i=1: valor=2, arr[0]=1, 1 < 2 → while no entra. 1 comparación, 0 desplazamientos.
i=2: valor=3, arr[1]=2, 2 < 3 → while no entra. 1 comparación, 0 desplazamientos.
i=3: valor=4, arr[2]=3, 3 < 4 → while no entra. 1 comparación, 0 desplazamientos.
i=4: valor=5, arr[3]=4, 4 < 5 → while no entra. 1 comparación, 0 desplazamientos.

Total: 4 comparaciones, 0 desplazamientos.
```

Este es su **gran punto fuerte**: para datos que llegan casi ordenados o que solo tienen unos pocos elementos fuera de sitio, la inserción es la más rápida de las tres ordenaciones cuadráticas, y **puede superar incluso a algoritmos O(n log n)** para arrays pequeños.

#### Peor caso: O(n²)

Si el array está **ordenado al revés**, cada elemento tiene que recorrer toda la parte ordenada:

```
[5, 4, 3, 2, 1]

i=1: valor=4, desplaza 1 elemento.
i=2: valor=3, desplaza 2 elementos.
i=3: valor=2, desplaza 3 elementos.
i=4: valor=1, desplaza 4 elementos.

Total desplazamientos: 1 + 2 + 3 + 4 = 10 = n·(n-1)/2
```

#### Caso medio: O(n²)

Con datos aleatorios, cada elemento se desplaza en promedio la mitad de la parte ordenada. Total: aproximadamente n·(n-1)/4 desplazamientos. Sigue siendo O(n²), pero con la mitad de operaciones que el peor caso.

#### ¿Cuántos desplazamientos son exactamente?

El número total de desplazamientos es igual al **número de inversiones** del array original. Una inversión es un par de posiciones `(i, j)` donde `i < j` pero `arr[i] > arr[j]`: exactamente un par que está en el orden equivocado.

| Array            | Inversiones      | Desplazamientos |
| ---------------- | ---------------- | --------------- |
| \[1, 2, 3, 4, 5] | 0                | 0               |
| \[2, 1, 3, 5, 4] | 2: (2,1) y (5,4) | 2               |
| \[5, 4, 3, 2, 1] | 10               | 10              |

Esto convierte a la inserción en un **algoritmo sensible a las inversiones**: cuanto más ordenado está el array (menos inversiones), menos trabajo hace. Ningún otro algoritmo O(n²) tiene esta propiedad de forma tan directa.

#### Memoria

**O(1)**. Solo usa la variable `valor` y el índice `j`. Es _in-place_.

#### Estabilidad

**Sí, es estable.** Como hemos visto, la condición `arr[j] > valor` (estrictamente mayor) garantiza que los elementos iguales nunca se cruzan. Un elemento se inserta justo **después** del primer igual o menor que encuentra, preservando el orden original entre iguales.

#### Adaptabilidad

**Sí, es la más adaptativa de las tres.** Su rendimiento depende directamente de cuánto desorden tiene el array. Un array "casi ordenado" (pocas inversiones) se ordena en tiempo casi lineal. Esta propiedad es la razón por la que TimSort la usa para fragmentos pequeños.

#### Tabla comparativa final

| Algoritmo     | Mejor    | Medio     | Peor      | Memoria  | Estable | Adaptativa    | Desplazamientos/Intercambios (peor) |
| ------------- | -------- | --------- | --------- | -------- | ------- | ------------- | ----------------------------------- |
| Burbuja       | O(n)     | O(n²)     | O(n²)     | O(1)     | Sí      | Sí (con flag) | n·(n-1)/2 intercambios              |
| Selección     | O(n²)    | O(n²)     | O(n²)     | O(1)     | No      | No            | n-1 intercambios                    |
| **Inserción** | **O(n)** | **O(n²)** | **O(n²)** | **O(1)** | **Sí**  | **Sí**        | **n·(n-1)/2 desplazamientos**       |

La inserción combina lo mejor de las otras dos: es **estable** como la burbuja y tiene **mejor caso O(n)** como la burbuja optimizada, pero además es **adaptativa de verdad** (su coste refleja fielmente el desorden del array, no solo si está perfectamente ordenado o no).

### 6. ¿Dónde se usa la inserción en la vida real?

Más de lo que parece:

**Dentro de TimSort.** Java (`Arrays.sort` para objetos) y Python usan TimSort, que divide el array en fragmentos pequeños llamados _runs_, ordena cada uno con **inserción**, y luego los mezcla con _merge sort_. La inserción se usa para los fragmentos precisamente porque es la más rápida para arrays pequeños y casi ordenados.

**Arrays pequeños.** Para arrays de menos de 10-20 elementos, la inserción es más rápida que _quicksort_ o _merge sort_ por su menor sobrecarga (sin recursión, sin arrays auxiliares). Muchas implementaciones de _quicksort_ cambian a inserción cuando el subarray baja de cierto umbral.

**Datos en tiempo real.** Si recibes datos uno a uno (sensores, eventos de red, logs) y necesitas mantener una colección ordenada, insertar cada nuevo dato en su posición correcta es exactamente lo que hace la inserción. Es O(n) por elemento en el peor caso, pero si los datos llegan aproximadamente en orden, es casi O(1) por elemento.

**Binary insertion sort.** Una variante usa **búsqueda binaria** para encontrar la posición de inserción en O(log n) en lugar de búsqueda lineal. Los desplazamientos siguen siendo O(n) en el peor caso, pero el número de **comparaciones** se reduce a O(n log n) en total. Es útil cuando comparar es caro (por ejemplo, comparar cadenas largas).

***

### 7. Ejercicios

#### Ejercicio 1 — Inserción descendente _(básico)_

Implementa una versión de la inserción que ordene **de mayor a menor**.

```
entrada:  [3, 1, 4, 1, 5, 9, 2, 6]
salida:   [9, 6, 5, 4, 3, 2, 1, 1]
```

**Firma:**

```java
public static void insercionDescendente(int[] arr)
```

> _Pista:_ solo cambia la condición del `while`: en lugar de `arr[j] > valor`, usa `arr[j] < valor`. Ahora desplazas hacia la derecha los que son **menores** que el valor a insertar.

***

#### Ejercicio 2 — Contar desplazamientos _(básico)_

Modifica la inserción para que devuelva el **número total de desplazamientos** realizados. Ejecútalo con estos arrays y compara:

```
[1, 2, 3, 4, 5]        ← ya ordenado: ¿cuántos?
[5, 4, 3, 2, 1]        ← al revés: ¿cuántos?
[2, 1, 3, 5, 4]        ← casi ordenado: ¿cuántos?
```

**Firma:**

```java
public static int insercionConContador(int[] arr)
```

> _Pista:_ un desplazamiento es cada ejecución de `arr[j + 1] = arr[j]`. Verás que para el array ya ordenado el resultado es 0, para el invertido es n·(n-1)/2, y para el casi ordenado es un número bajo. Compara con la selección: ella siempre hace las mismas comparaciones; la inserción se adapta.

***

#### Ejercicio 3 — Insertar en array ordenado _(básico)_

Antes de implementar la inserción completa, practica solo la operación nuclear: dado un array **ya ordenado** y un valor nuevo, inserta el valor en la posición correcta manteniendo el array ordenado. El array tiene una posición extra al final para el nuevo elemento.

```
insertarOrdenado([1, 3, 5, 7, _], 4, 4)  →  [1, 3, 4, 5, 7]
insertarOrdenado([2, 4, 6, _], 3, 1)      →  [1, 2, 4, 6]
insertarOrdenado([2, 4, 6, _], 3, 8)      →  [2, 4, 6, 8]
```

**Firma:**

```java
public static void insertarOrdenado(int[] arr, int longActual, int valor)
// longActual = cuántos elementos hay ya (el array tiene longActual+1 posiciones)
```

> _Pista:_ es exactamente el bucle interno de la inserción aislado. Empiezas desde `j = longActual - 1`, desplazas hacia la derecha mientras `arr[j] > valor`, y colocas `valor` en `j + 1`. Si dominas este ejercicio, dominas la inserción.

***

#### Ejercicio 4 — Ordenar Strings alfabéticamente _(medio)_

Adapta la inserción para ordenar un `String[]` en orden alfabético, sin distinguir mayúsculas de minúsculas.

```
entrada:  ["banana", "Ana", "cereza", "ana", "BANANA"]
salida:   ["Ana", "ana", "banana", "BANANA", "cereza"]
```

Comprueba que la estabilidad se mantiene: `"Ana"` aparece antes que `"ana"` (porque así estaban en el original), y `"banana"` aparece antes que `"BANANA"`.

**Firma:**

```java
public static void insercionStrings(String[] arr)
```

> _Pista:_ usa `compareToIgnoreCase` en lugar de `>`. La condición del while queda: `arr[j].compareToIgnoreCase(valor) > 0`. Reflexiona: ¿por qué `> 0` y no `>= 0`? Porque `>= 0` rompería la estabilidad al desplazar también los iguales.

***

#### Ejercicio 5 — Ordenar alumnos por nota (demostrar estabilidad) _(medio)_

Dada la clase:

```java
public class Alumno {
    String nombre;
    double nota;

    public Alumno(String nombre, double nota) {
        this.nombre = nombre;
        this.nota = nota;
    }
}
```

Ordena un `Alumno[]` por nota **ascendente** usando inserción. Después, verifica la estabilidad: los alumnos con la misma nota deben mantener su orden original.

```
entrada:
  Ana (7), Luis (5), María (7), Pedro (5), Juan (9)

salida:
  Luis (5), Pedro (5), Ana (7), María (7), Juan (9)

  Luis antes que Pedro ✓ (mismo orden original)
  Ana antes que María  ✓ (mismo orden original)
```

**Firma:**

```java
public static void ordenarAlumnos(Alumno[] alumnos)
```

> _Pista:_ la comparación es sobre `alumnos[j].nota > valor.nota`. El desplazamiento mueve objetos `Alumno` completos. Compara el resultado con lo que ocurriría usando selección sobre los mismos datos (ejercicio 7 del tutorial de selección): allí la estabilidad se rompía.

***

#### Ejercicio 6 — Inserción binaria _(medio-difícil)_

Implementa una variante que use **búsqueda binaria** para encontrar la posición de inserción en lugar de comparar elemento a elemento hacia la izquierda. Los desplazamientos siguen siendo los mismos (hay que mover los elementos de todos modos), pero las **comparaciones** se reducen.

```
entrada:  [5, 2, 4, 6, 1, 3]
salida:   [1, 2, 3, 4, 5, 6]
```

**Firma:**

```java
public static void insercionBinaria(int[] arr)
```

> _Pista:_ para cada `i`, en lugar del `while` que compara hacia la izquierda, haz una búsqueda binaria en `arr[0..i-1]` para encontrar la posición `pos` donde debe ir `arr[i]`. Luego desplaza todos los elementos de `arr[pos..i-1]` una posición a la derecha y coloca `arr[i]` en `pos`.
>
> La búsqueda binaria reduce las comparaciones de O(n) a O(log n) por elemento, así que el total de comparaciones baja de O(n²) a O(n log n). Pero los desplazamientos siguen siendo O(n²) en el peor caso, así que la complejidad total sigue siendo O(n²). Sin embargo, si comparar es caro (strings largos, objetos complejos), la mejora es significativa.

***

#### Ejercicio 7 — Casi ordenado _(medio-difícil)_

Un array está **casi ordenado** si cada elemento está a lo sumo a `k` posiciones de su posición final. Por ejemplo, con `k = 2`:

```
[2, 1, 4, 3, 6, 5, 8, 7]   ← cada elemento está a lo sumo 1 posición de su sitio (k=1)
```

Demuestra empíricamente que la inserción ordena estos arrays en **O(n·k)** en lugar de O(n²). Para ello:

**Parte A:** genera arrays "casi ordenados" de distintos tamaños `n` con `k = 5` (desordena cada elemento a lo sumo 5 posiciones de su sitio).

**Parte B:** mide los desplazamientos con tu función del ejercicio 2.

**Parte C:** compara con los desplazamientos para arrays completamente aleatorios del mismo tamaño.

> _Pista:_ para generar un array casi ordenado, parte de un array ordenado y, para cada posición, intercámbialo con una posición aleatoria dentro del rango `[i-k, i+k]`. Verás que los desplazamientos para arrays casi ordenados son aproximadamente `n·k`, muy por debajo del `n²/4` de los aleatorios.
>
> Esta propiedad es la razón por la que TimSort usa inserción: los _runs_ que detecta suelen estar casi ordenados, y la inserción los remata en tiempo casi lineal.

***

#### Ejercicio 8 — Comparativa de las tres ordenaciones cuadráticas _(reto)_

Implementa un programa que mida el tiempo de ejecución de **burbuja (optimizada)**, **selección** e **inserción** sobre los mismos datos, para arrays de tamaño 1 000, 5 000, 10 000 y 50 000 elementos, en tres escenarios:

* Array **ya ordenado**.
* Array **ordenado al revés**.
* Array **aleatorio**.

Presenta los resultados en una tabla y responde:

1. ¿Cuál es la más rápida con datos ya ordenados? ¿Por qué?
2. ¿Cuál es la más rápida con datos al revés? ¿Por qué?
3. ¿Cuál es la más rápida con datos aleatorios? ¿Esperabas ese resultado?
4. ¿A partir de qué tamaño se nota claramente que son O(n²)?

**Firma:**

```java
public static void comparativa()
```

> _Pista:_ usa `System.nanoTime()` para medir. Importante: **copia el array** antes de pasárselo a cada algoritmo para que los tres ordenen los mismos datos. Usa `Arrays.copyOf` para esto. Los resultados te van a sorprender en algunos casos: la inserción con datos ya ordenados será instantánea, y la selección tardará exactamente lo mismo da igual cómo venga el array.
