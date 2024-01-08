---
cover: ../../.gitbook/assets/image (8).png
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

# Jerarquías de varios niveles

Es posible crear jerarquías de clases de varios niveles. Por ejemplo, podríamos modificar el ejemplo anterior de la siguiente manera

```java
// Esta clase representa a cualquier tipo de ser vivo
public abstract class LivingBeing {
    private int age;

    public LivingBeing(int age) {
        this.age = age;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}

public abstract class Animal extends LivingBeing {
    private String color;

    public Animal(int age, String color) {
        super(age);
        this.color = color;
    }

    public String getColor() {
        return color;
    }

    public void setColor(String color) {
        this.color = color;
    }

    public void eat() {
        System.out.println("Estoy comiendo");
    }
}

public abstract class Vegetable extends LivingBeing{
    private int size;

    public Vegetable(int age, int size) {
        super(age);
        this.size = size;
    }

    public int getSize() {
        return size;
    }

    public void setSize(int size) {
        this.size = size;
    }
}


public class Dog extends Animal {
    private String owner;

    public Dog(int age, String color, String owner) {
        super(age, color);
        this.owner = owner;
    }

    public String getOwner() {
        return owner;
    }

    public void setOwner(String owner) {
        this.owner = owner;
    }

    public void bark() {
        System.out.println("Guau, guau");
    }
}

public class Lion extends Animal {
    private String jungleName;

    public Lion(int age, String color, String jungleName) {
        super(age, color);
        this.jungleName = jungleName;
    }

    public String getJungleName() {
        return jungleName;
    }

    public void setJungleName(String jungleName) {
        this.jungleName = jungleName;
    }

    public void roar() {
        System.out.println("Roar, roar!!");
    }
}

public class Ficus extends Vegetable{
    private String type;

    public Ficus(int age, int size, String type) {
        super(age, size);
        this.type = type;
    }

    public String getType() {
        return type;
    }

    public void setType(String type) {
        this.type = type;
    }
}

```

Hemos añadido a la jerarquía la clase LivingBeing, Vegetable y Ficus. Gracias a estos cambios ahora podemos representar vegetales además de animales, en este caso la única especie vegetal que hemos creado es Ficus.

Como podemos ver, puede haber clases abstractas en varios niveles, lo importante es que los subtipos finales no sean abstract para que podemos instanciarlos



```java
public class Main {
    public static void main(String[] args) {
        // Se instancia in ficus silvestre de 10 años, 5 de tamaño
        Ficus ficus = new Ficus(10, 5, "Silvestre");
        // No compila porque Vegetable es abstracta
        Vegetable vegetable = new Vegetable(5, 2);

    }
}
```

