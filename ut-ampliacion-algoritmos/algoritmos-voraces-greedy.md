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

# Algoritmos voraces (greedy)

Un **algoritmo voraz** es el que, ante una secuencia de decisiones, **siempre toma la que parece mejor en ese momento** sin preocuparse de las consecuencias futuras. No recalcula, no deshace, no mira atrás: elige lo que localmente parece óptimo y confía en que eso conduzca a una solución globalmente buena.

La palabra _greedy_ (codicioso, voraz) captura perfectamente la idea: el algoritmo es "avaricioso", coge siempre lo máximo que puede en cada paso.

#### Analogía

Imagina que vas a un buffet libre y quieres llevarte la mayor cantidad posible de comida en un solo plato. Una estrategia voraz sería: en cada momento, coge el trozo más grande que quepa. No te paras a pensar si cogiendo tres piezas medianas cabrían más que una grande. Simplemente coges lo más grande disponible.

A veces esa estrategia funciona perfectamente. Otras veces te deja con un plato lleno de sandía y sin espacio para nada más. Saber **cuándo funciona y cuándo no** es la habilidad que vamos a desarrollar en este tutorial.

## 1. Estructura general

Todo algoritmo voraz sigue este esquema:

```
función voraz(datos):
    ordenar o preparar los datos según el criterio voraz
    solución = vacía

    para cada candidato en datos:
        si el candidato es compatible con la solución actual:
            añadir candidato a la solución

    devolver solución
```

Los tres elementos clave son:

**El criterio voraz**: ¿qué significa "el mejor" en cada paso? ¿El más grande? ¿El más barato? ¿El que termina antes? Elegir bien este criterio es lo que determina si el algoritmo funciona.

**La comprobación de compatibilidad**: ¿puedo añadir este candidato sin violar las restricciones del problema?

**La irreversibilidad**: una vez que tomo una decisión, no la deshago. Esto es lo que hace a los voraces tan rápidos y tan peligrosos a la vez.

## 2. Primer ejemplo: el problema del cambio de monedas

#### Enunciado

Tienes monedas de 1, 2, 5, 10, 20 y 50 céntimos (el sistema monetario europeo), en cantidades ilimitadas. Debes dar un cambio de `C` céntimos usando el **menor número posible de monedas**.

```
C = 73 céntimos
Solución: 50 + 20 + 2 + 1 = 4 monedas
```

#### Estrategia voraz

**Criterio**: en cada paso, coge la moneda más grande que no se pase del importe que queda por dar.

**Intuición**: si puedo cubrir una parte grande del importe con una sola moneda, ¿por qué usar varias pequeñas?

#### Traza paso a paso para `C = 73`

| Paso | Queda por dar | Moneda elegida | Motivo                       |
| ---- | ------------- | -------------- | ---------------------------- |
| 1    | 73            | 50             | La más grande que cabe       |
| 2    | 23            | 20             | La más grande que cabe       |
| 3    | 3             | 2              | 5 no cabe; la siguiente es 2 |
| 4    | 1             | 1              | La única que cabe            |

Resultado: `[50, 20, 2, 1]` → **4 monedas** ✅

#### Implementación en Java

```java
public static List<Integer> cambioMonedas(int cantidad) {
    int[] monedas = {50, 20, 10, 5, 2, 1};  // ordenadas de mayor a menor
    List<Integer> resultado = new ArrayList<>();

    for (int moneda : monedas) {
        while (cantidad >= moneda) {
            resultado.add(moneda);
            cantidad -= moneda;
        }
    }

    return resultado;
}
```

El código es sorprendentemente corto. Esa es una de las señas de identidad de los voraces: suelen ser fáciles de implementar. La dificultad no está en el código, sino en **demostrar que el criterio elegido da la solución correcta**.

#### ¿Por qué funciona con monedas europeas?

Porque el sistema monetario europeo está diseñado de forma que cada moneda es al menos el doble de la anterior (1, 2, 5, 10, 20, 50). Esa propiedad garantiza que usar la moneda más grande posible **nunca es una mala decisión**: no existe una combinación de monedas pequeñas que sea mejor.

#### ¿Y si no funciona?

Cambiemos el sistema de monedas. Supongamos que tenemos monedas de **1, 3 y 4** céntimos, y queremos dar un cambio de **6**.

Estrategia voraz: coge la más grande que quepa.

