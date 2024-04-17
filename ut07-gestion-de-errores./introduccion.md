---
cover: ../.gitbook/assets/quality-assurance-code-bug.jpg
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

# Introducción

Durante el desarrollo de un programa, van a surgir múltiples problemas, en algunos casos, dichos problemas provocarán un error. En otras ocasiones, los problemas permanecerán ocultos hasta que sean detectados sin provocar ningún error.

Dependiendo el momento en el que se produce un error, podemos clasificarlos de la siguiente manera:

## Errores en tiempo de **compilación**

Están vinculados a fallos en la codificación del programa. Estos fallos pueden deberse a una sintaxis errónea, a problemas semánticos, etc...  No es posible ejecutar un programa hasta que no se hayan solucionado todos los errores de compilación.

## Errores en tiempo de **ejecución** (excepciones):

Las excepciones ocurren durante la ejecución del programa y pueden provocar que el programa se detenga inesperadamente. Dentro de las excepciones, podemos diferenciar unas de otras dependiendo de la causas:

#### Excepciones provocadas por una mala codificación (**bugs**):

Son excepciones cuya causa es una mala codificación, este tipo de excepciones se pueden evitar corrigiendo el código erróneo (bug)

#### Excepciones provocados por **factores externos no controlado**s

Otras excepciones se producen por eventos sobre los que no tenemos control en nuestro código. Por ejemplo, si se llena el disco duro del ordenador, se cae la conexión a internet...
