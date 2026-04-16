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

# Introducción

Un **algoritmo** es una secuencia finita y ordenada de instrucciones que, partiendo de unos datos de entrada, resuelve un problema produciendo una salida.&#x20;

No es un concepto exclusivo de la informática: una receta de cocina, las instrucciones para montar un mueble o el procedimiento para resolver una ecuación de segundo grado son algoritmos. Lo que caracteriza a un algoritmo bien formado son cinco propiedades:

* **Finitud:** termina tras un número finito de pasos.
* **Precisión:** cada instrucción está definida sin ambigüedad.
* **Entrada:** acepta cero o más datos iniciales.
* **Salida:** produce uno o más resultados.
* **Eficacia:** cada paso es realizable en un tiempo razonable con los medios disponibles.

Cuando un algoritmo se traduce a un lenguaje de programación concreto —Java, Python, C#— obtenemos un **programa**. El mismo algoritmo puede implementarse en muchos lenguajes, igual que la misma receta puede escribirse en castellano, en inglés o en forma de vídeo: lo esencial es la lógica, no el idioma.

## Clasificación por propósito

Aquí agrupamos por qué problema resuelven:

* **Algoritmos de búsqueda:** localizan un elemento dentro de una colección. Ejemplos: búsqueda lineal, búsqueda binaria.
* **Algoritmos de ordenación:** reorganizan los elementos de una colección según un criterio. Ejemplos: burbuja, inserción, selección, _merge sort_, _quicksort_.
* **Algoritmos de recorrido:** visitan sistemáticamente todos los elementos de una estructura. Imprescindibles en árboles y grafos (BFS, DFS), pero también en formas básicas al recorrer un array.
* **Algoritmos numéricos y matemáticos:** cálculo de primos, máximo común divisor, potencias, conversiones de base, operaciones sobre matrices.
* **Algoritmos de cadenas:** manipulación y análisis de texto: palíndromos, anagramas, búsqueda de subcadenas.
* **Algoritmos de optimización:** buscan la mejor solución según algún criterio (mínimo coste, máximo beneficio). Ejemplos clásicos: el camino más corto en un mapa, la mochila óptima.
* **Algoritmos criptográficos:** cifrado, firma digital, _hashing_ seguro. Ejemplos: AES, RSA, SHA-256.
* **Algoritmos de compresión:** reducen el tamaño de los datos sin perder información (o con pérdida controlada). Ejemplos: Huffman, LZ77.

## Clasificación por técnica de diseño

Aquí agrupamos por **cómo** se aborda el problema. Esta clasificación resulta más útil a medio plazo, porque reconocer la técnica adecuada es lo que permite resolver problemas nuevos.

**Fuerza bruta.** Probar todas las posibilidades hasta encontrar la solución. Fácil de escribir, raramente eficiente, pero es la referencia de corrección contra la que se comparan las demás. Ejemplo: búsqueda lineal, comprobar si un número es primo dividiéndolo por todos los anteriores.

**Divide y vencerás.** Dividir el problema en subproblemas más pequeños del mismo tipo, resolverlos recursivamente y combinar las soluciones. Ejemplos: búsqueda binaria, _merge sort_, _quicksort_.

**Algoritmos voraces (**_**greedy**_**).** Toman en cada paso la decisión que parece localmente óptima, confiando en que la concatenación de decisiones locales óptimas lleve a una solución globalmente buena. No siempre funciona, pero cuando lo hace es muy eficiente. Ejemplo: dar cambio con el menor número de monedas (en sistemas monetarios "bien diseñados").

**Programación dinámica.** Cuando un problema tiene subproblemas solapados, se resuelven una sola vez y se almacena el resultado para reutilizarlo. Transforma algoritmos exponenciales en polinómicos. Ejemplo canónico: Fibonacci calculado recursivamente sin memoización (exponencial) frente a la versión con memoización (lineal).

**Backtracking (vuelta atrás).** Exploración sistemática de soluciones candidatas, abandonando (retrocediendo) tan pronto como una rama resulte inviable. Ejemplos: resolver un sudoku, las ocho reinas del ajedrez.

**Algoritmos probabilísticos.** Introducen aleatoriedad en sus decisiones, bien para acelerar el cálculo medio (_quicksort_ con pivote aleatorio), bien porque no se conoce un método determinista eficiente (tests de primalidad de Miller-Rabin).

**Algoritmos aproximados y heurísticos.** Cuando el problema óptimo es intratable en tiempo razonable, se renuncia a la solución perfecta a cambio de una "suficientemente buena". Fundamentales en problemas de optimización reales y, actualmente, en inteligencia artificial.

## Otros criterios de clasificación

Además de los anteriores, se habla de:

* **Iterativos vs. recursivos**, según usen bucles o llamadas a sí mismos.
* **Deterministas vs. no deterministas**, según produzcan siempre la misma salida para la misma entrada o incorporen azar.
* **Secuenciales vs. paralelos/concurrentes**, según ejecuten los pasos uno tras otro o simultáneamente en varios núcleos o máquinas.
* **En línea vs. fuera de línea (**_**online/offline**_**)**, según procesen los datos según llegan o dispongan de ellos íntegramente desde el principio.

