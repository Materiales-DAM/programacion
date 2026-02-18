---
cover: ../.gitbook/assets/oop.png
coverY: 0
---

# Records

Un **record** es un tipo de clase inmutable y muy concisa, pensada para representar **datos** (“data carriers”) sin todo el boilerplate típico de getters, constructor, `equals`, `hashCode`, `toString`, etc.

> Mentalmente: es como un POJO inmutable, pero el compilador te genera casi todo.

Disponible como feature estándar desde **Java 16** (previews antes).

## 1. Sintaxis básica

```java
public record Person(String name, int age) { }
```

Con esa única línea, el compilador genera automáticamente:

* Campos `private final String name; private final int age;`
*   Un **constructor canónico**:

    ```java
    public Person(String name, int age) { ... }
    ```
*   Métodos de acceso (no se llaman `getX`, sino el nombre del componente):

    ```java
    public String name() { return name; }
    public int age() { return age; }
    ```
* `equals(...)`, `hashCode()` y `toString()` apropiados, basados en todos los componentes.

Uso:

```java
Person p = new Person("Alice", 30);
System.out.println(p.name()); // "Alice"
System.out.println(p);        // Person[name=Alice, age=30]
```

## 2. Características de los records

### 2.1 Inmutabilidad (superficial)

* Los campos del record son **`final` e implícitamente `private`**.
* No hay setters.
* No puedes reasignar los campos dentro de la clase.

```java
public record Point(int x, int y) { 
}
// NO: p.x = 5; // error de compilación
```

### 2.2 Restricciones

Un `record`:

* **Extiende implícitamente `java.lang.Record`**, no puedes extender otra clase.
*   Puede **implementar interfaces**:

    ```java
    public record User(String username, String email) implements Serializable { }
    ```
* No puedes declarar **otros campos de instancia no estáticos** que no sean los componentes del record.
  * Sí puedes tener campos `static` o `static final`.

### 2.3 Métodos

Puedes añadir métodos como en una clase normal:

```java
public record Person(String name, int age) {

    public boolean isAdult() {
        return age >= 18;
    }
}
```

## 3. Records vs POJOs

#### PersonPojo

```java
public class PersonPojo {

    private String name;
    private int age;

    public PersonPojo() { }

    public PersonPojo(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // getters y setters
    public String getName() { return name; }
    public void setName(String name) { this.name = name; }

    public int getAge() { return age; }
    public void setAge(int age) { this.age = age; }

    // equals, hashCode, toString (boilerplate o Lombok)
}
```

#### Person record

```java
public record Person(String name, int age) { }
```

#### 3.1 Boilerplate

* **POJO clásico**: mucho código repetitivo (constructores, getters, setters, `equals`, `hashCode`, `toString`).
* **Record**: todo eso viene generado automáticamente, lo que reduce errores y ruido.

Si usas Lombok en POJOs, el diferencial se reduce, pero:

* El record es **nativo del lenguaje** (sin dependencia externa).
* Lombok es una herramienta extra, con anotaciones y procesado de código.

#### 3.2 Mutabilidad

* **POJO**: por defecto suelen ser **mutables** (tienen setters). También puedes hacerlos inmutables manualmente (sin setters, campos `final`).
* **Record**: inmutables por diseño (no setters, campos `final`).

Para lógica de negocio que necesita modificar estado paso a paso, un POJO mutable puede ser más natural.\
Para **DTOs, mensajes, configuraciones, resultados de consulta**, etc., la inmutabilidad de los records es muy cómoda.

#### 3.3 Herencia

* **Record**: no puede extender otra clase que no sea `java.lang.Record`. Pero sí puede implementar interfaces.
* **POJO**: puede extender otra clase y usar herencia clásica.

Si necesitas una jerarquía de herencia compleja, records no son buena opción.

#### 3.4 Legibilidad y mantenimiento

* **Record**: ideal para modelos de datos pequeños y claros. Una sola línea comunica la estructura completa.
* **POJO**: mejor cuando hay mucha lógica de negocio asociada, o cuando la clase va a evolucionar con herencia, estados intermedios, etc.

### 4. Pattern matching y deconstruction

Los records están pensados para funcionar muy bien con el **pattern matching** de Java moderno.

Ejemplo simple (instanceof + deconstruction):

```java
static void printShape(Object shape) {
    if (shape instanceof Rectangle(int width, int height)) {
        System.out.println("Rectangle " + width + "x" + height);
    }
}
```

Aquí `Rectangle` podría ser:

```java
public record Rectangle(int width, int height) { }
```

El pattern matching “descompone” el record en sus componentes, lo que hace el código muy expresivo.

### 5. ¿Cuándo usar record y cuándo POJO?

#### Usa **records** cuando:

* El objetivo principal es **transportar datos**.
* Quieres **inmutabilidad** por defecto.
* No necesitas herencia.
* No estás atado a frameworks que exigen POJOs mutables (especialmente JPA entities).
* Quieres aprovechar pattern matching y deconstruction.

Ejemplos:

* DTOs de entrada/salida en servicios.
* Resultados de cálculos.
* Configs inmutables.
* Value objects (Money, Coordinates, Range, etc.).

#### Usa **POJOs** cuando:

* Es una **entidad JPA** o similar.
* Necesitas **estado mutable** durante el ciclo de vida del objeto.
* Necesitas **herencia clásica**.
* El framework que usas asume presencia de setters, constructor por defecto, etc.
