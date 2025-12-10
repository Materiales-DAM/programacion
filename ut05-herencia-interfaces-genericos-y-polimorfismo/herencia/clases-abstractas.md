---
cover: ../../.gitbook/assets/image (8) (1).png
coverY: 0
---

# Clases abstractas

Las clases abstractas son un concepto fundamental en la programación orientada a objetos (POO). En términos simples, una clase abstracta sirve como un modelo o plantilla para otras clases. A diferencia de una clase común, una clase abstracta **no puede ser instanciada**; en cambio, se utiliza como base para derivar clases concretas.

Aquí hay algunos puntos clave sobre las clases abstractas:

1. **No se pueden instanciar:** No puedes crear objetos directamente a partir de una clase abstracta. Debes derivar una clase concreta que implemente (defina) los métodos abstractos de la clase base.
2. **Permte definir métodos abstractos:** Una clase abstracta generalmente incluye uno o más métodos abstractos. Un método abstracto es un método que se declara en la clase abstracta pero no se implementa en ella. La implementación real se deja a las clases concretas que heredan de la clase abstracta.
3. **Puede contener métodos concretos:** Además de los métodos abstractos, una clase abstracta puede contener métodos concretos (métodos con implementación) que son compartidos por las clases derivadas.
4. **Promueven la reutilización de código:** Al definir una clase abstracta, puedes establecer un conjunto común de métodos que deben implementarse en las clases derivadas. Esto fomenta la reutilización del código y ayuda a mantener una estructura coherente en las clases hijas.

Si volvemos al ejemplo anterior, veremos que la clase Animal puede ser definida como abstracta. Esto es posible porque todo animal es de una especie en concreto, por lo que no tiene sentido crear un animal genérico sin especie

La jerarquía de clases quedaría de la siguiente manera haciendo Animal abstracta

```java
// Clase abstracta Animal
public abstract class Animal {
    private String name;

    // Constructor
    public Animal(String name) {
        this.name = name;
    }

    // Método concreto compartido por todas las clases derivadas
    public void sleep() {
        System.out.println(name + " está durmiendo.");
    }
}

// Clase concreta Lion que extiende Animal
public class Lion extends Animal {
    
    private String jungleName;

    public Lion(String name, String jungleName) {
        super(name);
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

// Clase concreta Dog que extiende Animal
public class Dog extends Animal {
    private String owner;

    public Dog(String name, String owner) {
        super(name);
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

// Clase principal para probar el código
public class Main {
    public static void main(String[] args) {
        // Crear instancias de Lion y Dog
        Lion leon = new Lion("Simba", "Sabana");
        Dog perro = new Dog("Buddy", "Bob Esponja");

        leon.sleep();

        perro.sleep();
    }
}
```

En este ejemplo:

* `Animal` es una clase abstracta que tiene un método abstracto `saySomething()` y un método concreto `sleep()`.
* `Lion` y `Dog` son clases concretas que extienden `Animal` y proporcionan implementaciones específicas para el método `saySomething()`.
* En la clase principal (`Main`), se crean instancias de `Lion` y `Dog` y se llaman a sus métodos para mostrar cómo heredan y pueden utilizar tanto los métodos compartidos como los específicos de su propia clase.

## Métodos abstractos

Un método abstracto es un método que se declara en una clase abstracta pero no tiene una implementación en esa clase. La implementación real del método se deja a las subclases que heredan de la clase abstracta. Aquí hay algunos puntos clave sobre los métodos abstractos:

1.  **Declaración sin implementación:** Un método abstracto se declara en una clase abstracta utilizando la palabra clave `abstract`, pero no contiene un bloque de código que defina cómo se debe realizar la operación.

    ```java
    public abstract class Animal {
        private String name;

        // Constructor
        public Animal(String name) {
            this.name = name;
        }

        // Método abstracto que debe ser implementado por las clases derivadas
        public abstract void saySomething();

        // Método concreto compartido por todas las clases derivadas
        public void sleep() {
            System.out.println(name + " está durmiendo.");
        }
    }
    ```
