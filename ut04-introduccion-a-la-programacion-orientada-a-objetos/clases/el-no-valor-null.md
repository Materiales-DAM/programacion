---
cover: ../../.gitbook/assets/oop.png
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

# El (no) valor null

Cuando tenemos una variable cuyo tipo es una clase (por ejemplo String, Person...) es posible asignarle el valor null. Este valor significa que no tiene asignado un valor del tipo correspondiente.

Podemos usar el valor null para:

* Campos opcionales
* Cuando no hay resultado para un operación, se puede devolver null. Por ejemplo, calcular el máximo de un array vacío.

## NullPointerException

Esta excepción ocurre cuando se intenta invocar un método de objeto de una variable que tiene valor null.

{% code lineNumbers="true" %}
```java
Student student = null;

if(student.getNif().equals("000000X")) {
    System.out.println(student.getName());
}
```
{% endcode %}

Este código produce un `NullPointerException` en la línea 3, cuando se trata de ejecutar el método getNif() de la variable `student`, ya que dicha variable es `null`.

Esta excepción es la más común en Java y otros lenguajes que no implementan ningún mecanismo de null safety. Para evitar esta excepción debemos comprobar si la variable es null antes de ejecutar el código.

{% code lineNumbers="true" %}
```java
Student student = null;

if(student != null) {
    if(student.getNif().equals("000000X")) {
        System.out.println(student.getName());
    }
}
```
{% endcode %}

