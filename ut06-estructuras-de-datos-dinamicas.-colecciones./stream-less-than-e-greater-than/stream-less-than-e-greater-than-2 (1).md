---
cover: ../../.gitbook/assets/lambda.jpeg
coverY: 0
---

# Ejercicios operaciones intermedias

```java
import lombok.AllArgsConstructor;
import lombok.Data;

import java.time.LocalDate;
import java.util.List;

@Data
@AllArgsConstructor
public class Order {
    private int id;
    private LocalDate date;
    private List<Item> items;
}
```

```java
import lombok.AllArgsConstructor;
import lombok.Data;

@Data
@AllArgsConstructor
public class Item {
    private int productId;
    private int quantity;
}
```

```java
import lombok.AllArgsConstructor;
import lombok.Data;

@Data
@AllArgsConstructor
public class Student {
    private String nif;
    private String name;
    private String surname;
    private String email;
}
```

Resuelve estos ejercicios usando Stream

1. Escribe un programa que cree un ArrayList y lo rellene con varios String. Luego conviértelo en un Stream y recórrelo mostrando en pantalla cada elemento.
2. Un método sum10(List\<Integer> numbers) que dado una lista de enteros, devuelve otra lista de enteros del mismo tamaño en la que se le ha sumado 10 a cada número de la primera lista.
3. Un método List\<String> mapToEmails(List\<Student> students) que dada una lista de estudiantes, devuelva una lista de los emails de los estudiantes en el mismo orden
4. Un método List\<Student> filterByZipCode(List\<Student> students, int zipCode) que dada una lista de estudiantes y un código postal, devuelva una lista con los estudiantes que vivan en ese código postal
5. Un método que recibe una lista de números enteros (numbers) y devuelve otra lista con los números pares que había en numbers
6. Un método que dado una lista de pedidos, devuelve una lista con los precios de cada pedido
7. Un método que dado una lista de pedidos, devuelva una lista con todos los OrderItem

