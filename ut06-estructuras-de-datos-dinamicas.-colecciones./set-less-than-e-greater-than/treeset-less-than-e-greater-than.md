---
cover: ../../.gitbook/assets/tree.png
coverY: 94.60266666666666
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

# TreeSet\<E>

La estructura de datos que implementa es un Self Balanced Binary Search Tree (árbol binario de búsqueda autobalanceado). Es una estructura de datos no lineal, optimizada para almacenar **datos ordenados** según un determinado **criterio de ordenación**.&#x20;

<figure><img src="../../.gitbook/assets/image (16).png" alt=""><figcaption><p>Árbol binario de búsqueda balanceado</p></figcaption></figure>

Las principales características de los TreeSet son:

* Cada elemento se inserta dentro de la estructura en la posición que le corresponde según el criterio de ordenación definido, a diferencia de en las listas dicha posición no se puede modificar a voluntad.
* Tiene muy buen comportamiento en operaciones de búsqueda, inserción y eliminicación con una complejidad de O(log(n))

## Ordenación de los elementos

Para crear un TreeSet\<E> es necesario que haya algún criterio de ordenación de los valores. Existen varios opciones para definir esta ordenación.

### Ordenación de tipos básicos de Java&#x20;

En caso de que los elementos del TreeSet sean de algún tipo básico existe una ordenación por defecto:

* String: alfabéticamente
* Tipos númericos: de menor a mayor

En caso de que el tipo no sea básico o se desee una ordenación distinta de la que viene por defecto se debe utilizar la técnica explicada en la sección Comparator\<E>

### Ordenación con Comparable\<T>

Una forma de proveer el criterio de ordenación para elementos de un tipo, es hacer que la clase implemente la interface Comparable\<T>, donde T es la propia clase.

Esta interface obliga a implementar el método **int compareTo(T o):**

* La implementación de este método debe comparar dos objetos: this y el parámetro o.
* El método debe devolver un número entero de entre los siguientes valores:
  * 1: cuando el objeto o es mayor que this se devuelve 1.
  * 0: si los dos objetos se consideran iguales en términos de ordenación, se devuelve 0
  * \-1: cuando el objeto o es menor que this se devuelve -1.

Esta forma de establecer la ordenación de un tipo permite especificar un único criterio de ordenación para elementos de tipo T, ya que solo es posible implementar el método compareTo una sola vez.

Por ejemplo, si queremos crear un TreeSet\<Student> debemos hacer que la clase Student implemente Comparable\<Student>

```java
package org.ies.highschool.model;

import java.util.Objects;

// Student implementa Comparable<Student> para poder crear TreeSet<Student
public class Student implements Comparable<Student> {
    private String name;
    private String surname;
    private String address;

    public Student(String name, String surname, String address) {
        this.name = name;
        this.surname = surname;
        this.address = address;
    }
    
    public void info() {
        System.out.println(name + " " + surname + ". Dirección: " + address);
    }

    /**
     * Este compareTo ordena alfabéticamente por apellidos y nombre
     */
     @Override
    public int compareTo(Student other) {
        int compare = this.surname.compareTo(other.getSurname());
        // Si los apellidos de ambos son iguales compareTo devuelve 0
        if (compare == 0) {
            // Si el apellido era igual ordenamos por nombre
            compare = this.name.compareTo(other.getName());
        }
        // Devolvemos el valor de compare
        return compare;
    }


    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getSurname() {
        return surname;
    }

    public void setSurname(String surname) {
        this.surname = surname;
    }

    public String getAddress() {
        return address;
    }

    public void setAddress(String address) {
        this.address = address;
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Student student = (Student) o;
        return Objects.equals(name, student.name) && Objects.equals(surname, student.surname) && Objects.equals(address, student.address);
    }

    @Override
    public int hashCode() {
        return Objects.hash(name, surname, address);
    }
    
}

public class Main {
    public static void main(String[] args) {
        Set<Student> students = new TreeSet<>();
        students.add(
                new Student("Peppa", "Pig", "Calle Falsa")
        );
        students.add(
                new Student("Bob", "Esponja", "Calle Falsa")
        );
        students.add(
                new Student("George", "Pig", "Calle Falsa")
        );

        for (Student student: students) {
            student.info();
        }
    }
}
```

Si ejecutamos este programa veremos que a la salida los estudiantes están ordenados por apellidos y nombre:

```
Bob Esponja. Dirección: Calle Falsa
George Pig. Dirección: Calle Falsa
Peppa Pig. Dirección: Calle Falsa
```

### Ordenación con Comparator\<T>

La otra forma de proveer un criterio de ordenación para elementos de un tipo T, es crear una nueva clase que implemente la interface Comparator\<T>.

Esta interface obliga a implementar el método **int compare(T o1, T o2):**

* La implementación de este método debe comparar dos objetos: o1 y el parámetro o2.
* Esta implementación de la ordenación está desacoplada de la clase de objetos que ordena.
* El método debe devolver un número entero de entre los siguientes valores:
  * 1: cuando el objeto o1 es mayor que o2 se devuelve 1.
  * 0: si los dos objetos se consideran iguales en términos de ordenación, se devuelve 0
  * \-1: cuando el objeto o1 es menor que o2 se devuelve -1.

El uso de esta interface permite especificar múltiples criterios de ordenación para elementos de tipo T, al estar desacoplado la definición de T de sus criterios de ordenación

```java
public class StudentComparator implements Comparator<Student> {

    @Override
    public int compare(Student o1, Student o2) {
        int compare = o1.getSurname().compareTo(o2.getSurname());
        // Si los apellidos de ambos son iguales compareTo devuelve 0
        if (compare == 0) {
            // Si el apellido era igual ordenamos por nombre
            compare = o1.getName().compareTo(o2.getName());
        }
        // Devolvemos el valor de compare
        return compare;
    }
}
```