2.  **Obligación de implementación:** Las clases que heredan de una clase abstracta que tiene métodos abstractos están obligadas a proporcionar implementaciones concretas para esos métodos. Si una clase no proporciona una implementación para un método abstracto, también debe declararse como abstracta. Es muy recomendable añadir la anotación @Override antes de la definición del método en las clases hijas.

    ```java
    public class Lion extends Animal {
        
        private String jungleName;

        public Lion(String name, String jungleName) {
            super(name);
            this.jungleName = jungleName;
        }

        public String getJungleName() {
            return jungleName;
        }

        public void setJungleName(String jungleName) {
            this.jungleName = jungleName;
        }

        // Implementación del método abstracto saySomething
        @Override
        public void saySomething() {
            System.out.println("Roar, roar!!");
        }

    }

    ```
3. **Palabra clave `abstract`:** Tanto la clase que contiene el método abstracto como el propio método se deben marcar con la palabra clave `abstract`.
4. **Facilita la herencia y la especialización:** Los métodos abstractos permiten definir una interfaz común en una clase base y luego permiten a las clases derivadas proporcionar implementaciones específicas según sus necesidades. Esto facilita la herencia y la especialización de clases.
5. **No puede ser estático:** Los métodos abstractos no pueden ser declarados como `static`. Son métodos que deben ser implementados por las clases hijas y pueden ser sobrescritos en esas clases.
6. **No puede tener un cuerpo:** Los métodos abstractos no pueden tener un cuerpo en la clase abstracta. La implementación real se proporciona en las clases derivadas.

Veamos cómo quedaría la jerarquía de clases anterior añadiendo el método abstracto `saySomething`:

```java
// Clase abstracta Animal
public abstract class Animal {
    private String name;

    // Constructor
    public Animal(String name) {
        this.name = name;
    }

    // Método abstracto que debe ser implementado por las clases derivadas
    public abstract void saySomething();

    // Método concreto compartido por todas las clases derivadas
    public void sleep() {
        System.out.println(name + " está durmiendo.");
    }
}

// Clase concreta Lion que extiende Animal
public class Lion extends Animal {
    
    private String jungleName;

    public Lion(String name, String jungleName) {
        super(name);
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

// Clase concreta Dog que extiende Animal
public class Dog extends Animal {
    private String owner;

    public Dog(String name, String owner) {
        super(name);
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

// Clase principal para probar el código
public class Main {
    public static void main(String[] args) {
        // Crear instancias de Lion y Dog
        Lion leon = new Lion("Simba", "Sabana");
        Dog perro = new Dog("Buddy", "Bob Esponja");

        leon.sleep();
        leon.saySomething();

        perro.sleep();
        perro.saySomething();
    }
}
```

En este ejemplo, la clase `Animal` tiene un método abstracto llamado `saySomething`. Las clases concretas `Lion` y `Dog` proporcionan implementaciones específicas para ese método. Cuando se crean instancias de estas clases y se llama al método `saySomething`, se ejecuta la implementación correspondiente de cada clase.

## Constructores

Cuando una clase hija hereda de una clase padre en Java, la clase hija puede proporcionar su propio constructor. La implementación de constructores en clases hijas implica dos aspectos principales: la invocación del constructor de la clase padre y la definición de cualquier inicialización específica de la clase hija.

Aquí hay algunas pautas generales sobre la implementación de constructores en clases hijas:

1.  **Invocar al constructor de la clase padre:**

    * Utiliza la palabra clave `super` para llamar al constructor de la clase padre.
    * Esto se hace en el bloque de inicialización del constructor de la clase hija, y generalmente es la primera instrucción dentro del constructor de la clase hija.

    ```java
    public class Dog extends Animal {
        private String owner;

        public Dog(String name, String owner) {
            // Invocación del constructor de la clase padre
            super(name);
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
2.  **Definir la inicialización específica de la clase hija:**

    * Después de la llamada al constructor de la clase padre, puedes incluir código adicional para inicializar miembros específicos de la clase hija.

    ```java
    public class Dog extends Animal {
        private String owner;

        public Dog(String name, String owner) {
            super(name);
            // Se inicializan los campos específicos de la subclase
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

### **Constructores sin parámetros**

Si la clase padre tiene un constructor sin parámetros y la clase hija no llama explícitamente a `super(...)`, Java automáticamente insertará una llamada implícita al constructor sin parámetros de la clase padre.
