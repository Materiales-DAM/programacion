---
cover: ../../.gitbook/assets/generics.jpg
coverY: 0
---

# Ejercicios genéricos

## Zoo

Implementa un programa que permita gestionar un Zoo. El Zoo está compuesto por:

* Nombre del zoo
* Área de herbívoros
* Área de carnívoros
* Área de animales de todo tipo

Todo área es génerica en el tipo de animal que puede contener. Cada área tiene

* Número de área
* Array de animales

Los animales pueden ser carnívoros o herbívoros. Todos los animales tienen:

* Especie
* Edad
* Nombre

Además, los carnívoros tienen:

* Tipo de carne que comen

Los herbívoros tienen:

* Conjunto de plantas que comen

## Grandes almacenes

Implementa un programa que permita gestionar unos grandes almacenes. Unos grandes almacenes están compuestos por:

1. Nombre
2. Dirección
3. Sección de electrónica
4. Sección de ropa
5. Sección general

Cada sección vende productos del tipo de su sección, la sección general vende todo tipo de productos. Cada sección tiene:

1. Planta
2. Nombre del gerente
3. Listado de productos

Los productos tienen:

1. Id de producto
2. Precio
3. Unidades
4. Además hay varios tipos de producto:
   1. Ropa
      1. Tipo (camiseta, pantalón, jersey...)
      2. Talla
      3. Marca
   2. Electrónica
      1. Tipo (ordenador, televisor...)
      2. Nombre del modelo
      3. Fabricante
5. Todos los productos deben tener un método info() que muestre todos los datos del mismo

Componentes:

* MainApp:
  * Crea un warehouse hardcodeado
  * Mostrar todos los productos de electrónica (incluyendo los que pueda haber en la planta general)
  * Mostrar todos los productos de ropa (incluyendo los que pueda haber en la planta general)
  * Mostrar todos los productos