```
Paso 1: queda 6 → coge 4 → queda 2
Paso 2: queda 2 → 4 no cabe, 3 no cabe → coge 1 → queda 1
Paso 3: queda 1 → coge 1 → queda 0
Resultado voraz: [4, 1, 1] → 3 monedas
```

Pero existe una solución **mejor**: `[3, 3]` → **2 monedas**.

El algoritmo voraz ha fallado. La decisión de coger el 4 parecía buena en el momento, pero nos dejó en una situación donde solo podíamos completar con monedas de 1. Si hubiéramos "aguantado" y cogido un 3, el resultado habría sido mejor.

**Esta es la lección fundamental de los algoritmos voraces: no siempre dan la solución óptima.** Funcionan cuando el problema tiene una propiedad concreta (la _propiedad de elección voraz_), y fallan cuando no la tiene. Distinguir un caso del otro requiere pensar, no simplemente programar.

## 3. Segundo ejemplo: planificación de actividades

#### Enunciado

Tienes una sala y una lista de actividades, cada una con una hora de **inicio** y una hora de **fin**. Dos actividades son **compatibles** si no se solapan (la segunda empieza cuando o después de que termine la primera). Debes seleccionar el **mayor número posible de actividades** compatibles.

```
Actividades:
  A: [1, 3]    (de la hora 1 a la 3)
  B: [2, 5]
  C: [3, 6]
  D: [5, 7]
  E: [6, 8]
  F: [8, 9]
```

#### ¿Cuál es el criterio voraz correcto?

Aquí es donde hay que pensar. Se nos podrían ocurrir varios criterios:

* **La que empieza antes.** Parece lógico: "no pierdas el tiempo, empieza cuanto antes". Pero una actividad que empieza pronto podría durar todo el día y bloquear todas las demás.
* **La más corta.** Así "liberamos" la sala rápido. Pero una actividad corta en medio del día podría impedir colocar dos actividades más largas a los lados.
* **La que termina antes.** Este es el criterio correcto. Al elegir siempre la actividad que libera la sala lo antes posible, maximizamos el tiempo disponible para las siguientes.

La intuición: terminar pronto es lo que deja más hueco para el futuro.

#### Traza paso a paso

Primero ordenamos por hora de fin: A\[1,3], B\[2,5], C\[3,6], D\[5,7], E\[6,8], F\[8,9].

| Paso | Candidata | ¿Compatible con la última seleccionada?        | Decisión        |
| ---- | --------- | ---------------------------------------------- | --------------- |
| 1    | A \[1,3]  | Sí (es la primera)                             | **Seleccionar** |
| 2    | B \[2,5]  | No (empieza en 2, antes de que A termine en 3) | Descartar       |
| 3    | C \[3,6]  | Sí (empieza en 3, A termina en 3)              | **Seleccionar** |
| 4    | D \[5,7]  | No (empieza en 5, antes de que C termine en 6) | Descartar       |
| 5    | E \[6,8]  | Sí (empieza en 6, C termina en 6)              | **Seleccionar** |
| 6    | F \[8,9]  | Sí (empieza en 8, E termina en 8)              | **Seleccionar** |

Resultado: **A, C, E, F → 4 actividades** ✅

Ninguna otra selección consigue más de 4.

#### Implementación en Java

```java
public static List<int[]> planificarActividades(int[][] actividades) {
    // Ordenar por hora de fin (criterio voraz)
    Arrays.sort(actividades, (a, b) -> Integer.compare(a[1], b[1]));

    List<int[]> seleccionadas = new ArrayList<>();
    int finUltima = Integer.MIN_VALUE;

    for (int[] act : actividades) {
        if (act[0] >= finUltima) {          // ¿compatible?
            seleccionadas.add(act);
            finUltima = act[1];             // actualizar el fin de la última seleccionada
        }
    }

    return seleccionadas;
}
```

Fíjate en la estructura: **ordenar según el criterio** + **recorrer tomando lo compatible**. Este es el esqueleto de casi todo algoritmo voraz.

#### Complejidad

Ordenar cuesta O(n log n). El recorrido posterior es O(n). Total: **O(n log n)**, dominado por la ordenación.

Comparado con probar todas las combinaciones posibles de actividades (fuerza bruta), que sería O(2ⁿ), la mejora es gigantesca. Para 30 actividades, fuerza bruta examina más de mil millones de combinaciones; el voraz hace 30 pasos.

## 4. Tercer ejemplo: la mochila fraccionaria

