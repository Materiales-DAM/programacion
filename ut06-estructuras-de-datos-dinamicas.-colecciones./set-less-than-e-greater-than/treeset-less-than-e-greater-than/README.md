---
cover: ../../../.gitbook/assets/tree.png
coverY: 94.60266666666666
---

# TreeSet\<E>

La estructura de datos que implementa es un Self Balanced Binary Search Tree (árbol binario de búsqueda autobalanceado). Es una estructura de datos no lineal, optimizada para almacenar **datos ordenados** según un determinado **criterio de ordenación**.

<figure><img src="../../../.gitbook/assets/image (16).png" alt=""><figcaption><p>Árbol binario de búsqueda balanceado</p></figcaption></figure>

Algunos conceptos que debemos manejar en cuanta a árboles:

* Cada valor se guarda en una estructura llamada nodo
* Cada nodo puede tener un valor a su izquierda y otro a su derecha.
* Se denominan hojas a los nodos a los que les falta alguno de sus nodos izquierdo o derecho.
* Los valores de los nodos a la izquierda con más pequeños que el valor del nodo y los de la derecha son mayores.
* La altura de un nodo es la distancia entre el nodo raíz y el propio nodo
* La profundidad de un árbol es la distancia entre la raíz y el nodo más alto
* Un árbol está balanceado cuando la distancia entre sus dos hojas más distantes no es superior a 1
* La profundidad de un árbol balanceado se calcula aplicando la fórmula **log n**

Las principales características de los árboles binarios de búsqueda son:

* Cada elemento se inserta dentro de la estructura en la posición que le corresponde según el criterio de ordenación definido, a diferencia de en las listas dicha posición no se puede modificar a voluntad.
* Tiene muy buen comportamiento en operaciones de búsqueda, inserción y eliminación con una complejidad de O(log(n))
* Para comprobar si un elemento existe en el árbol habrá que realizar, como máximo, tantos pasos como la profundidad del árbol.

## Árboles desbalanceados

Un árbol puede llegar a estar desbalanceado dependiendo del orden en el que se hayan insertado / eliminado los elementos que contiene. Por ejemplo, cuando insertamos los elementos de mayor a menor (o viceversa) el árbol queda completamente desbalanceado. Un arbol que no está balanceado resulta ser una estructura de datos ineficiente.

<figure><img src="../../../.gitbook/assets/image (19).png" alt=""><figcaption><p>Eficiencia de árbol binario (no autobalanceado)</p></figcaption></figure>

Para evitar este problema los árboles suelen incorporar algún algoritmo de balanceo automático como parte de su funcionalidad de inserción y eliminación. Los árboles auto balanceados más conocidos son AVL (Adelson-Velskii), Red-Black Tree y B-Tree.

<figure><img src="../../../.gitbook/assets/image (20).png" alt=""><figcaption><p>Eficiencia de operaciones en árbol binario (no balanceado) vs AVL</p></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (12).png" alt=""><figcaption><p>Notación BIg-O</p></figcaption></figure>

## Ordenación de los elementos

Para crear un TreeSet\<E> es necesario que haya algún criterio de ordenación de los valores. Existen varios opciones para definir esta ordenación.

### Ordenación de tipos básicos de Java

En caso de que los elementos del TreeSet sean de algún tipo básico existe una ordenación por defecto:

* String: alfabéticamente
* Tipos númericos: de menor a mayor

En caso de que el tipo no sea básico o se desee una ordenación distinta de la que viene por defecto se debe utilizar la técnica explicada en la sección Comparator\<E>

### Ordenación con Comparable\<T>

Una forma de proveer el criterio de ordenación para elementos de un tipo, es hacer que la clase implemente la interface Comparable\<T>, donde T es la propia clase.

Esta interface obliga a implementar el método **int compareTo(T o):**

* La implementación de este método debe comparar dos objetos: this y el parámetro o.
* El método debe devolver un número entero de entre los siguientes valores:
  * 1: cuando el objeto o es mayor que this se devuelve 1.
  * 0: si los dos objetos se consideran iguales en términos de ordenación, se devuelve 0
  * -1: cuando el objeto o es menor que this se devuelve -1.

