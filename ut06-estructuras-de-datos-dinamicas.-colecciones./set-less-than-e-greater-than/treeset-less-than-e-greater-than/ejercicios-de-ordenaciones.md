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
    
    @Override
    public boolean equals(Object o) {
        if (o == null || getClass() != o.getClass()) return false;
        Flight flight = (Flight) o;
        return number == flight.number && Objects.equals(company, flight.company) && Objects.equals(origin, flight.origin) && Objects.equals(destination, flight.destination);
    }

    @Override
    public int hashCode() {
        return Objects.hash(number, company, origin, destination);
    }

    @Override
    public String toString() {
        return "Flight{" +
                "number=" + number +
                ", company='" + company + '\'' +
                ", origin='" + origin + '\'' +
                ", destination='" + destination + '\'' +
                '}';
    }
}

```

* Crea un TreeSet\<Flight> que ordene por origen y destino . Con Comparable y Comparator
* Crea un TreeSet\<Flight> que ordene por compañia. Con Comparable y Comparator

## Passenger

```java
import java.util.Objects;

public class Passenger {
    private String nif;
    private String name;
    private String surname;
    private int seat;

    public Passenger(String nif, String name, String surname, int seat) {
        this.nif = nif;
        this.name = name;
        this.surname = surname;
        this.seat = seat;
    }

    public String getNif() {
        return nif;
    }

    public void setNif(String nif) {
        this.nif = nif;
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
    
    public int getSeat() {
        return seat;
    }
    
     public void setSeat(int seat) {
        this.seat = seat;
    }
    

}
```

* Ordena los pasajeros por nombre y apellidos. Comparator y Comparable
* Ordena los pasajeros por número de asiento. Comparator y Comparable.
