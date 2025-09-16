---
cover: ../../.gitbook/assets/oop.png
coverY: 0
---

# Enumeraciones

En ocasiones vamos a querer crear un tipo para codificar campos categóricos. Un campo categórico se caracteriza por poder tomar un conjunto de valores conocido.

Por ejemplo, si quisiéramos almacenar los campos de las personas y, de entre ellos, queremos el estado civil, sabemos que ese datos es un dato categórico porque solo puede tomar como valores: soltero, casado, divorciado o viudo.

En este caso podemos crear un tipo especial de tipo enum que nos permite delimitar los valores que puede tomar el campo de estado civil.

```java
public enum CivilState{
    Single, Married, Divorced, Widower;
}
```

Una vez definido el tipo ya podemos usarlo en la clase Person

```java
public class Person {

    private String name;

    private String surname;

    private CivilState civilState;

    private int age;

    public Person(String name, String surname, CivilState civilState, int age) {
        this.name = name;
        this.surname = surname;
        this.civilState = civilState;
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

    public void printPerson() {
        System.out.println(name + " " + surname + ". Edad: " + age);
    }
}

```

Ahora podemos crear objetos de tipo Person en los que especificamos su estado civil

```java
// Bob está soltero
Person person1 = new Person("Bob", "Esponja", CivilState.Single, 3);
// Peppa está divorciada
Person person2 = new Person("Peppa", "Pig", CivilState.Divorced, 4);
```

## Menús interactivos

Las enumeraciones son muy útiles para codificar las opciones de menús interactivos

```java
public enum MyMenuOptions{
    Sum("Sumar"), Substract("Restar"), Exit("Salir");

    private final String description;

    MyMenuOptions(String description) {
        this.description = description;
    }

    public static MyMenuOptions fromIndex(int opt) {
        return MyMenuOptions.values()[opt];
    }

    public static void printMenu() {
        System.out.println("Elige una opción:");
        for (int i = 0; i < MyMenuOptions.values().length; i++) {
            System.out.println(i +"." + MyMenuOptions.values()[i].description); 
        }
    }
}
```
