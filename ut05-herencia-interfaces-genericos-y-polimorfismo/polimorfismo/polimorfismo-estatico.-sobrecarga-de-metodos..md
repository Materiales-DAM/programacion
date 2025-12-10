---
cover: ../../.gitbook/assets/polymorphism.png
coverY: 0
---

# Polimorfismo estático. Sobrecarga de métodos.

La **sobrecarga de métodos** en Java es un tipo de polimorfismo conocido como "polimorfismo de compilación" o "polimorfismo estático". El polimorfismo permite que un mismo nombre de método se utilice de diferentes maneras, y el compilador selecciona automáticamente la versión correcta del método en función de los tipos y la cantidad de argumentos proporcionados.

Por ejemplo, podríamos tener una clase Calculadora que defina los siguientes métodos:

```java
public class Calculadora {

    // Método para sumar dos números enteros
    public int sumar(int a, int b) {
        return a + b;
    }

    // Método sobrecargado para sumar tres números enteros
    public int sumar(int a, int b, int c) {
        return a + b + c;
    }

    // Método sobrecargado para sumar dos números decimales
    public double sumar(double a, double b) {
        return a + b;
    }

    // Método sobrecargado para concatenar dos cadenas de texto
    public String sumar(String a, String b) {
        return a + b;
    }
}
```

```java
public class Main {
    public static void main(String[] args) {
        Calculadora calculadora = new Calculadora();

        // Ejemplo de uso de los métodos sobrecargados
        System.out.println("Suma de enteros: " + calculadora.sumar(3, 5));
        System.out.println("Suma de enteros: " + calculadora.sumar(2, 4, 6));
        System.out.println("Suma de decimales: " + calculadora.sumar(2.5, 3.5));
        System.out.println("Concatenación de cadenas: " + calculadora.sumar("Hola", " Mundo"));
    }
}
```

Explicación:

* La clase `Calculadora` tiene varios métodos llamados `sumar`, pero con diferentes tipos y cantidades de parámetros.
* El método `sumar(int a, int b)` suma dos números enteros.
* El método `sumar(int a, int b, int c)` suma tres números enteros.
* El método `sumar(double a, double b)` suma dos números decimales.
* El método `sumar(String a, String b)` concatena dos cadenas de texto.

En el método `main`, se creó una instancia de `Calculadora` y se llamaron a los diferentes métodos `sumar` con diferentes tipos de argumentos para ilustrar cómo se selecciona automáticamente el método correcto según los parámetros proporcionados. Este es un ejemplo básico de cómo la sobrecarga de métodos en Java puede mejorar la flexibilidad y claridad del código.
