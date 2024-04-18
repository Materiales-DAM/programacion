---
cover: ../../.gitbook/assets/quality-assurance-code-bug.jpg
coverY: 110.50526315789473
layout:
  cover:
    visible: true
    size: full
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

# Errores de compilación

Los errores de compilación son problemas que ocurren durante el proceso de compilación de un programa de software. La compilación es el proceso mediante el cual el código fuente escrito por un programador se traduce a un lenguaje de bajo nivel (como código máquina) que la computadora puede entender y ejecutar.

Cuando se produce un error de compilación, significa que el compilador no pudo traducir el código fuente a un programa ejecutable debido a algún problema detectado durante el proceso de compilación. Estos problemas pueden variar en gravedad, desde errores sintácticos simples hasta problemas más complejos relacionados con la lógica del programa.

Aquí hay algunas categorías comunes de errores de compilación:

1. **Errores de sintaxis:** Estos ocurren cuando el código fuente no sigue las reglas gramaticales del lenguaje de programación. Por ejemplo, faltar un punto y coma al final de una línea, usar una palabra clave reservada como nombre de variable, o escribir mal un operador.
2. **Errores semánticos:** Estos ocurren cuando el código fuente es gramaticalmente correcto pero tiene un significado lógico incorrecto. Por ejemplo, sumar una cadena de caracteres y un número entero sin convertir primero la cadena en un número.
3. **Errores de tipo:** Estos ocurren cuando se intenta usar una variable o una función de un tipo incorrecto en una operación. Por ejemplo, intentar sumar un número entero con una cadena de caracteres.
4. **Errores de declaración:** Estos ocurren cuando se hace referencia a una variable o una función que no ha sido declarada previamente en el programa.

Cuando se encuentra un error de compilación, el compilador generalmente proporciona un mensaje de error que indica la naturaleza del problema y la ubicación dentro del código fuente donde ocurrió el error. Los programadores utilizan estos mensajes de error para identificar y corregir los problemas en su código antes de intentar compilarlo nuevamente.

<table data-full-width="false"><thead><tr><th width="299.5">Error</th><th>Descripción</th></tr></thead><tbody><tr><td>error: cannot find symbol</td><td><p>Causas:</p><p>- Se está intentando usar una variable que no existe, está mal escrita o no está en el scope</p><p>- Se está intentando usar una clase que no está importada o no existe</p></td></tr><tr><td>error: ';' expected</td><td>Falta el ; al final de una sentencia.</td></tr><tr><td>error: ')' expected</td><td>Falta un cierre de paréntesis en alguna estructura sintáctica</td></tr><tr><td>unclosed string literal</td><td>No se ha cerrado un String por ejemplo: String saludo = "hola;</td></tr><tr><td>illegal start of an expression</td><td>Es uno de los mensajes de error más difíciles de interpretar, suele ocurrir porque la estructura del programa no es correcta.</td></tr><tr><td>incompatible types</td><td><p>Causas:</p><p>- Se está intentando devolver un valor de un tipo que no corresponde con el return type del método</p><p>- Se está intentando invocar un método pasando algún parámetro con el tipo equivocado</p><p>- Se intenta asignar un valor de un tipo a una variable de otro tipo</p></td></tr><tr><td>method &#x3C;X> in class &#x3C;Y> cannot be applied to given types;</td><td>Se está invocando un método con un número de parámetros equivocado.</td></tr><tr><td>missing return statement</td><td>Ocurre cuando tenemos un método cuyo return type no es void y hay alguna rama de ejecución que no define un return</td></tr><tr><td>reached end of file while parsing</td><td>Faltan uno o varios cierres de llaves al final de la clase</td></tr><tr><td>unreachable statement</td><td><p>Hay alguna sentencia que nunca se va a ejecutar, esto se puede deber a:</p><p>- Sentencias que estén después de un return</p><p>- Sentencias que estén después de un throw</p><p>- Sentencias condicionales cuya condición nunca se vaya a cumplir</p></td></tr><tr><td>variable &#x3C;X> might not have been initialized</td><td>Ocurre cuando se lee una variable a la que no se le ha asignado valor alguno.</td></tr></tbody></table>

&#x20;
