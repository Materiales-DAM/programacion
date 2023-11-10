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

# Comparar objetos

Para poder comprobar si dos objetos son equivalentes es necesario implementar el método equals en la clase.

Si comparamos dos objetos utilizando el operador == devolverá true únicamente cuando a izquierda y derecha pongamos la misma instancia. No funcionará cuando comparemos dos instancias con los mismos valores.

La implementación del método equals es tediosa y es muy fácil introducir bugs, por ello es recomendable que el método lo genere el IDE. Además, dicha implementación se debe actualizar cada vez que se introduzca un cambio en los campos de la clase lo cual es una fuente de bugs.

```java
package oop.example;

import java.util.Objects;

public class Student {
    private String name;
    private String surname;
    private int age;

    public Student(String name, String surname, int age) {
        this.name = name;
        this.surname = surname;
        this.age = age;
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

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Student student = (Student) o;
        return age == student.age && Objects.equals(name, student.name) && Objects.equals(surname, student.surname);
    }

    @Override
    public int hashCode() {
        return Objects.hash(name, surname, age);
    }
}
```

Una vez definido el método equals, podemos comparar objetos.

```java
// Creamos un objeto de tipo Student con los datos de Bob
Student bob1  = new Student("Bob", "Esponja", 1);
// Creamos un objeto de tipo Student idéntico a bob1
Student bob2  = new Student("Bob", "Esponja", 1);

// Creamos un objeto de tipo Student con los datos de Peppa                
Student peppa  = new Student("Peppa", "Pig", 2);

if(bob1 == bob2) {
    // Este código no se ejecuta, porque bob1 y bob2 son instancias distintas
}

if(bob1.equals(bob2)) {
    // Este código se ejecuta si el método equals de Student está implementado correctamente
}

if(peppa.equals(bob1)) {
    // Este código no se ejecuta porque peppa y bob son distintos
}


```
