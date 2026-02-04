---
cover: ../../../.gitbook/assets/tree.png
coverY: 94.60266666666666
---

# Ejercicios de ordenaciones

## Student

1. Crea un TreeSet\<Student> que ordene por apellidos y nombre implementando Comparable
2. Crea un TreeSet\<Student> que ordene por zipCode, apellidos y nombre usando un Comparator

## Flight

```java
import lombok.AllArgsConstructor;
import lombok.Data;

@Data
@AllArgsConstructor
public class Flight {
    private int number;
    private String company;
    private String origin;
    private String destination;

}

```

* Crea un TreeSet\<Flight> que ordene por origen y destino . Con Comparable y Comparator
* Crea un TreeSet\<Flight> que ordene por compañia. Con Comparator

## Passenger

```java
import lombok.AllArgsConstructor;
import lombok.Data;

@Data
@AllArgsConstructor
public class Passenger {
    private String nif;
    private String name;
    private String surname;
    private int seat;

}
```

* Ordena los pasajeros por nombre y apellidos. Con Comparator y Comparable
* Ordena los pasajeros por número de asiento. Con Comparator.