#### Enunciado

Tienes una mochila que soporta como máximo `W` kilos. Hay `n` objetos, cada uno con un **peso** y un **valor**. Puedes llevarte **fracciones** de objetos (puedes cortar un lingote de oro por la mitad, por ejemplo). ¿Cómo maximizas el valor total de lo que te llevas?

```
Capacidad: 15 kg
Objetos:
  A: peso 10 kg, valor 60€  (6€/kg)
  B: peso 5 kg,  valor 50€  (10€/kg)
  C: peso 7 kg,  valor 28€  (4€/kg)
```

#### Criterio voraz

Calcular el **valor por kilo** de cada objeto y coger primero los que tienen mayor ratio. Si no cabe entero, coge la fracción que quepa.

#### Traza

Ordenados por valor/kg: B (10€/kg) > A (6€/kg) > C (4€/kg).

| Paso | Objeto | Valor/kg | Disponible en mochila | Decisión                                      |
| ---- | ------ | -------- | --------------------- | --------------------------------------------- |
| 1    | B      | 10€/kg   | 15 kg                 | Coger entero (5 kg). Queda 10 kg. Valor: 50€  |
| 2    | A      | 6€/kg    | 10 kg                 | Coger entero (10 kg). Queda 0 kg. Valor: +60€ |
| 3    | C      | 4€/kg    | 0 kg                  | No cabe nada                                  |

Resultado: **110€** con 15 kg (B completo + A completo) ✅

Si la mochila fuera de 12 kg:

| Paso | Objeto | Disponible | Decisión                                               |
| ---- | ------ | ---------- | ------------------------------------------------------ |
| 1    | B      | 12 kg      | Entero (5 kg). Queda 7 kg. Valor: 50€                  |
| 2    | A      | 7 kg       | No cabe entero (pesa 10). Coge 7/10 = 70%. Valor: +42€ |

Resultado: **92€** con 12 kg (B completo + 70% de A) ✅

#### Implementación en Java

```java
public static double mochilaFraccionaria(double capacidad, double[] pesos, double[] valores) {
    int n = pesos.length;

    // Crear índices y ordenar por valor/peso descendente
    Integer[] indices = new Integer[n];
    for (int i = 0; i < n; i++) indices[i] = i;
    Arrays.sort(indices, (a, b) -> Double.compare(valores[b] / pesos[b], valores[a] / pesos[a]));

    double valorTotal = 0;

    for (int i : indices) {
        if (capacidad <= 0) break;

        if (pesos[i] <= capacidad) {
            // Cabe entero
            valorTotal += valores[i];
            capacidad -= pesos[i];
        } else {
            // Cabe una fracción
            valorTotal += valores[i] * (capacidad / pesos[i]);
            capacidad = 0;
        }
    }

    return valorTotal;
}
```

#### ¿Por qué funciona?

Porque al poder llevar fracciones, nunca hay "desperdicio". El objeto con mejor ratio siempre aporta más valor por kilo que cualquier otro. No hay forma de que coger más de un objeto peor mejore el resultado: cada kilo de capacidad se gasta en lo más valioso disponible.

#### ¿Cuándo no funciona?

Si los objetos son **indivisibles** (no puedes llevar fracciones: o te llevas el objeto entero o no te lo llevas). Ese es el famoso **problema de la mochila 0/1**, y el voraz **no** da la solución óptima. Ese problema requiere programación dinámica, que veréis en 2º.

## 5. ¿Cuándo funciona un voraz y cuándo no?

Esta es la pregunta más importante del tutorial. No existe una receta universal, pero hay señales:

#### Señales de que un voraz probablemente funciona

**El problema tiene la "propiedad de elección voraz"**: la decisión localmente óptima no cierra el camino a la solución global. En las monedas europeas, coger la moneda más grande nunca impide dar el cambio exacto. En las actividades, coger la que termina antes nunca impide alcanzar el máximo de actividades.

**El problema tiene "subestructura óptima"**: la solución óptima del problema contiene soluciones óptimas de los subproblemas. Si la mejor planificación de actividades incluye la actividad A, entonces el resto de actividades seleccionadas son la mejor planificación para el tiempo que queda tras A.

**Hay un criterio de ordenación natural** que resulta intuitivamente razonable: "el más grande", "el que termina antes", "el de mejor ratio valor/peso".

#### Señales de que un voraz probablemente falla

