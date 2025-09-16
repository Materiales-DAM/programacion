---
cover: ../.gitbook/assets/tree.png
coverY: 94.60266666666666
---

# Introducción

Uno de los aspectos fundamentales en el desarrollo de software es el acceso y manipulación de datos. La forma en la que estructuramos los datos tiene un enorme impacto en la facilidad de uso de los mismos. Adaptar las estructuras que usamos para manejar los datos al problema que se está tratando de resolver nos permite resolver los problemas de forma mucho más eficiente.

**Llamamos estructura de datos a una forma de organizar, almacenar y gestionar un conjunto de datos**. Cada estructura de datos está optimizada para un conjunto de operaciones concreto.

La primera gran clasificación de las estructuras de datos hace referencia a la capacidad de las mismas a cambiar de tamaño dinámicamente

* **Estructuras estáticas**: son aquellas que definen su tamaño en el momento de su creación y no tienen la capacidad de aumentar ni disminuir su tamaño. El ejemplo más común de estructuras estáticas es el **array**.

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption><p>Los arrays tienen un tamaño fijo</p></figcaption></figure>

* **Estructuras dinámicas**: son aquellas con la capacidad de aumentar o disminuir su tamaño en función de las necesidades del programa que las está usando. Existe una gran variedad de estructuras dinámicas: **listas enlazadas, árboles binarios.**.

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption><p>Las listas enlazadas pueden cambiar de tamaño</p></figcaption></figure>

### Estructuras estáticas (arrays)

Los arrays son estructuras estáticas, es decir, una vez creadas no pueden cambiar de tamaño. Están optimizados para acceder a cualquier posición en tiempo constante.

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

No resultan muy convenientes cuando la cantidad de datos no se conoce a priori o cuando se quieren realizar búsquedas, ordenaciones, etc... sobre los mismos. Es una de las estructuras más simples y es ampliamente utilizada en diversos problemas.

### Estructuras dinámicas

Existen una gran variedad de estructuras dinámicas, cada estructura está optimizada para realizar un conjunto de operaciones y resulta ineficiente para realizar otras.

No existe una estructura de datos "maestra" que sea la mejor para realizar cualquier operación, sino que cada una tiene sus ventajas e inconvenientes.

## Medir la eficiencia

Para poder elegir la estructura de datos adecuada a cada problema debemos ser capaces de describir cómo de eficiente es una determinada estructura para un problema. La mejor manera de describir la eficiencia es a través de una función matemática que relaciona el tamaño de una estructura de datos con el tiempo que tarda en realizar una determinada operación sobre los mismos.

Existe una notación matemática llamada Big-O que nos facilita la clasificación de la eficiencia de una determinada operación de forma matemática. En esta notación n es el tamaño de los datos alojados en la estructura de datos, y el resultado de la función representa el tiempo que tardará en realizar la operación.

<figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

* **O(1):** también conocida como constante, significa que la operación se ejecuta en un tiempo fijo, independiente de la cantidad de datos que almacene la estructura de datos. Por ejemplo, el acceso a una posición de un array. Las operaciones de complejidad constante son las más eficientes que hay.
* **O(log n):** también conocida como **logarítmica**, el tiempo de ejecución crece conforme aumentan los datos en la estructura, pero la curva se va aplanando conforme aumenta la cantidad de datos. Las operaciones de complejidad logarítmica son muy eficientes.
* **O(n)**: también conocida como **lineal**, el tiempo de ejecución crece de manera proporcional al tamaño de la estructura de datos. Estas operaciones necesitan un escalado de recursos proporcional a la cantidad de datos que se estén procesando. La eficiencia de estas operaciones es aceptable en muchos casos, pero puede llegar a ser problemática si la cantidad de datos crece mucho.
* **O(n log n)**: el tiempo de ejecución crece **algo más a lo proporcional** en este caso. Estas operaciones necesitan un escalado de recursos proporcional a la cantidad de datos que se estén procesando. La eficiencia de estas operaciones es aceptable en muchos casos, pero puede llegar a ser problemática si la cantidad de datos crece mucho.
* **O(n²)**: también conocida como complejidad **cuadrática**. El tiempo de ejecución aumenta mucho más rápido que el tamaño de la estructura y lo hace cada vez más rápido. Las operaciones que tienen esta eficiencia no se adaptan bien cuando los datos son de un cierto tamaño.
* **O(**$$2^n$$**)**: también conocida como **exponencial**. El tiempo de ejecución aumenta a una velocidad aún mayor que la cuadrática, haciendo inviable la operación con tamaños incluso menores. Esta eficiencia es por lo general inaceptable para la resolución de cualquier problema.
* **O(n!)**: también conocida como **factorial**. El tiempo de ejecución aumenta a una velocidad aún mayor que la exponencial, haciendo inviable la operación con tamaños incluso menores.Esta eficiencia es por lo general inaceptable para la resolución de cualquier problema.
