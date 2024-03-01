---
cover: ../../../.gitbook/assets/tree.png
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

# Ejercicios de ordenaciones

## Student

1. Crea un TreeSet\<Student> que ordene por apellidos y nombre implementando Comparable
2. Crea un TreeSet\<Student> que ordene por zipCode, apellidos y nombre usando un Comparator

## Flight

```java
import java.util.Arrays;
import java.util.Objects;

public class Flight {
    private int number;

    private String company;

    private String origin;

    private String destination;


    public Flight(int number, String company, String origin, String destination) {
        this.number = number;
        this.company = company;
        this.origin = origin;
        this.destination = destination;
    }

    public int getNumber() {
        return number;
    }

    public void setNumber(int number) {
        this.number = number;
    }

    public String getCompany() {
        return company;
    }

    public void setCompany(String company) {
        this.company = company;
    }

    public String getOrigin() {
        return origin;
    }

    public void setOrigin(String origin) {
        this.origin = origin;
    }

    public String getDestination() {
        return destination;
    }

    public void setDestination(String destination) {
        this.destination = destination;
    }
}

```

* Crea un TreeSet\<Flight> que ordene por origen y destino . Con Comparable y Comparator
* Crea un TreeSet\<Flight> que ordene por compañia. Con Comparable y Comparator