**Decisiones tempranas condicionan decisiones futuras de forma no obvia.** En el cambio con monedas de {1, 3, 4}, coger la moneda de 4 parece bueno pero impide usar dos monedas de 3. La elección local afecta negativamente a lo global.

**El problema tiene dependencias entre elementos.** Si elegir un objeto afecta al valor o viabilidad de otros de formas complejas, el voraz no puede anticiparlo.

**Existen contraejemplos.** La mejor forma de demostrar que un voraz no funciona es encontrar **un solo caso** donde dé una respuesta subóptima. Si lo encuentras, descártalo.

#### Cómo verificar tu voraz

1. **Piensa un contraejemplo.** Intenta inventar una entrada donde tu criterio falle. Si no encuentras ninguno, puede que funcione.
2. **Compara con fuerza bruta.** Para entradas pequeñas, genera todas las soluciones posibles y comprueba que el voraz siempre da la óptima.
3. **Argumenta informalmente.** ¿Puedes convencerte de que elegir lo localmente óptimo nunca cierra puertas? Si la argumentación es natural, probablemente el voraz es correcto.

En el ámbito profesional y académico, la demostración formal se hace por **contradicción** o por **intercambio** (si hubiera una solución mejor, podrías "intercambiar" una de sus decisiones por la voraz sin empeorar, lo que contradice que fuera mejor). Pero para 1º DAM, los tres pasos de arriba son más que suficientes.

***

## 6. Resumen comparativo

| Ejemplo              | Criterio voraz              | ¿Funciona siempre? | Complejidad |
| -------------------- | --------------------------- | ------------------ | ----------- |
| Cambio (€)           | Moneda más grande que quepa | Sí (con sistema €) | O(n)        |
| Cambio ({1,3,4})     | Moneda más grande que quepa | **No**             | —           |
| Actividades          | La que termina antes        | Sí                 | O(n log n)  |
| Mochila fraccionaria | Mayor valor/peso            | Sí                 | O(n log n)  |
| Mochila 0/1          | Mayor valor/peso            | **No**             | —           |

La tabla deja clara la lección: el mismo tipo de problema (cambio, mochila) puede admitir solución voraz o no, dependiendo de las restricciones concretas.

***

## 7. Ejercicios

#### Ejercicio 1 — Cajero automático _(básico)_

Un cajero automático dispone de billetes de 5, 10, 20 y 50 euros en cantidades ilimitadas. Dada una cantidad a retirar (siempre múltiplo de 5), devuelve la lista de billetes que el cajero entrega usando el **menor número posible** de billetes.

```
retirar(95)   →  [50, 20, 20, 5]   (4 billetes)
retirar(200)  →  [50, 50, 50, 50]  (4 billetes)
retirar(15)   →  [10, 5]           (2 billetes)
retirar(5)    →  [5]               (1 billete)
```

**Firma:**

```java
public static List<Integer> retirar(int cantidad)
```

> _Pista:_ es prácticamente idéntico al ejemplo del cambio de monedas. Cambian los valores de los billetes, pero el criterio voraz y la estructura del código son los mismos.

***

#### Ejercicio 2 — Contraejemplo del cambio _(básico, pero importante)_

Dado un sistema de monedas de **{1, 6, 9}** y una cantidad objetivo de **12**:

**Parte A**: ejecuta mentalmente (o en código) la estrategia voraz (moneda más grande que quepa) y anota el resultado.

**Parte B**: encuentra manualmente una solución con menos monedas.

**Parte C**: responde: ¿qué propiedad del sistema de monedas hace que el voraz falle aquí?

> _Pista:_ ejecuta el voraz y llegarás a un resultado de 4 monedas. Hay una combinación de 2 monedas que da exactamente 12. El voraz no la ve porque toma una decisión temprana que le cierra el camino.

***

#### Ejercicio 3 — Repartir caramelos _(medio)_

Eres profesor y tienes un bote de caramelos de distintos tamaños. Cada alumno tiene una expectativa mínima: solo queda contento si recibe un caramelo de tamaño **igual o mayor** que su expectativa. Cada alumno recibe **como mucho un caramelo**. Quieres maximizar el número de alumnos contentos.

```
expectativas = [1, 3, 4]   (tres alumnos)
caramelos    = [1, 2, 3]   (tres caramelos)

Solución: alumno con expectativa 1 recibe caramelo 1,
          alumno con expectativa 3 recibe caramelo 3.
          Alumno con expectativa 4 no puede ser satisfecho.
          Resultado: 2 alumnos contentos.
```

