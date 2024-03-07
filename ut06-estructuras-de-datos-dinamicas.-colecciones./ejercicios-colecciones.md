---
cover: ../.gitbook/assets/tree.png
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

# Ejercicios colecciones

## Biblioteca

Crea un programa que maneje los datos de una biblioteca:

1. Nombre de la biblioteca
2. Libros inexados por ISBN. Por cada libro se guardará: ISBN, título, autor, genéros (Set)
3. Socios de la biblioteca (lista). Por cada socio se guardará: nif, nombre, apellidos, número de socio, código postal.
4. Se almacenará un historial de préstamos: ISBN, fecha préstamos, nif (del socio que lo ha tomado prestado)

Implementar los métodos en Biblioteca :

* Dado un género, devuelve todos los libros que tengan ese género (List\<Book>).
  * Add
  * foreach
  * Contains
* Dado un código postal, devuelve los socios que viven ahí (List\<Member>)
  * Add
  * foreach
* Dado un nif y un ISBN, crea un préstamo para un socio. Crea un BookLend con la fecha actual.
  * Add
* Dado un ISBN y un género, elimina el género del libro
  * Foreach
  * Remove
* Dado un ISBN y un número de socio (no NIF), devuelve si el socio ha tomado prestado el libro o no (boolean).
  * Foreach

## Banco

Crea una aplicación que sirva para gestionar las cuentas de los clientes de un banco. Crea una estructura de clases que permita almacenar estos datos:

1. Nombre del banco
2. Listado de clientes. Por cada cliente:
   1. Nombre y apellidos
   2. NIF
   3. Código postal
3. Cuentas indexadas por iban. Por cada cuenta
   1. Iban (String)
   2. Nif del cliente
   3. Saldo

El banco debe permitir realizar las siguientes operaciones:

* Dado un iban y una cantidad, ingresar la cantidad en la cuenta. Si no existe la cuenta devuelve null.
* Dado un nif, devolver todas las cuentas de ese cliente. Si el cliente no existe devuelve null.
* Dado un iban y una cantidad, sacarla cantidad en la cuenta.
* Realizar una transferencia entre dos cuentas de dos clientes. Para realizar la transferencia será necesario proporcionar la cantidad, el iban de cuenta de origen y de destino
* Dado un código postal, devuelve todas las cuentas cuyo propietario vive en ese código postal

## Tienda

Implementa una estructura de clases que permita gestionar una tienda. De la tienda se debe almacenar:

* Nombre
* Productos: los productos deben estar indexados por id de producto. Por cada producto:
  * Id de producto (entero)
  * Nombre del producto
  * Precio (entero)
  * Etiquetas: conjunto no ordenado de etiquetas (cada etiqueta es un String)
* Clientes: Conjunto de clientes ordenados por apellidos, nombre y nif. Por cada cliente
  * Nif (String)
  * Nombre
  * Apellidos
  * Lista de pedidos, por cada pedido:
    * Id del pedido
    * Fecha del pedido
    * Precio total
    * Lista de items del pedido, por cada item:
      * Id de producto (entero)
      * Cantidad

Implementa los siguientes métodos en la clase Shop:

* Dado un nif, devuelve el cliente con ese NIF.
* Dado un nif y un id de pedido, devuelve el pedido del cliente.
* Dado un id de producto, devuelve el producto con ese id.
* Dado un nif y un id de pedido, devuelve una lista con los productos que se han pedido.
* Dado una etiqueta (String), devuelve una lista de productos que tienen esa etiqueta.
* Dado un nif, devuelve cuánto se ha gastado el cliente en la tienda.