Esta forma de establecer la ordenación de un tipo permite especificar un único criterio de ordenación para elementos de tipo T, ya que solo es posible implementar el método compareTo una sola vez.

Por ejemplo, si queremos crear un TreeSet\<Student> debemos hacer que la clase Student implemente Comparable\<Student>

```java
import java.util.Objects;

public class Student implements Comparable<Student> {
    private String name;

    private String surname;

    private String email;

    private int zipCode;

    public Student(String name, String surname, String email, int zipCode) {
        this.name = name;
        this.surname = surname;
        this.email = email;
        this.zipCode = zipCode;
    }

    @Override
    public int compareTo(Student other) {
        // Como zipCode es primitivo, necesitamos hacer la comparacion con la 
        // clase análoga al primitivo, en este caso Integer
        return Integer.compare(this.zipCode, other.getZipCode());
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

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public int getZipCode() {
        return zipCode;
    }

    public void setZipCode(int zipCode) {
        this.zipCode = zipCode;
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;

        Student student = (Student) o;

        if (zipCode != student.zipCode) return false;
        if (!Objects.equals(name, student.name)) return false;
        if (!Objects.equals(surname, student.surname)) return false;
        return Objects.equals(email, student.email);
    }

    @Override
    public int hashCode() {
        int result = name != null ? name.hashCode() : 0;
        result = 31 * result + (surname != null ? surname.hashCode() : 0);
        result = 31 * result + (email != null ? email.hashCode() : 0);
        result = 31 * result + zipCode;
        return result;
    }

    @Override
    public String toString() {
        return "Student{" +
                "name='" + name + '\'' +
                ", surname='" + surname + '\'' +
                ", email='" + email + '\'' +
                ", zipCode=" + zipCode +
                '}';
    }
}

```

Si ejecutamos este programa veremos que a la salida los estudiantes están ordenados por apellidos y nombre:

```
Bob Esponja. Dirección: Calle Falsa
George Pig. Dirección: Calle Falsa
Peppa Pig. Dirección: Calle Falsa
```

### Ordenación con Comparator\<T>

La otra forma de proveer un criterio de ordenación para elementos de un tipo T, es crear una nueva clase que implemente la interface Comparator\<T>.

Esta interface obliga a implementar el método **int compare(T o1, T o2):**

* La implementación de este método debe comparar dos objetos: o1 y el parámetro o2.
* Esta implementación de la ordenación está desacoplada de la clase de objetos que ordena.
* El método debe devolver un número entero de entre los siguientes valores:
  * 1: cuando el objeto o1 es mayor que o2 se devuelve 1.
  * 0: si los dos objetos se consideran iguales en términos de ordenación, se devuelve 0
  * -1: cuando el objeto o1 es menor que o2 se devuelve -1.

El uso de esta interface permite especificar múltiples criterios de ordenación para elementos de tipo T, al estar desacoplado la definición de T de sus criterios de ordenación

```java
public class NameSurnameStudentComparator implements Comparator<Student> {

    @Override
    public int compare(Student o1, Student o2) {
        int compare = o1.getSurname().compareTo(o2.getSurname());
        // Si los apellidos de ambos son iguales compareTo devuelve 0
        if (compare == 0) {
            // Si el apellido era igual ordenamos por nombre
            compare = o1.getName().compareTo(o2.getName());
            
            // Añadimos un compareTo usando un campo que sea único para que no se
            // descarte ningún estudiante, aunque ya haya uno con el mismo nombre 
            // y apellidos
            if(compare == 0) {
                compare = o1.getEmail().compareTo(o2.getEmail());
            }
        }
        // Devolvemos el valor de compare
        return compare;
    }
}
```

Cuando quiera crear un TreeSet\<Student> deberé pasar al constructor el Comparator\<Student> que quiero aplicar ese TreeSet

```java
TreeSet<Student> students = new TreeSet<>(new NameSurnameStudentComparator());
students.add(new Student("Bob", "Esponja", "bob@esponja.es", 28000));
students.add(new Student("Peppa", "Pig", "peppa@pig.es", 28001));
students.add(new Student("George", "Pig", "george@pig.es", 28001));
System.out.println(students);
```
