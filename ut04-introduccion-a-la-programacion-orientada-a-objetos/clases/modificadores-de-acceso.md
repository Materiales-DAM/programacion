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

# Modificadores de acceso

Los modificadores de acceso definen desde dónde es accesible un campo, método o clase.

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

```java
public class Student {
    // Los campos no son accesibles desde fuera de la clase Student porque son privados
    private String name;
    private String surname;
    private int course;
    
    // Esto es un constructor de Student
    public Student(String name, String surname, int course) {
        this.name = name;
        this.surname = surname;
        this.course = course;        
    }
    
    // El método sayHello se puede invocar desde fuera de la clase Student porque es público
    public void sayHello() {
        System.out.println("Hola, soy " + name + " " + surname + " y estoy en el curso " + course);
    }
    
    // El método saySomething solo se puede invocar desde dentro de la clase Student porque es privado
    private void saySomething() {
        System.out.println("Hola, soy " + name+" y digo algo");
    }
    
}
```
