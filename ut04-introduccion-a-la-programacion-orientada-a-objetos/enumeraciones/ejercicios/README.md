---
cover: ../../../.gitbook/assets/oop.png
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

# Ejercicios

1. Crea una clase para guardar información de personas
   * De cada persona queremos guardar:
     * Nombre
     * Apellidos
     * Estado civil (soltero, casado, divorciado o viudo)
     * DNI / NIF
     * Edad
   * Define los siguientes métodos vinculados a cada persona:
     * Saludo: imprimirá en pantalla el mensaje "Hola soy  \<nombre>  \<apellidos> y mi DNI/NIF es \<DNI>"
     * Despedida:  imprimirá en pantalla el mensaje "Hasta la próxima! Firmado \<nombre>"
   * Instancia un objeto Persona que almacene tus datos personales, una vez creado invoca el método de saludo y después el de despedida
2.  Crea una clase para guardar los datos de diferentes vehículos:&#x20;

    1. Tipo de vehiculo (coche, moto, camión): Usar tipo enum
    2. Velocidad máxima&#x20;
    3. Color&#x20;
    4. Matrícula&#x20;

    La clase debe incluir un constructor con todos los campos, métodos getter y setter para acceder a los campos y un método info que imprima en pantalla todos los datos del vehiculo..

Crea otra clase llamada VehicleReader que permita leer vehículos. Esta clase tendrá como campo un Scanner y tendrá un método que pide al usuario los datos de un vehículo y lo devuelve.

Además habrá una clase Main que realice lo siguiente:

* Inicializa un Scanner&#x20;
* Crea un VehicleReader
* Pide un vehiculo
* Invoca el método info del vehículo