```
expectativas = [2, 1]
caramelos    = [1, 3, 2]
Resultado: 2 alumnos contentos.
```

**Firma:**

```java
public static int maximoAlumnosContentos(int[] expectativas, int[] caramelos)
```

> _Pista:_ ordena ambos arrays. El criterio voraz es emparejar al alumno con menor expectativa con el caramelo más pequeño que le satisfaga. Así no "desperdicias" caramelos grandes en alumnos fáciles de contentar, reservándolos para los más exigentes.
>
> Recorre ambos arrays con dos punteros. Si el caramelo actual satisface al alumno actual, avanza ambos (emparejados). Si no, avanza solo el puntero de caramelos (ese caramelo es demasiado pequeño para todos los alumnos restantes).

***

#### Ejercicio 4 — Mochila fraccionaria _(medio)_

Implementa el problema de la mochila fraccionaria descrito en la sección 5. Dados `n` objetos con peso y valor, y una capacidad máxima `W`, devuelve el **valor máximo** que se puede transportar, pudiendo llevarse fracciones de objetos.

```
capacidad = 50
objetos:
  peso = [10, 20, 30]
  valor = [60, 100, 120]

Valor/peso: [6, 5, 4]
Solución: objeto 1 entero (10kg, 60€) + objeto 2 entero (20kg, 100€)
        + 2/3 del objeto 3 (20kg, 80€) = 240€
```

**Firma:**

```java
public static double mochilaFraccionaria(double capacidad, double[] pesos, double[] valores)
```

> _Pista:_ calcula el ratio valor/peso de cada objeto, ordena por ratio descendente, y ve cogiendo objetos enteros hasta que no quepa uno más; del último, coge la fracción que quepa.

***

#### Ejercicio 5 — Plataformas de tren _(medio-difícil)_

Dadas las horas de **llegada** y **salida** de `n` trenes a una estación, calcula el **mínimo número de andenes** necesarios para que ningún tren tenga que esperar.

```
llegadas = [9.00, 9.40, 9.50, 11.00, 15.00, 18.00]
salidas  = [9.10, 12.00, 11.20, 11.30, 19.00, 20.00]
Resultado: 3 andenes (a las 9:50, hay 3 trenes simultáneos)
```

**Firma:**

```java
public static int minimoAndenes(double[] llegadas, double[] salidas)
```

> _Pista:_ ordena llegadas y salidas **por separado**. Usa dos punteros (uno para llegadas, otro para salidas). Si la próxima llegada ocurre antes de la próxima salida, necesitas un andén más; si no, se libera uno. Lleva un contador de andenes en uso y quédate con el máximo observado.
>
> El criterio voraz es: procesar los eventos (llegadas y salidas) en orden cronológico y gestionar los recursos según van ocurriendo.

***

#### Ejercicio 6 — Planificación de tareas con plazos _(reto)_

Tienes `n` tareas, cada una con un **beneficio** (lo que ganas si la completas) y un **plazo** (el día límite para completarla, contando desde el día 1). Cada tarea tarda exactamente **un día** y solo puedes hacer una tarea por día. Quieres maximizar el beneficio total.

```
Tareas:
  T1: beneficio 20, plazo día 1
  T2: beneficio 15, plazo día 1
  T3: beneficio 10, plazo día 3
  T4: beneficio 5,  plazo día 1
  T5: beneficio 1,  plazo día 3

Solo puedes hacer una tarea el día 1, una el día 2, una el día 3.

Solución voraz: T1 el día 1, T3 el día 2, T2... no, T2 tiene plazo día 1 y ya pasó.
¿O mejor T1 el día 1, T3 el día 3, y buscar algo para el día 2?
```

**Firma:**

```java
public static int maximoBeneficio(int[] beneficios, int[] plazos)
```

> _Pista:_ ordena las tareas por **beneficio descendente**. Para cada tarea, intenta asignarla al **día más tardío posible** dentro de su plazo que esté libre. Si no hay día libre, descártala. Usa un array de booleanos `diaOcupado[]` para saber qué días están asignados.
>
> La idea de asignar al día más tardío posible es la parte ingeniosa: así reservas los días tempranos para tareas con plazos más ajustados que puedan venir después. Es un voraz que "administra" el recurso escaso (los días) con visión estratégica dentro de su codicia.
