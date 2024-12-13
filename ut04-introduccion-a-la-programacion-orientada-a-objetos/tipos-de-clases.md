---
cover: ../.gitbook/assets/oop.png
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

# Componentes

Cuando escribimos un programa en el paradigma POO (Programación Orientada a Objetos), podemos diferenciar entre dos tipos de clases:

* Clases que sirven para representar datos (POJO)
* Clases que sirven para codificar procesos

## Componentes

Además de clases para representar las entidades, nuestro programa va a necesitar codificar una serie de rutinas que sirvan para realizar determinadas funciones. Estas rutinas van a ser codificadas en otro tipo de clases llamadas componentes.

Los componentes se caracterizan por:

* Sirven para codificar una determinada rutina.
* Sus campos son dependencias, es decir, otros componentes que necesita para realizar su trabajo. Se considera una buena práctica que los campos de los componentes sean inmutables, esto se consigue añadiendo la palabra final
* Tiene un constructor en el que recibe instancias de sus dependencias
* No define getters ni setters
* No define hashCode, equals ni toString

Por ejemplo, el componente que codifica la rutina que pide al usuario los datos de un vehículo sería:

```java
package org.ies.vehicles.components;

import org.ies.vehicles.model.Vehicle;

import java.util.Scanner;

/**
 * Esta clase NO ES un POJO porque ni es una clase de datos, ni tiene getters y setters
 */
public class VehicleReader {
    private final Scanner scanner;

    public VehicleReader(Scanner scanner) {
        this.scanner = scanner;
    }

    public Vehicle read() {
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
* Un método read que implementa la rutina de pedir al usuario un vehículo.
