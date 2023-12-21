# Soluciones

1\.

CivilState.java

```java
package oop.example;

public enum CivilState {
    Single, Married, Divorced, Widower;

}
```

Person.java

```java
package oop.example;

import java.util.Objects;

public class Person {

    private String nif;

    private String name;

    private String surname;

    private CivilState civilState;

    private int age;

    public Person(String nif, String name, String surname, CivilState civilState, int age) {
        this.nif = nif;
        this.name = name;
        this.surname = surname;
        this.civilState = civilState;
        this.age = age;
    }

    public void saluda() {
        System.out.println("Hola soy " + name + " " + surname + " y mi DNI/NIF es " + nif);
    }

    public void despedida() {
        System.out.println("Hasta la próxima! Firmado " + name);
    }

    public String getNif() {
        return nif;
    }

    public void setNif(String nif) {
        this.nif = nif;
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

    public CivilState getCivilState() {
        return civilState;
    }

    public void setCivilState(CivilState civilState) {
        this.civilState = civilState;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    @Override
    public String toString() {
        return "Person{" +
                "nif='" + nif + '\'' +
                ", name='" + name + '\'' +
                ", surname='" + surname + '\'' +
                ", civilState=" + civilState +
                ", age=" + age +
                '}';
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Person person = (Person) o;
        return age == person.age && Objects.equals(nif, person.nif) && Objects.equals(name, person.name) && Objects.equals(surname, person.surname) && civilState == person.civilState;
    }

    @Override
    public int hashCode() {
        return Objects.hash(nif, name, surname, civilState, age);
    }
}

```

