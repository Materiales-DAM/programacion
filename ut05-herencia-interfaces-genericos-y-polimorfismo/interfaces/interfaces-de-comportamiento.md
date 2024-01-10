---
cover: ../../.gitbook/assets/image (1).png
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

# Interfaces de comportamiento

Utilizar interfaces es una manera efectiva de añadir comportamientos a una clase sin necesidad de herencia múltiple, ya que Java no admite herencia múltiple de clases, pero sí permite implementar múltiples interfaces.

Por ejemplo, podríamos crear un interface Printable que permita imprimir en pantalla los datos de los objetos que lo implementen

```java
public interface Printable {
    void print();  // Abstract method that classes must implement
}
```

Ahora creamos la clase Student y hacemos que sea Printable. Esto nos obliga a implementar el método print()

```java

public class Student implements Printable {
    private String name;
    private String surname;
    private String address;

    public Student(String name, String surname, String address) {
        this.name = name;
        this.surname = surname;
        this.address = address;
    }

    @Override
    public void print() {
        System.out.println("Nombre: " + name +". Apellidos: " + surname + ". Dirección: " + address);
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
}
```



## Interfaces estándar

Java proporciona varios interfaces en su biblioteca estándar que juegan un papel importante en el desarrollo de aplicaciones. Algunos de los interfaces más importantes son:

1. **`Serializable`:**
   * **Propósito:** Indica que una clase puede ser serializada, es decir, convertida en una secuencia de bytes para ser almacenada o transmitida.
   * **Métodos Clave:** No contiene métodos, actúa como una interfaz de marcador.
2. **`Runnable`:**
   * **Propósito:** Permite que una clase sea ejecutada en un hilo separado.
   * **Métodos Clave:** `run()`: Define el punto de entrada del hilo.
3. **`Comparable`:**
   * **Propósito:** Permite que las instancias de una clase sean comparables entre sí.
   * **Métodos Clave:** `compareTo(T o)`: Compara la instancia actual con otra.
4. **`Iterable`:**
   * **Propósito:** Define un método para obtener un iterador, permitiendo que una clase sea utilizada en un bucle for-each.
   * **Métodos Clave:** `iterator()`: Devuelve un iterador para la clase.
5. **`Closeable` y `AutoCloseable`:**
   * **Propósito:** Indica que una clase puede liberar recursos cuando ya no es necesaria.
   * **Métodos Clave:** `close()`: Libera los recursos.
6. **`EventListener`:**
   * **Propósito:** Sirve como la interfaz base para todos los escuchadores de eventos en el modelo de eventos AWT y Swing.
   * **Métodos Clave:** No contiene métodos, actúa como una interfaz de marcador.
7. **`Observer`:**
   * **Propósito:** Define un protocolo para objetos que observan cambios en otros objetos.
   * **Métodos Clave:** `update(Observable o, Object arg)`: Método llamado cuando el objeto observado cambia.

Estos son solo algunos de los interfaces clave en Java. La biblioteca estándar de Java proporciona una amplia variedad de interfaces para abordar diferentes aspectos del desarrollo de software, desde la concurrencia hasta la manipulación de colecciones y la gestión de eventos.
