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

# Clases

Una clase describe un conjunto de variables relacionadas y un conjunto de operaciones que se pueden realizar sobre ellos. Podemos ver una clase como una plantilla que nos permite representar objetos que conceptualmente representan algo parecido. Las clases se componen de:

* **Campos**: son cada uno de los atributos que componen los objetos de esta clase&#x20;
* **Constructores**: Son métodos que sirven para crear objetos de esta clase
* **Métodos**: Además de los constructores, se pueden definir métodos vinculados a los objetos que realicen algún tipo de cálculo, operación o modificación sobre los datos del objeto.

Por ejemplo, si se desea hacer un programa que gestione información de alumnos, podríamos crear una clase Student que nos sirva para modelar los datos de los estudiantes

```java
public class Student {
    // Estos son los campos de la clase Student
    private String name;
    private String surname;
    private int course;
    
    // Esto es un constructor de Student
    public Student(String name, String surname, int course) {
        this.name = name;
        this.surname = surname;
        this.course = course;        
    }
    
    // Esto es un método que sirve para que un estudiante se presente
    public void sayHello() {
        System.out.println("Hola, soy " + name + " " + surname + " y estoy en el curso " + course);
    }
    
}
```

Una vez hemos definido la clase, ya podemos empezar a crear objetos de esa clase:

```java
public class StudentMain {
    public static void main(String[] args) {
        // Creamos un objeto de tipo Student con los datos de Bob
        Student bob  = new Student("Bob", "Esponja", 1);

        // Creamos un objeto de tipo Student con los datos de Peppa                
        Student peppa  = new Student("Peppa", "Pig", 2);
        
        // Invocamos el método sayHello() del objeto bob
        bob.sayHello();
        // Invocamos el método sayHello() del objeto peppa
        peppa.sayHello();
    }
}
```

## Campos

