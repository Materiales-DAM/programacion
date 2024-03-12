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

1. name: Nombre de la biblioteca
2. booksByIsbn: libros inexados por ISBN. Por cada libro se guardará:&#x20;
   1. isbn
   2. title
   3. author
   4. genres (Set\<String>)
3. customers: socios de la biblioteca (lista). Por cada socio se guardará:
   1. nif
   2. name
   3. surname
   4. customerNumber: entero
   5. zipCode: entero
4. booklends: se almacenará un historial de préstamos (BookLend) ordenados por fecha:&#x20;
   1. isbn,
   2. date,
   3. nif

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

1. name: Nombre del banco
2. customers: Listado de clientes. Por cada cliente:
   1. nif
   2. name
   3. surname
   4. zipCode
3. accountsByIban: cuentas indexadas por iban. Por cada cuenta
   1. iban (String)
   2. nif
   3. balance: saldo

El banco debe permitir realizar las siguientes operaciones:

* Dado un iban y una cantidad, ingresar la cantidad en la cuenta. Si no existe la cuenta devuelve null.
* Dado un nif, devolver todas las cuentas de ese cliente. Si el cliente no existe devuelve null.
* Dado un iban y una cantidad, sacarla cantidad en la cuenta.
* Realizar una transferencia entre dos cuentas de dos clientes. Para realizar la transferencia será necesario proporcionar la cantidad, el iban de cuenta de origen y de destino
* Dado un código postal, devuelve todas las cuentas cuyo propietario vive en ese código postal

## Tienda

Implementa una estructura de clases que permita gestionar una tienda. De la tienda se debe almacenar:

* name
* productsById: los productos deben estar indexados por id de producto. Por cada producto:
  * id: de producto (entero)
  * name
  * price: double
  * tags: conjunto no ordenado de etiquetas (cada etiqueta es un String)
* customers: Conjunto de clientes ordenados por apellidos, nombre y nif. Por cada cliente
  * nif (String)
  * name
  * surnmae
  * orders: lista de pedidos, por cada pedido:
    * id: int
    * date
    * price: double
    * items: lista de items del pedido, por cada item:
      * productId: entero
      * amount

Implementa los siguientes métodos en la clase Shop:

* Dado un nif, devuelve el cliente con ese NIF.
* Dado un nif y un id de pedido, devuelve el pedido del cliente.
* Dado un id de producto, devuelve el producto con ese id.
* Dado un nif y un id de pedido, devuelve una lista con los productos que se han pedido.
* Dado una etiqueta (String), devuelve una lista de productos que tienen esa etiqueta.
* Dado un nif, devuelve cuánto se ha gastado el cliente en la tienda.
