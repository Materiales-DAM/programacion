---
cover: ../../.gitbook/assets/image (8) (1).png
coverY: 0
---

# Jerarquías de varios niveles

Es posible crear jerarquías de clases de varios niveles. Por ejemplo, podríamos modificar el ejemplo anterior de la siguiente manera

```java
// Esta clase representa a cualquier tipo de ser vivo
public abstract class LivingBeing {
    protected int age;

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
```

```java
public abstract class Animal extends LivingBeing {
    protected String name;

    public Animal(int age, String name) {
        super(age);
        this.name = name;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public abstract void saySomething();

    // Método concreto compartido por todas las clases derivadas
    public void sleep() {
        System.out.println(nombre + " está durmiendo.");
    }
}
```

```java
public abstract class Vegetable extends LivingBeing{
    protected int size;

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
```

```java
public class Dog extends Animal {
    private String owner;

    public Dog(int age, String name, String owner) {
        super(age, name);
        this.owner = owner;
    }

    public String getOwner() {
        return owner;
    }

    public void setOwner(String owner) {
        this.owner = owner;
    }

    @Override
    public void saySomething() {
        System.out.println("Guau, guau");
    }
}
```

```java
public class Lion extends Animal {
    private String jungleName;

    public Lion(int age, String name, String jungleName) {
        super(age, name);
        this.jungleName = jungleName;
    }

    public String getJungleName() {
        return jungleName;
    }

    public void setJungleName(String jungleName) {
        this.jungleName = jungleName;
    }

    @Override
    public void saySomething() {
        System.out.println("Roar, roar!!");
    }
}
```

```java
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

## Herencia entre clases abstractas

Cuando una clase abstracta hereda de otra clase abstracta, no es necesario que implemente los métodos abstractos de la superclase, ya que puede dejar que las subclases sean responsables de ello.

Por ejemplo, añadamos a LivingBeing los métodos abstractos grow e info

```java
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
    
    public abstract void grow();
    
    public abstract void info();
}
```

En el caso de los animales vamos a implementar el método grow de la misma manera para todos ellos, pero el método info será diferente.

```java
public abstract class Animal extends LivingBeing {
    private String name;

    public Animal(int age, String name) {
        super(age);
        this.name = name;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public abstract void saySomething();

    
    public void sleep() {
        System.out.println(name + " está durmiendo.");
    }
    
    // El método grow es igual para todos los animales
    @Override
    public void grow() {
        System.out.println(name + " está creciendo.");
    }
}
```

```java
public class Dog extends Animal {
    private String owner;

    public Dog(int age, String name, String owner) {
        super(age, name);
        this.owner = owner;
    }

    public String getOwner() {
        return owner;
    }

    public void setOwner(String owner) {
        this.owner = owner;
    }

    @Override
    public void saySomething() {
        System.out.println("Guau, guau");
    }
    
    // Este es el método info de un perro
    @Override
    public void info() {
        System.out.println(name + " es el perro de " + owner);
    }
}
```

```java
public class Lion extends Animal {
    private String jungleName;

    public Lion(int age, String name, String jungleName) {
        super(age, name);
        this.jungleName = jungleName;
    }

    public String getJungleName() {
        return jungleName;
    }

    public void setJungleName(String jungleName) {
        this.jungleName = jungleName;
    }

    @Override
    public void saySomething() {
        System.out.println("Roar, roar!!");
    }
    
    // Este es el método info de un león
    @Override
    public void info() {
        System.out.println(name + " es un león del " + jungleName);
    }
}
```

Por otro lado, los métodos grow e info son iguales para todos los vegetale

```java
public abstract class Vegetable extends LivingBeing{
    protected int size;

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
    
    @Override
    public void info() {
        System.out.println("Es un vegetal de " + age +" años y " + size + " metros");
    }
    
    @Override
    public void grow() {
        System.out.println("Vegetal está creciendo.");
        size = size + 1;
    }
}
```
