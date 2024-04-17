---
cover: ../.gitbook/assets/tree.png
coverY: 94.60266666666666
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

# Stack\<E>

Una pila es una estructura de datos lineal que sigue el principio LIFO (Last-In, First-Out), lo que significa que el último elemento insertado es el primero en ser eliminado. Las operaciones en una pila generalmente se realizan en el extremo superior de la misma. Esto se asemeja a una pila de platos en un restaurante, donde los platos recién lavados se apilan en la parte superior y se retiran desde la misma parte superior.

Aquí están algunos métodos importantes de la clase `Stack` en Java:

1. **push(E elemento)**: Este método se utiliza para insertar un elemento en la parte superior de la pila.
2. **pop()**: Este método elimina y devuelve el elemento en la parte superior de la pila.
3. **peek()**: Este método devuelve el elemento en la parte superior de la pila sin eliminarlo.
4. **empty()**: Este método comprueba si la pila está vacía.

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption><p>Last In First Out en una pila</p></figcaption></figure>

Estos son los métodos básicos proporcionados por la clase `Stack` en Java. Recuerda que aunque `Stack` es fácil de entender y usar, se recomienda utilizar la interfaz `Deque` y su implementación `ArrayDeque` para nuevas implementaciones debido a su mayor eficiencia y flexibilidad.

Por ejemplo, aquí tienes un ejemplo de cómo usar la clase `Stack` en Java para invertir una cadena de caracteres:

```java
import java.util.Stack;

public class StackExample {
    public static String invertirCadena(String cadena) {
        // Creamos una pila para almacenar los caracteres
        Stack<Character> pila = new Stack<>();

        // Convertimos la cadena en un array de caracteres
        char[] caracteres = cadena.toCharArray();

        // Push cada carácter en la pila
        for (char c : caracteres) {
            pila.push(c);
        }

        // Construimos la cadena invertida extrayendo los caracteres de la pila
        StringBuilder resultado = new StringBuilder();
        while (!pila.isEmpty()) {
            resultado.append(pila.pop());
        }

        return resultado.toString();
    }

    public static void main(String[] args) {
        // Definimos una cadena
        String cadena = "Hola Mundo";

        // Invertimos la cadena
        String cadenaInvertida = invertirCadena(cadena);

        // Imprimimos la cadena invertida
        System.out.println("Cadena invertida: " + cadenaInvertida);
    }
}
```
