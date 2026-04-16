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

# Algoritmos de ordenación

Ordenar una colección consiste en reorganizar sus elementos según un criterio determinado: de menor a mayor, alfabéticamente, por fecha, por prioridad... Es una de las operaciones más antiguas y estudiadas de la informática, y conviene entender por qué le dedicamos tanto tiempo.

**Ordenar es habilitar otras operaciones.** La búsqueda binaria, que es exponencialmente más rápida que la lineal, **solo funciona sobre datos ordenados**. Detectar duplicados, calcular medianas, agrupar elementos iguales, mezclar dos colecciones o encontrar los `k` mayores se vuelven triviales cuando los datos están ordenados, y costosos cuando no lo están.

No es casualidad que los grandes proveedores de _cloud_ cobren por operaciones de ordenación a gran escala, que las bases de datos inviertan enormes esfuerzos en índices ordenados, o que Java incluya ordenación en su biblioteca estándar (`Arrays.sort`, `Collections.sort`).

## Cómo se evalúa un algoritmo de ordenación

Dos algoritmos que producen el mismo resultado final pueden ser muy distintos. Algunas propiedades de los algoritmos de ordenación que vamos a comparar:

* **Complejidad temporal.** Cuántas operaciones realiza en función del tamaño `n` de la entrada. Se suele distinguir entre el **mejor caso** (entrada más favorable), el **caso medio** y el **peor caso**. Un buen algoritmo tiene peor caso aceptable; uno "peligroso" tiene buen caso medio pero un peor caso catastrófico.
* **Complejidad espacial.** Cuánta memoria adicional necesita, aparte del propio array de entrada. Un algoritmo que ordena "in situ" (**in-place**) apenas usa memoria extra; otros necesitan arrays auxiliares.
* **Estabilidad.** Un algoritmo es **estable** si, cuando dos elementos tienen la misma clave de ordenación, mantiene entre ellos el orden original. Importa cuando se ordena por varios criterios sucesivos: si ordenas una lista de alumnos por nota y luego por nombre, la estabilidad garantiza que, a igualdad de nombre, se conserve el orden por nota.
* **Adaptabilidad.** Un algoritmo es **adaptativo** si aprovecha que los datos ya estén parcialmente ordenados para terminar antes. La inserción lo es; la selección no.

## Principales algoritmos de ordenación

| Algoritmo  | Mejor      | Medio      | Peor       | Memoria  | Estable | In-place |
| ---------- | ---------- | ---------- | ---------- | -------- | ------- | -------- |
| Burbuja    | O(n)       | O(n²)      | O(n²)      | O(1)     | Sí      | Sí       |
| Selección  | O(n²)      | O(n²)      | O(n²)      | O(1)     | No      | Sí       |
| Inserción  | O(n)       | O(n²)      | O(n²)      | O(1)     | Sí      | Sí       |
| Merge sort | O(n log n) | O(n log n) | O(n log n) | O(n)     | Sí      | No       |
| Quicksort  | O(n log n) | O(n log n) | O(n²)      | O(log n) | No      | Sí       |
| Heapsort   | O(n log n) | O(n log n) | O(n log n) | O(1)     | No      | Sí       |

Los tres primeros son **cuadráticos** y los llamaremos "didácticos": son los que vais a implementar a mano porque enseñan patrones fundamentales. Los tres siguientes son los **eficientes** y los veréis más adelante: son los que usan las bibliotecas reales, incluyendo `Arrays.sort` de Java (que combina variantes de quicksort y merge sort internamente).

#### ¿Por qué empezar por la burbuja si es "la peor"?

Porque es la más intuitiva. Nadie en un curso serio usa burbuja en producción, pero su lógica es tan transparente que permite concentrarnos en el **pensamiento algorítmico** —invariantes, pasadas, optimizaciones, análisis de coste— sin que la complejidad del algoritmo en sí nos distraiga. Una vez dominada, las demás ordenaciones son variaciones sobre el mismo tema.
