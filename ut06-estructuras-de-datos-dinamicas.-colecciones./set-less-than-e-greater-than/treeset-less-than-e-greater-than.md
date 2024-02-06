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

### Ordenación con Comparable\<E>

Esta opción solo es posible con POJOs que se definen en el propio proyecto ya que es necesario modificar la propia clase de los objetos que se desean ordenar.&#x20;

Por ejemplo, si queremos crear un TreeSet\<Student> debemos hacer que implemente Comparable\<Student>

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

### Ordenación con Comparator\<E>

Creando una clase que implemente Comparator\<E> y pasándola en el momento de la creación del TreeSet\<E>
