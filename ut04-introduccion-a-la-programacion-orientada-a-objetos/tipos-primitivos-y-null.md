---
cover: ../.gitbook/assets/oop.png
coverY: 0
---

# Tipos primitivos y null

Los tipos primitivos no pueden tomar el valor null, la causa de este problema es que los tipos primitivos de Java NO SON OBJETOS y, por tanto, no pueden tomar el valor null.

```java
// No compila
int number = null;
```

Sin embargo, puede haber ocasiones en las que queramos que un determinado campo de tipo numérico pueda ser null. Por ejemplo, si hacemos un POJO para representar estudiantes y la edad es un campo opcional

```java
import java.util.Objects;

public class Student {
    private String name;
    private String surname;
    private String address;
    private int age;

    public Student(String name, String surname, String address, int age) {
        this.name = name;
        this.surname = surname;
        this.address = address;
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

    public String getAddress() {
        return address;
    }

    public void setAddress(String address) {
        this.address = address;
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
        return age == student.age && Objects.equals(name, student.name) && Objects.equals(surname, student.surname) && Objects.equals(address, student.address);
    }

    @Override
    public int hashCode() {
        return Objects.hash(name, surname, address, age);
    }
}

```

Tal y como está definida esta clase es obligatorio pasar un valor en la edad de todo estudiante ya que el tipo int no permite almacenar null

<pre class="language-java"><code class="lang-java"><strong>// Bob no define la dirección y tiene 30 años. Este código funciona
</strong>Student student1 = new Student("Bob", "Esponja", null, 30);

// Peppa define todos sus campos menos la edad. ESTE CÓDIGO NO COMPILA, la edad no puede ser null.
Student student2 = new Student("Peppa", "Pig", "Calle Falsa", null);

</code></pre>

## Wrapper classes

Para solucionar este problema, existen en Java un conjunto de clases denominadas Java Wrapper Classes que permiten almacenar los tipos primitivos en objetos Java.

<figure><img src="../.gitbook/assets/image (7) (1).png" alt=""><figcaption></figcaption></figure>

En el ejemplo anterior, podríamos cambiar el tipo de age de int a Integer

```java
import java.util.Objects;


public class Student {
    private String name;
    private String surname;
    private String address;

    private Integer age;

    public Student(String name, String surname, String address, Integer age) {
        this.name = name;
        this.surname = surname;
        this.address = address;
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

    public String getAddress() {
        return address;
    }

    public void setAddress(String address) {
        this.address = address;
    }

    public Integer getAge() {
        return age;
    }

    public void setAge(Integer age) {
        this.age = age;
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Student student = (Student) o;
        return Objects.equals(name, student.name) && Objects.equals(surname, student.surname) && Objects.equals(address, student.address) && Objects.equals(age, student.age);
    }

    @Override
    public int hashCode() {
        return Objects.hash(name, surname, address, age);
    }
}

```

Ahora sí que podemos crear estudiantes cuya edad es nul

<pre class="language-java"><code class="lang-java"><strong>// Bob no define la dirección y tiene 30 años. Este código funciona
</strong>Student student1 = new Student("Bob", "Esponja", null, 30);

// Peppa define todos sus campos menos la edad. Este código compila.
Student student2 = new Student("Peppa", "Pig", "Calle Falsa", null);

</code></pre>

### Boxing, unboxing y autoboxing

El proceso por el cual un valor primitivo se convierte en un valor de su wrapped class se denomina boxing. Este nombre viene de meter el valor en una "caja", que es la wrapped class.

```java
int age = 5;
// Autoboxing del valor 5 en el objeto Integer(5)
Integer ageWrapped = age;

```

Este proceso de conversión también se puede realizar en sentido contrario, denominándose unboxing

```java
Integer ageWrapped = 5;
// Unboxing del objeto Integer(5) al primitivo 5
int age = ageWrapped;
```

El proceso de boxing y autoboxing es totalmente seguro, sin embargo el unboxing fallará cuando el valor del objeto sea null

```java
Integer value = null;
// Produce NullPointerException ya que no hay ningún valor del que hacer unboxing
int v = value;
```
