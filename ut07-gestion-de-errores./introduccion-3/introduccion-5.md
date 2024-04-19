---
cover: ../../.gitbook/assets/quality-assurance-code-bug.jpg
coverY: 110.50526315789473
layout:
  cover:
    visible: true
    size: full
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

# Ejercicios de diseño de excepciones

## Edificio

Crea un programa que almacene la información de un edificio

1. Dirección
2. Municipio
3. Lista de apartamentos
   1. Número de planta
   2. Puerta
   3. Lista de Propietarios
      1. Nombre
      2. Apellidos

Crea en el main los métodos para pedir al usuario la información del edificio. En caso de que el usuario meta alguna información mal, se debe capturar la excepción (try y catch) y volver a pedir el dato.

## Calculadora

Implementar un programa tipo calculadora. Imprime un menú con las siguientes opciones:

* Divide: recibe dos número double y devuelve su división. En caso de que el segundo número sea cero lanza la excepción DivideByZeroException (debes definir la excepción)
* Media: recibe un array de double y devuelve la media. En caso de que el array esté vacío lanza la excepción EmptyArrayException.

Estos dos métodos deben propagar la excepción que lanza cada uno de ellos, capturalos en el componente del menu interactivo.

## Empresa

Crea un programa que permita representar los datos de una empresa:

1. Nombre de la empresa
2. CIF
3. Departamentos. Por cada departamento: nombre y listado de empleados
   1. Por cada empleado: nif, nombre, apellidos y puesto

Crea los siguientes métodos en Company:

1. Devuelve los empleados de un departamento dado. En caso de que el departamento no exista lanza la excepción DepartmentNotFoundException.
2. Devuelve los datos de un departamento dado. En caso de que el departamento no exista lanza la excepción DepartmentNotFoundException
3. Devuelve los datos de un empleado a partir de un NIF. E En caso de que el emleado no exista lanza la excepción EmployeeNoFoundException

## Biblioteca

Crea un programa que maneje los datos de una biblioteca:

1. Nombre de la biblioteca
2. Libros del catálogo. Por cada libro se guardará: ISBN, título, autor, genéros (listado)
3. Socios de la biblioteca. Por cada socio se guardará: nif, nombre, apellidos, número de socio, código postal.
4. Se almacenará un historial de préstamos: ISBN, fecha préstamos, nif (del socio que lo ha tomado prestado), fecha de devolución

Implementar los métodos en Biblioteca (crear interface IBibiloteca):

1. Un método que dado un ISBN, devuelve el libro. Si no existe el libro se lanza la excepción BookNotFoundException(isbn)
2. Dado un nif, devuelve el socio. Si no existe MemberNotFoundException(nif)
3. Comprueba que, dado un nif y un isbn, el socio ha tomado prestado un libro. Si no existe el socio MemberNotFoundException(nif) y si no existe el libro BookNotFoundException(isbn)
