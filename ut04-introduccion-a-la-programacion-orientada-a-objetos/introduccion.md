---
cover: ../.gitbook/assets/oop.png
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

# Introducción

La programación orientada a objetos (POO o OOP en inglés) es uno de los paradigmas de programación más utilizados en la actualidad.&#x20;

Este paradigma se enmarca dentro de la programación imperativa, en la cual los programas se expresan en secuencias de órdenes (sentencias).&#x20;

Este paradigma supuso una revolución en su día al incluir novedosos conceptos que permitían generar código de mayor calidad, facilitar el desarrollo y reutilizar el código de una forma más sencilla

Algunos lenguajes de programación orientada a objetos son:

* Java
* C#
* C++
* Go
* Kotlin
* Y mucho más

### Programación estructurada vs orientada a objetos

La manera de programar que hemos visto hasta ahora se enmarcaría en el paradigma de programación estructurada. En dicho paradigma, los datos y los procedimientos están separados y sin relación, ya que lo único que se busca es el procesamiento de unos datos de entrada para obtener otros de salida. En la programación estructurada prima el concepto de procedimientos o funciones sobre el de estructuras (se emplean principalmente funciones que procesan datos).

Sin embargo, en el paradigmo POO, los datos y los procedimientos se encuentran entrelazados y conformando un conjunto. En este paradigma, primero se definen las estructuras y luego sus métodos.

## Conceptos fundamentales

### Clases

Las clases son el elemento básico de este paradigma. Una clase describe un conjunto de variables relacionadas y un conjunto de operaciones que se pueden realizar sobre ellos. Podemos ver una clase como una plantilla que nos permite representar objetos que representan instancias de entidades de un mismo tipo. Las clases se componen de:

* **Campos**: son cada uno de los atributos que componen los objetos de esta clase&#x20;
* **Constructores**: Son métodos que sirven para crear objetos de esta clase
* **Métodos**: Además de los constructores, se pueden definir métodos vinculados a los objetos que realicen algún tipo de cálculo, operación o modificación sobre los datos del objeto.

### Objetos

Una vez definida una clase, podemos crear instancias de la misma llamados objetos. Cada objeto almacena un conjunto los valores concretos que tiene asignados a través de sus campos.

Por ejemplo, si definimos la clase Persona:

<figure><img src="../.gitbook/assets/image (3) (1) (1).png" alt=""><figcaption></figcaption></figure>

En la clase Persona definimos que toda perona tiene los siguientes campos:

* nombrePersona
* primerApellido
* segundoApellido
* fechaNacimiento

SI se deasea crear un objeto de tipo Persona, se deben proveer valores conretos para esos campos.



```java
// La variable person1 almacena un objeto de tipo Persona
Persona person1 = new Persona("Bob", "Esponja", "De Mar", "23-11-2000");


// La variable person2 almacena otro objeto de tipo Persona
Persona person2 = new Persona("Peppa", "Pig", "UK", "2-12-2001");
```
