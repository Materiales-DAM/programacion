---
cover: ../../.gitbook/assets/image (8).png
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

## 1. Animales

Crea una jerarquía de clases que represente diferentes tipos de animales:

* Perro
* Gato
* Cerdo

Queremos almacenar la edad de todos los animales, y todo animal debe ser un perro, un gato o un cerdo.

Además, queremos almacenar esta información adicional de cada uno de estos tipos:

* Perro
  * Raza
* Gato
  * Color
* Cerdo
  * Alimentación (String): “bellotas”, “pienso”, etc...

Se desea que exista un método (talk()) que implementen todos los animales que sirva para que saquen un mensaje por pantalla:

* Cerdo: “oink, oink”
* Gato: “miau”
* Perro: “guau, guau”

Además crea un método showInfo que muestre la información de cada animal.

## 2. Vehiculos

Crea una jerarquía de clases que permita representar diferentes tipos de vehículos. Todo vehiculo debe tener:

* Km realizados (int)
* Matrícula

Los tipos de vehículo son:

* Camión:
  * Número de ejes (int)
* Coche:
  * Número de puertas
  * Caballos
* Moto
  * Cilindrada

Añade los siguientes métodos de vehículo

* move: dada una distancia en kilometros, muestra en pantalla "Recorridos \<distancia> kilometros más" y añade la distancia a los kilómetros relizados
* showInfo: muestra toda la información del vehículo

## 3. Formas

Crear una jerarquía de clases  para representar formas geométricas. Todas las formas tienen:

* color: de tipo string

Los tipos de formas son:

* Cuadrado
  * Lado: de tipo double
* Círculo
  * Radio: de tipo double&#x20;
* Triángulo (rectángulo==
  * Base: de tipo double
  * Altura: de tipo double

Añade los siguientes métodos a la clase Forma.

* area: calcula el área de la forma( devuelve un double=
  * Cuadrado: area = lado \* lado
  * Circulo: area = PI  \* radio \* radio
  * Triángulo: area = base \* altura / 2
* info:  muestra toda la información de la figura geométrica

## 4. Empleados

Crea una jerarquía de clases que nos permita representar los empleados de una empresa de programación:

* Programador
  * Nif
  * Nombre
  * Apellidos
  * Horas trabajadas
  * Lenguajes de programación
  * Proyecto
* Jefes proyectos
  * Nif
  * Nombre
  * Apellidos
  * Horas trabajadas
  * Proyectos
* Product manager
  * Nif
  * Nombre
  * Apellidos
  * Horas trabajadas
  * Proyecto
* Director de tecnología
  * Nif
  * Nombre
  * Apellidos
  * Horas trabajadas

Todo empleado debe ser programador, jefe de proyecto, product manager o director de tecnología. Todos los empleados deben tener los siguientes métodos:

* Mostrar información
* Imputar horas: dado un número de horas aumentar las horas trabajadas.

Además, debe haber los siguientes métodos específicos de cada tipo de empleado:

* Programador
  * Un método que dado un lenguaje de programación devuelve true si lo conoce y false si no lo conoce
* Jefe de proyecto
  * Un método que dado un proyecto devuelve true si lo dirige y false si no

## 5. Médicos

Crea una jerarquía de clases que permita representar a los diferentes tipos de médicos:

* Todos los médicos tienen:
  * Nombre
  * Apellidos
  * Número de colegiado
  * Listado de pacientes (lista de string)
* Además, existen las siguientes especialidades:
  * Cirujano (Surgeon)
    * Hospital
    * Número de box
  * De familia
    * Nombre del centro de salud
  * Podólogo
    * Hospital
    * Planta

Métodos

* Todos los médicos deben tener un método que permita mostrar su información:
  * Cirujano: “\<Nombre> \<Apellidos> (\<nº colegiado>), cirujano en el box \<Box> del hospital \<Hospital>”
  * De familia: “\<Nombre> \<Apellidos> (\<nº colegiado>), médico de familia en el centro de salud de \<Centro de salud>”
  * Podólogo: “\<Nombre> \<Apellidos> (\<nº colegiado>), podólogo en el centro de salud de \<Centro de salud>”
* Un método que devuelva si el médico trabaja en un hospital o no (boolean)
