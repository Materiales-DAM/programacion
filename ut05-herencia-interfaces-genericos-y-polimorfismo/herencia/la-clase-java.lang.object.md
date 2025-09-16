---
cover: ../../.gitbook/assets/image (8) (1).png
coverY: 0
---

# La clase java.lang.Object

La clase `Object` en Java es la clase base de todas las clases en Java. Todas las clases, directa o indirectamente, heredan de la clase `Object`. Esto significa que todos los objetos en Java comparten ciertas características y métodos proporcionados por la clase `Object`.

Aquí hay algunas de las características y métodos más importantes de la clase `Object`:

1.  **Método `equals(Object obj)`**: Este método se utiliza para comparar si dos objetos son iguales. Por defecto, el método `equals` de la clase `Object` compara la referencia de los objetos, es decir, si ambos objetos se refieren a la misma ubicación en la memoria. Sin embargo, es común que las clases hijas sobrescriban este método para proporcionar una comparación más significativa según el contenido de los objetos.

    ```java
    public boolean equals(Object obj) {
        // Implementación personalizada de la comparación de igualdad
    }
    ```
2.  **Método `hashCode()`**: Devuelve un valor hash único para el objeto. Este método se utiliza comúnmente en estructuras de datos que dependen de hash, como las colecciones basadas en hash (por ejemplo, HashMap). Si sobrescribes el método `equals`, es una buena práctica sobrescribir también el método `hashCode` para asegurar la coherencia.

    ```java
    public int hashCode() {
        // Implementación personalizada del valor hash
    }
    ```
3.  **Método `toString()`**: Devuelve una representación en cadena del objeto. Este método es comúnmente utilizado para obtener una representación legible del objeto y se invoca automáticamente cuando se utiliza el objeto en un contexto que requiere una cadena, como en la concatenación de cadenas o en la impresión.

    ```java
    public String toString() {
        // Implementación personalizada para representar el objeto como cadena
    }
    ```
4.  **Método `getClass()`**: Devuelve la clase del objeto en tiempo de ejecución. Puede ser útil para obtener información sobre el tipo de objeto en tiempo de ejecución.

    ```java
    public final native Class<?> getClass();
    ```

Estas son solo algunas de las funciones más destacadas de la clase `Object`. Al ser la clase base, proporciona métodos comunes que son útiles en muchas situaciones, pero en la mayoría de los casos, se espera que las clases hijas sobrescriban algunos de estos métodos para adaptarse a sus propios comportamientos y propósitos específicos.
