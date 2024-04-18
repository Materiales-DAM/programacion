---
cover: ../../.gitbook/assets/testing.jpg
coverY: 0
layout:
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
---

# Testing

## Pruebas unitarias

El testing unitario es una práctica de desarrollo de software en la que se prueban unidades individuales de código, como métodos o funciones, de forma aislada para verificar que funcionen como se espera. El objetivo principal del testing unitario es validar el comportamiento de cada unidad de código de manera independiente, lo que ayuda a detectar y corregir errores de manera temprana en el proceso de desarrollo.

Aquí hay una explicación detallada del proceso de testing unitario:

1. **Seleccionar la unidad a probar**: La unidad de código a testear puede ser un método, una función, una clase o incluso un componente pequeño del sistema. Es importante elegir unidades de código lo más pequeñas y cohesivas posible para facilitar la prueba y el aislamiento de posibles problemas.
2. **Escribir el caso de prueba**: Se escribe un caso de prueba que ejecute la unidad de código con entradas específicas y verifique el resultado esperado. Este caso de prueba debe cubrir diversos escenarios, incluidos casos normales, casos límite y casos de error.
3. **Preparar el entorno de prueba**: Se configura el entorno de prueba necesario para ejecutar la unidad de código. Esto puede incluir la creación de objetos, la configuración de valores iniciales y la preparación de cualquier dependencia externa, como bases de datos o servicios web, utilizando técnicas como stubs, mocks o fakes.
4. **Ejecutar el caso de prueba**: Se ejecuta el caso de prueba, que llama a la unidad de código con las entradas especificadas y verifica que el resultado sea el esperado.
5. **Evaluar el resultado**: Se evalúa si la unidad de código pasó o falló el caso de prueba. Si falla, se investiga la causa del fallo y se corrige el código correspondiente. Si pasa, se puede considerar la unidad de código como funcionalmente correcta para ese caso de prueba.
6. **Repetir el proceso**: Se repite el proceso para cada unidad de código en el sistema, asegurando que todas estén debidamente probadas y validadas.

### Tipos de casos de prueba

Existen varios tipos de casos de prueba que se utilizan para validar diferentes aspectos del comportamiento de una unidad de código. Algunos de los tipos más comunes de casos de prueba incluyen:

1. **Casos de prueba positivos**: Estos casos de prueba verifican el comportamiento esperado de la unidad de código cuando se le proporcionan entradas válidas. Se aseguran de que la unidad de código produzca el resultado correcto cuando se le proporcionen datos válidos.
2. **Casos de prueba negativos**: Estos casos de prueba prueban cómo responde la unidad de código ante entradas inválidas o inesperadas. Se aseguran de que la unidad de código maneje adecuadamente situaciones de error y no cause fallos o comportamientos inesperados.
3. **Casos de prueba de borde (edge cases)**: Estos casos de prueba evalúan el comportamiento de la unidad de código en los límites de sus valores de entrada. Se prueban valores límite, como el mínimo, el máximo o los valores cercanos a los límites, para garantizar que la unidad de código maneje correctamente estos casos especiales.
4. **Casos de prueba de excepciones**: Estos casos de prueba se centran en probar el manejo de excepciones por parte de la unidad de código. Se aseguran de que la unidad de código lance excepciones cuando sea necesario y de que las excepciones se manejen correctamente en el contexto adecuado.
5. **Casos de prueba de flujo de control (control flow testing)**: Estos casos de prueba se centran en probar diferentes caminos de ejecución dentro de la unidad de código. Se aseguran de que todas las instrucciones y ramificaciones condicionales sean ejecutadas y evaluadas correctamente.
6. **Casos de prueba de rendimiento (performance testing)**: Estos casos de prueba evalúan el rendimiento de la unidad de código en términos de tiempo de ejecución, consumo de memoria u otros recursos. Se aseguran de que la unidad de código cumpla con los requisitos de rendimiento establecidos.
7. **Casos de prueba de integración (integration testing)**: Aunque no son exclusivos del testing unitario, estos casos de prueba se utilizan para probar la interacción entre múltiples unidades de código, verificando que trabajen juntas correctamente.

