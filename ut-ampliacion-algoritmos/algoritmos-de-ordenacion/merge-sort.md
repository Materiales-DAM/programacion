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

# Merge sort

Es un algoritmo de ordenación basado en **divide y vencerás**.

Comparado con lo que habéis visto hasta ahora, _merge sort_ marca un salto cualitativo. Ordenar un millón de elementos con la burbuja requiere aproximadamente medio billón de comparaciones; _merge sort_ lo hace con unos veinte millones, unas 25 000 veces menos.

#### Requisitos previos

Para entender este algoritmo hace falta:

* Manejar con soltura la **recursión**.
* Entender la **técnica de dos punteros** (la operación central del algoritmo la utiliza).
* Tener clara la idea de **complejidad** O(n) vs O(n log n) vs O(n²).

Si alguno de estos tres conceptos aún no está asentado, conviene repasarlo antes de seguir.

### La idea central: divide y vencerás

_Divide y vencerás_ es una estrategia general de diseño de algoritmos con tres fases:

1. **Dividir** el problema en subproblemas más pequeños del mismo tipo.
2. **Vencer** (resolver) cada subproblema, normalmente de forma recursiva. Cuando los subproblemas son triviales, resolvemos directamente: ese es el **caso base**.
3. **Combinar** las soluciones de los subproblemas para obtener la solución del problema original.

Aplicado a la ordenación:

1. **Dividir:** partimos el array en dos mitades.
2. **Vencer:** ordenamos cada mitad _por separado_ (llamada recursiva). El caso base es un array de 0 o 1 elementos, que ya está ordenado.
3. **Combinar:** **mezclamos** las dos mitades ya ordenadas en un único array ordenado.

La idea clave: mezclar dos arrays que **ya están ordenados** es mucho más fácil que ordenar uno desordenado. Esa es la razón por la que el algoritmo funciona y es eficiente.

### 3. El corazón del algoritmo: la operación _merge_

Antes de atacar el algoritmo completo, necesitamos dominar la operación que le da nombre. La operación _merge_ toma **dos arrays que ya están ordenados** y produce un tercer array también ordenado con todos los elementos de ambos.

#### ¿Cómo se mezclan dos arrays ordenados?

Usamos la **técnica de dos punteros**, uno en cada array de entrada. En cada paso:

1. Comparamos los elementos apuntados.
2. Copiamos el **menor** al array resultado.
3. Avanzamos el puntero del array del que acabamos de copiar.
4. Repetimos hasta que uno de los dos arrays se agote.
5. Cuando uno se agota, copiamos los elementos restantes del otro directamente al resultado (ya están ordenados).
