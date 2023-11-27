---
cover: ../../.gitbook/assets/oop.png
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

# Tipos de clases

Cuando escribimos un programa en el paradigma POO (Programación Orientada a Objetos), podemos diferenciar entre dos tipos de clases:

* Clases que sirven para representar datos
* Clases que sirven para codificar procesos

## Clases de datos (Java Beans)

En los sistemas informáticos vamos a querer representar entidades del mundo real como objetos para poder manipularlos. Para poder representar estas entidades vamos a usar los Java Beans.

Un Java Bean cumple las siguientes características:

* Es una clase que sirve para representar los datos de una entidad del mundo real
* Todos los campos son privados
* Cada campo tiene un getter y un setter
* Hay un constructor con todos los campos
* Implementa los métodos hashCode y equals

Por ejemplo, si quisieramos almacenar los datos de un taller mecánico, podríamos crear un Java Bean para representar cada uno de los vehículos que están en el taller

```java
package org.ies.vehicles.model;

import java.util.Objects;

/**
 * Esto es un Java bean o POJO (Plain Old Java Object), porque sirve para guardar los datos de un vehiculo.
 * Para que sea una clase sea Java Bean:
 * - Todos los campos son privados
 * - Cada campo tiene un getter y un setter
 * - Hay un constructor con todos los campos
 * - Hay un hashCode y equals
 * - Es una clase que sirve para representar datos
 */
public class Vehicle {
    private String vehicleType;
    private String color;
    private int maxSpeed;
    private String plate;

    public Vehicle(String vehicleType, String color, int maxSpeed, String plate) {
        this.vehicleType = vehicleType;
        this.color = color;
        this.maxSpeed = maxSpeed;
        this.plate = plate;
    }

    public void info() {
        System.out.println(this.toString());
    }

    public String getVehicleType() {
        return vehicleType;
    }

    public void setVehicleType(String vehicleType) {
        this.vehicleType = vehicleType;
    }

    public String getColor() {
        return color;
    }

    public void setColor(String color) {
        this.color = color;
    }

    public int getMaxSpeed() {
        return maxSpeed;
    }

    public void setMaxSpeed(int maxSpeed) {
        this.maxSpeed = maxSpeed;
    }

    public String getPlate() {
        return plate;
    }

    public void setPlate(String plate) {
        this.plate = plate;
    }

    @Override
    public boolean equals(Object o) {

        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Vehicle vehicle = (Vehicle) o;
        return maxSpeed == vehicle.maxSpeed && Objects.equals(vehicleType, vehicle.vehicleType) && Objects.equals(color, vehicle.color) && Objects.equals(plate, vehicle.plate);
    }

    @Override
    public int hashCode() {
        return Objects.hash(vehicleType, color, maxSpeed, plate);
    }

    @Override
    public String toString() {
        return "Vehicle{" +
                "vehicleType='" + vehicleType + '\'' +
                ", color='" + color + '\'' +
                ", maxSpeed=" + maxSpeed +
                ", plate='" + plate + '\'' +
                '}';
    }
}

```

Una vez tenemos la clase Vehicle, ya podemos crear objetos de ese tipo que nos permiten almacenar información de diferentes vehículos



```java
Vehicle vehicle1 = new Vehicle("Moto","Rojo", 180, "3432JVK");

Vehicle vehicle2 = new Vehicle("Coche","Azul", 200, "3422KVB");

// Muestra los datos del primer vehículo
vehicle1.info();


// Muestra los datos del segundo vehículo
vehicle2.info();
```

## Componentes

Además de clases para representar las entidades, nuestro programa va a necesitar codificar una serie de rutinas que sirvan para realizar determinadas funciones. Estas rutinas van a ser codificadas en otro tipo de clases llamadas componentes.

Los componentes se caracterizan por:

* Sirven para codificar una determinada rutina.
* Sus campos son dependencias, es decir, otros componentes que necesita para realizar su trabajo
* Tiene un constructor en el que recibe instancias de sus dependencias
* No define getters ni setters
* No define hashCode, equals ni toString

Por ejemplo, el componente que codifica la rutina que pide al usuario los datos de un vehículo sería:

```java
package org.ies.vehicles.components;

import org.ies.vehicles.model.Vehicle;

import java.util.Scanner;

/**
 * Esta clase NO ES un Java Bean porque ni es una clase de datos, ni tiene getters y setters
 */
public class VehicleReader {
    private Scanner scanner;

    public VehicleReader(Scanner scanner) {
        this.scanner = scanner;
    }

    public Vehicle askVehicle() {
        System.out.println("Introduce los datos del vehículo");

        System.out.println("Tipo de vehículo:");
        String vehicleType = scanner.nextLine();

        System.out.println("Color:");
        String color = scanner.nextLine();

        System.out.println("Velocidad máxima:");
        int maxSpeed = scanner.nextInt();
        scanner.nextLine();

        System.out.println("Matrícula:");
        String plate = scanner.nextLine();

        Vehicle vehicle = new Vehicle(vehicleType, color, maxSpeed, plate);
        return vehicle;

    }
}

```



Este componente VehicleReader tiene:

* Una dependencia de tipo Scanner: necesita ese componente para realizar su trabajo
* Un métood askVehicle que implementa la rutina de pedir al usuario un vehículo.

