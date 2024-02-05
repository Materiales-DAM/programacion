---
cover: ../../.gitbook/assets/image (1) (1).png
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

# Interfaces y herencia múltiple

En Java, aunque no existe la herencia múltiple de clases, se puede lograr cierta flexibilidad utilizando interfaces.&#x20;

A continuación, vamos a ver un ejemplo&#x20;

```java
// Interface for carnivorous animals
interface Carnivore {
    void eatMeat();
}

// Interface for herbivorous animals
interface Herbivore {
    void eatPlants();
}

interface Omnivore extends Carnivore, Herbivore{
    void eatMeatWithPlants();
}

// Interface for oviparous animals
interface Oviparous {
    void layEggs();
}

// Interface for mammals
interface Mammal {
    void nurse();
}

// Class representing a lion, which is carnivorous and a mammal
class Lion implements Carnivore, Mammal {
    @Override
    public void eatMeat() {
        System.out.println("El león come gacelas.");
    }

    @Override
    public void nurse() {
        System.out.println("La leona amamanta a sus crías.");
    }
}

// Class representing a cow, which is herbivorous and a mammal
class Cow implements Herbivore, Mammal {
    @Override
    public void eatPlants() {
        System.out.println("La vaca come hierba.");
    }

    @Override
    public void nurse() {
        System.out.println("La vaca amamanta sus terneros");
    }
}

// Class representing a snake, which is carnivorous and oviparous
class Snake implements Carnivore, Oviparous {
    @Override
    public void eatMeat() {
        System.out.println("La serpiente come ratones.");
    }

    @Override
    public void layEggs() {
        System.out.println("La serpiente pone huevos.");
    }
}

class Platipus implements Omnivore, Oviparous, Mammal {
    @Override
    public void eatMeat() {
        System.out.println("El ornitorrinco come serpientes.");
    }
    
    @Override
    public void eatPlants() {
        System.out.println("El ornitorrinco come hierba.");
    }
    
    @Override
    public void eatMeatWithPlants() {
        System.out.println("El ornitorrinco come de todo.");
    }

    @Override
    public void layEggs() {
        System.out.println("El ornitorrinco pone huevos.");
    }
    
     @Override
    public void nurse() {
        System.out.println("El ornitorrinco amamanta sus crías.");
    }
}

public class Main {
    public static void main(String[] args) {
        Lion lion = new Lion();
        lion.eatMeat();
        lion.nurse();

        Cow cow = new Cow();
        cow.eatPlants();
        cow.nurse();

        Snake snake = new Snake();
        snake.eatMeat();
        snake.layEggs();
        
        Platipus platipus = new Platipus();
        platipus.eatMeat();
        platipus.layEggs();
        platipus.nurse();
    }
}
```

1. **Interfaces:** Las interfaces (`Carnivore`, `Herbivore`, `Oviparous`, `Mammal`) definen los métodos relacionados con los comportamientos de cada tipo de animal.
2. **Clases concretas:** Las clases `Lion`, `Cow,` `Snake` y `Platipus` implementan las interfaces según sus comportamientos específicas. Por ejemplo, el león implementa las interfaces `Carnivore` y `Mammal`.
3. **Método principal (`main`):** En el método principal, se crean instancias de las clases y se llaman a los métodos específicos de cada interfaz para demostrar los comportamientos de cada animal.

Este enfoque muestra cómo las interfaces pueden ser utilizadas para simular herencia múltiple, permitiendo que las clases implementen múltiples interfaces según las características que necesiten representar. Cada clase puede elegir las interfaces que mejor se adapten a sus atributos y comportamientos específicos.
